Here’s a clearer, well-structured version of your requirements:

---

# **Report Management System – Requirements**

## **1. Report Setup & Configuration**

- Define **report name**.
    
- Configure **reporting cycles**, including:
    
    - Start date and end date
        
    - Review timelines
        
    - Reporting year(s)
        
- Allow **intermediate deadlines** for departments and individual users.
    

---

---

## **2. Sections & Content Structure**

- Create **sections and subsections** with custom names.
- Define **content blocks** within each section/subsection.
- Content blocks should remain **editable during report creation**, and users should also be able to **add, modify, or remove sections and subsections** as needed.
- Allow assigning the **same section/subsection to multiple users or departments**.
- Provide an option to define:
    - **Data source at subsection level**, or
    - **Data source at section level** (if subsection-level is not required).
- Enable **access control** for sections and subsections.

---

## **3. Task Assignment & Workflow**

- Assign **tasks or sections** with specific **review deadlines**.
    
- Configure a **multi-level approval workflow** for reviewing tasks.
    
- Each submission should support:
    
    - Review
        
    - Approval
        
    - Rework (send back for corrections)
        

---

## **4. Status Tracking**

- Support the following statuses:
    
    - Not Started
        
    - In Progress
        
    - Submitted
        
    - Under Review
        
    - Approved
        
    - Sent Back
        
    - Locked
        
- Provide **filters and dashboards** for institute-level monitoring.
    

---

## **5. Review & Collaboration**

- Enable reviewers to:
    
    - Add **comments on specific content blocks**
        
    - Track **changes and version history**
        
    - **Compare current and previous versions**
        

---

## **6. Version Control & Modifications**

- Implement a **version control system** for reports.
    
- Allow **modification of report structure** while preserving previous versions.
    
- Maintain full **audit history** of changes.
    

---

## **7. Reporting Cycle Closure & Archival**

- Provide the ability to:
    
    - **Close a reporting cycle**
        
    - **Lock further edits**
        
    - **Archive the final report** along with all supporting data for auditing and reference
        

---

## **8. Multi-language Support**

- Allow **multiple language variants per section**.
    
- Generate **language-specific compiled reports**.
    
- Ensure **content consistency across languages**.
    

---

## **9. UI & Design Customization**

- Support customization of:
    
    - **Table headers**
        
    - **Text styles**
        
    - Overall **color schemes**
        

---

## **10. Dashboards & Insights**

- Provide dashboards displaying:
    
    - **Completion percentage** by section and department
        
    - **Overdue tasks**
        
    - **Bottlenecks**
        
- Enable **real-time monitoring** for timely completion of reports.




# Report Management System — PostgreSQL Database Design Plan

## Context

The goal is to design a production-ready PostgreSQL schema for a Report Management System that supports multi-department reporting cycles, hierarchical content structures, multi-level approval workflows, version control, multi-language output, and real-time dashboards. This is a greenfield project — no existing schema exists.

---

## ENUM Types

```sql
CREATE TYPE work_status AS ENUM (
    'not_started', 'in_progress', 'submitted',
    'under_review', 'approved', 'sent_back', 'locked'
);
CREATE TYPE review_action AS ENUM ('approved', 'sent_back', 'reviewed');
CREATE TYPE section_node_type AS ENUM ('section', 'subsection');
CREATE TYPE content_block_type AS ENUM ('text', 'table', 'image', 'chart', 'file_attachment', 'rich_text');
CREATE TYPE data_source_level AS ENUM ('section', 'subsection');
CREATE TYPE access_level AS ENUM ('view', 'edit', 'review', 'approve');
CREATE TYPE workflow_step_type AS ENUM ('submit', 'review', 'approve', 'lock');
CREATE TYPE assignee_type AS ENUM ('user', 'department');
CREATE TYPE language_status AS ENUM ('draft', 'complete', 'locked');
CREATE TYPE audit_event_type AS ENUM (
    'create', 'update', 'delete', 'status_change',
    'version_snapshot', 'archive', 'lock', 'access_change'
);
```

---

## Tables (22 tables + 1 materialized view)

### Domain: Identity & Organization

#### `institutes`
The top-level entity. Each institute is an independent reporting entity (e.g., AIIA, CCRYN, NCISM). **All operational tables (reports, departments, users) are scoped to `institute_id`.** No parent organization table exists.

Key columns: `id`, `name`, `code` (unique), `settings: jsonb`, `created_at`, `deleted_at`.
Index: `UNIQUE(code) WHERE deleted_at IS NULL`.

#### `departments`
Hierarchical via `parent_department_id` self-reference. Scoped to an `institute_id`. `code` unique per institute. Soft-deleted.

Key columns: `id`, `institute_id (FK → institutes)`, `parent_department_id (self-ref)`, `name`, `code`, `metadata: jsonb`, `created_at`, `deleted_at`.
Index: `UNIQUE(institute_id, code) WHERE deleted_at IS NULL`.

#### `users`
Belongs to one institute and optionally one department. `role` (text) for broad RBAC. `preferences: jsonb` for UI/language preferences.

Key columns: `id`, `institute_id (FK → institutes)`, `department_id (FK)`, `email`, `full_name`, `role`, `preferences: jsonb`, `is_active`, `created_at`, `deleted_at`.
Index: `UNIQUE(institute_id, email) WHERE deleted_at IS NULL`.

#### `languages`
Global registry. `code` (ISO 639-1), `is_rtl` flag. Not institute-scoped — shared across all institutes.

---

### Domain: Report Configuration

#### `reports`
Top-level entity. Scoped to an **institute** (not organization). Links to one `approval_workflow`. `design_config: jsonb` stores color scheme, fonts, branding. `current_version: int` is a monotonic counter bumped on structural changes.

Key change: `institute_id (FK → institutes)` replaces a direct `organization_id` FK on reports; org-level access is derived via institute.

#### `report_cycles`
Each report has one or more cycles (start/end date, review dates, submission deadline). Only one can be `is_active` at a time. `is_closed` triggers archival.

#### `report_cycle_department_deadlines`
Per-department deadline overrides within a cycle. `UNIQUE(cycle_id, department_id)`.

#### `report_cycle_user_deadlines`
Per-user deadline overrides. `UNIQUE(cycle_id, user_id)`.

---

### Domain: Section Hierarchy

```sql
CREATE EXTENSION IF NOT EXISTS ltree;
```

#### `section_nodes`
Single table for both sections and subsections. `node_type` discriminator. `parent_id` self-reference. `path: ltree` for fast ancestor/descendant queries. `position: smallint` for ordered siblings. `data_source_config: jsonb` when data source is defined at this level. Soft-deleted.

Key indexes: `USING GIST (path)`, `(report_id, position)`.

#### `section_node_assignments`
Maps a section node to a user OR department within a specific cycle. Enforces XOR via check constraints. Tracks `status: work_status` and optional deadline override.

#### `section_node_access`
Fine-grained ACL per section node. Soft-revoked via `revoked_at`. Enforces `UNIQUE(section_node_id, principal, ...)` while active.

#### `section_node_translations`
Translated names/descriptions per section node per language. `UNIQUE(section_node_id, language_id)`.

---

### Domain: Content

#### `content_blocks`
Leaf-level blocks within a section. `block_type` enum. `header_config: jsonb` for table column definitions. `style_config: jsonb` for text styling. Ordered by `position` within a section.

#### `content_block_versions`
**Core of version control.** Immutable row per save, per block, per language. `content: jsonb` holds the actual payload (rich text delta, table rows, chart config, etc.). `plain_text_snapshot` for full-text search. `is_current: boolean` is a denormalized fast-path flag (updated in same transaction as insert).

Key indexes: `UNIQUE(content_block_id, version_number, language_id)`, `(content_block_id, is_current) WHERE is_current`.

#### `content_block_translations`
Language-specific content per version. `UNIQUE(content_block_version_id, language_id)`. `status: language_status` tracks translation progress.

#### `compiled_reports`
Fully assembled per-language, per-format artifacts. One row per (cycle × language × format × version). Points to blob storage via `storage_url`. `checksum` for integrity verification.

New `format` ENUM:
```sql
CREATE TYPE export_format AS ENUM ('pdf', 'docx', 'html');
```

Key columns: `id`, `report_id (FK)`, `cycle_id (FK)`, `language_id (FK)`, `format: export_format`, `version_snapshot: int`, `storage_url`, `compiled_at`, `compiled_by (FK → users)`, `checksum`, `metadata: jsonb`.

Index: `UNIQUE(cycle_id, language_id, format, version_snapshot)`.

---

### Domain: Workflow

#### `approval_workflows`
Reusable workflow templates. Decoupled from reports — a report points to a workflow by FK.

#### `approval_workflow_steps`
Ordered steps within a workflow. `step_order` enforces sequence. `role_required` for RBAC gating. `timeout_hours` triggers escalation if no action.

#### `submission_reviews`
Records every review action (approved / sent_back / reviewed) on a section assignment. References the workflow step active at review time. Tracks which content version was reviewed.

---

### Domain: Comments

#### `comments`
Threaded (via `parent_comment_id`) and anchored to a specific `content_block_version_id`. `is_resolved` flag with resolver/timestamp. Soft-deleted.

#### `comment_mentions`
@mention tracking for notifications. `UNIQUE(comment_id, mentioned_user_id)`.

---

### Domain: Audit & Version History

#### `audit_logs`
Strictly append-only. `before_state` / `after_state` are full JSONB row snapshots. Partitioned by `occurred_at` (monthly range partitions) for archive efficiency.

Key indexes: `(institute_id, occurred_at DESC)`, `(entity_type, entity_id)`, `(report_id, occurred_at DESC)`.

#### `report_version_snapshots`
Structural snapshot of the full section tree at cycle close or before restructuring. `snapshot: jsonb` stores the full hierarchy. Two-level versioning: structural (here) + content (in `content_block_versions`).

---

### Domain: Analytics & Dashboards

#### `section_completion_snapshots`
Periodically refreshed (background job / pg_cron) aggregate per cycle + section + department. Powers dashboard completion % without real-time aggregation on hot tables.

#### `v_assignment_overdue` (materialized view)
Refreshed every 5 min. Joins `section_node_assignments` with `report_cycles` to surface overdue, non-locked assignments with `hours_overdue`.

---

### Domain: Notifications

#### `notifications`
In-app notification log. `event_type` (text), `payload: jsonb` for rich context. `is_read` flag with `read_at` timestamp. Index on `(recipient_user_id, is_read, created_at DESC)` for unread inbox queries.

---

## Entity Relationship Diagram (Text)

```
institutes  ← top-level entity
    ├── departments (self-ref hierarchy, scoped to institute)
    ├── users (scoped to institute + optional department)
    └── reports (scoped to institute)
          │     ├── report_cycles
          │     │     ├── report_cycle_department_deadlines
          │     │     ├── report_cycle_user_deadlines
          │     │     ├── compiled_reports (per language × format)
          │     │     └── report_version_snapshots
          │     ├── section_nodes (self-ref, ltree path)
          │     │     ├── section_node_translations (per language)
          │     │     ├── section_node_assignments (per cycle)
          │     │     │     └── submission_reviews
          │     │     ├── section_node_access
          │     │     └── content_blocks
          │     │           └── content_block_versions (per language + version)
          │     │                 ├── content_block_translations
          │     │                 └── comments → comment_mentions
          │     └── approval_workflows
          │           └── approval_workflow_steps

audit_logs        (cross-cutting, append-only, partitioned)
notifications     (cross-cutting, per user)
section_completion_snapshots  (analytics)
v_assignment_overdue          (materialized view)
```

---

## Key Design Decisions

| Decision | Rationale |
|---|---|
| **`ltree` for sections** | Avoid recursive CTEs on every tree query; GiST index enables ancestor/descendant in O(log n) |
| **Two-level versioning** | `content_block_versions` for content diff; `report_version_snapshots` for structural diff at cycle boundaries |
| **JSONB for content payloads** | Heterogeneous block types (rich text, tables, charts) can't be normalized — JSONB with `plain_text_snapshot` for FTS |
| **JSONB for design config** | UI customization evolves frequently; avoids schema migrations for each new style property |
| **Denormalized `is_current`** | Avoids `MAX(version_number)` subquery on hot read path; updated atomically in same transaction |
| **Soft deletes throughout** | Preserves referential integrity for audit logs; all active-record indexes are partial `WHERE deleted_at IS NULL` |
| **`audit_logs` append-only + partitioned** | Monthly range partitions enable cheap archival; JSONB snapshots enable point-in-time reconstruction |
| **`institutes` as top-level entity** | No organization layer — institutes are the root. All reports, users, departments, and audit logs scope directly to `institute_id` |
| **`export_format` ENUM on compiled_reports** | One row per format (pdf/docx/html) per language per cycle; `UNIQUE(cycle_id, language_id, format, version_snapshot)` ensures no duplicate artifacts |
| **Workflow decoupled from reports** | Reusable templates; workflow definition is immutable once in use — changes require new version |
| **Completion snapshots** | Dashboard reads hit snapshots (refreshed async), not the live assignment table — separates read/write path |

---

## Archival / Cycle Closure Sequence

When `report_cycles.is_closed = true`:
1. Set all `section_node_assignments.status = 'locked'` for that cycle
2. Insert `report_version_snapshots` row with full structural JSONB snapshot
3. Insert `compiled_reports` rows — one per (language × format: pdf/docx/html) — pointing to blob storage artifacts
4. Set `section_nodes.is_locked = true` for affected nodes
5. Append `audit_logs` row with `event_type = 'archive'`

No data is physically deleted. Archive is additive.

---

## Migration File Structure

| File | Contents |
|---|---|
| `db/migrations/001_enums_and_extensions.sql` | All ENUMs (including `export_format`), `ltree`, `uuid-ossp` |
| `db/migrations/002_core_identity.sql` | **institutes**, departments, users, languages |
| `db/migrations/003_reports_and_cycles.sql` | reports, report_cycles, deadline overrides |
| `db/migrations/004_section_hierarchy_and_content.sql` | section_nodes, content_blocks, versions, assignments, access, translations |
| `db/migrations/005_workflow_audit_analytics.sql` | approval_workflows, steps, submission_reviews, audit_logs, snapshots, notifications, materialized views |

---

## Verification

- Run all migrations against a fresh PostgreSQL 15+ instance and verify `\dt` shows 22 tables
- Insert a sample report → cycle → section → content block → version and verify ltree path is correct
- Submit a section assignment and run through a 2-step approval workflow; verify `submission_reviews` records both steps
- Close a cycle and verify archival sequence produces rows in `report_version_snapshots` and `compiled_reports`
- Refresh `v_assignment_overdue` and verify overdue assignments appear with correct `hours_overdue`
- Run a section completion dashboard query against `section_completion_snapshots` and verify percentage math
    