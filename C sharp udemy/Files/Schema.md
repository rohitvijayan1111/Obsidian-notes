-- ============================================================
-- EXTENSIONS & ENUM TYPES
-- ============================================================

CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
CREATE EXTENSION IF NOT EXISTS ltree;

CREATE TYPE work_status AS ENUM (
    'not_started', 'in_progress', 'submitted',
    'under_review', 'approved', 'sent_back', 'locked'
);
CREATE TYPE review_action      AS ENUM ('approved', 'sent_back', 'reviewed');
CREATE TYPE section_node_type  AS ENUM ('section', 'subsection');
CREATE TYPE content_block_type AS ENUM (
    'text', 'table', 'image', 'chart', 'file_attachment', 'rich_text'
);
CREATE TYPE access_level       AS ENUM ('view', 'edit', 'review', 'approve');
CREATE TYPE workflow_step_type AS ENUM ('submit', 'review', 'approve', 'lock');
CREATE TYPE assignee_type      AS ENUM ('user', 'department');
CREATE TYPE language_status    AS ENUM ('draft', 'complete', 'locked');
CREATE TYPE export_format      AS ENUM ('pdf', 'docx', 'html');
CREATE TYPE audit_event_type   AS ENUM (
    'create', 'update', 'delete', 'status_change',
    'version_snapshot', 'archive', 'lock', 'access_change'
);


-- ============================================================
-- DOMAIN 1 — IDENTITY
-- ============================================================

CREATE TABLE institutes (
    id         UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    name       TEXT        NOT NULL,
    code       TEXT        NOT NULL,
    settings   JSONB       NOT NULL DEFAULT '{}',
    created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
    deleted_at TIMESTAMPTZ
);
CREATE UNIQUE INDEX uq_institutes_code
    ON institutes (code) WHERE deleted_at IS NULL;


CREATE TABLE languages (
    id        UUID    PRIMARY KEY DEFAULT gen_random_uuid(),
    code      TEXT    NOT NULL,
    name      TEXT    NOT NULL,
    is_rtl    BOOLEAN NOT NULL DEFAULT false,
    is_active BOOLEAN NOT NULL DEFAULT true
);
CREATE UNIQUE INDEX uq_languages_code ON languages (code);


CREATE TABLE departments (
    id                   UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    institute_id         UUID        NOT NULL REFERENCES institutes (id),
    parent_department_id UUID        REFERENCES departments (id),
    name                 TEXT        NOT NULL,
    code                 TEXT        NOT NULL,
    metadata             JSONB       NOT NULL DEFAULT '{}',
    created_at           TIMESTAMPTZ NOT NULL DEFAULT now(),
    deleted_at           TIMESTAMPTZ
);
CREATE INDEX idx_departments_institute ON departments (institute_id);
CREATE INDEX idx_departments_parent    ON departments (parent_department_id);
CREATE UNIQUE INDEX uq_departments_code
    ON departments (institute_id, code) WHERE deleted_at IS NULL;


CREATE TABLE users (
    id            UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    institute_id  UUID        NOT NULL REFERENCES institutes (id),
    department_id UUID        REFERENCES departments (id),
    email         TEXT        NOT NULL,
    full_name     TEXT        NOT NULL,
    role          TEXT        NOT NULL,
    preferences   JSONB       NOT NULL DEFAULT '{}',
    is_active     BOOLEAN     NOT NULL DEFAULT true,
    created_at    TIMESTAMPTZ NOT NULL DEFAULT now(),
    deleted_at    TIMESTAMPTZ
);
CREATE INDEX idx_users_institute  ON users (institute_id);
CREATE INDEX idx_users_department ON users (department_id);
CREATE UNIQUE INDEX uq_users_email
    ON users (institute_id, email) WHERE deleted_at IS NULL;


-- ============================================================
-- DOMAIN 2 — APPROVAL WORKFLOW TEMPLATES
-- ============================================================

CREATE TABLE approval_workflows (
    id           UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    institute_id UUID        NOT NULL REFERENCES institutes (id),
    name         TEXT        NOT NULL,
    description  TEXT,
    is_active    BOOLEAN     NOT NULL DEFAULT true,
    created_by   UUID        NOT NULL REFERENCES users (id),
    created_at   TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX idx_approval_workflows_institute ON approval_workflows (institute_id);


CREATE TABLE approval_workflow_steps (
    id            UUID               PRIMARY KEY DEFAULT gen_random_uuid(),
    workflow_id   UUID               NOT NULL REFERENCES approval_workflows (id),
    step_order    SMALLINT           NOT NULL,
    step_type     workflow_step_type NOT NULL,
    name          TEXT               NOT NULL,
    role_required TEXT,
    is_optional   BOOLEAN            NOT NULL DEFAULT false,
    timeout_hours INTEGER,
    CONSTRAINT uq_workflow_step_order UNIQUE (workflow_id, step_order)
);
CREATE INDEX idx_workflow_steps_workflow ON approval_workflow_steps (workflow_id);


-- ============================================================
-- DOMAIN 3 — REPORTS
-- (cycle fields merged directly — one cycle per report)
-- ============================================================

CREATE TABLE reports (
    id                   UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    institute_id         UUID        NOT NULL REFERENCES institutes (id),
    name                 TEXT        NOT NULL,
    description          TEXT,
    reporting_year       INTEGER     NOT NULL,
    default_language_id  UUID        NOT NULL REFERENCES languages (id),
    approval_workflow_id UUID        REFERENCES approval_workflows (id),
    design_config        JSONB       NOT NULL DEFAULT '{}',
    is_template          BOOLEAN     NOT NULL DEFAULT false,
    current_version      INTEGER     NOT NULL DEFAULT 1,
    status               work_status NOT NULL DEFAULT 'not_started',

    -- Annual cycle fields (updatable — deadlines may change)
    start_date           DATE,
    end_date             DATE,
    submission_deadline  TIMESTAMPTZ,
    review_start_date    TIMESTAMPTZ,
    review_end_date      TIMESTAMPTZ,
    is_closed            BOOLEAN     NOT NULL DEFAULT false,
    closed_at            TIMESTAMPTZ,
    closed_by            UUID        REFERENCES users (id),

    created_by           UUID        NOT NULL REFERENCES users (id),
    created_at           TIMESTAMPTZ NOT NULL DEFAULT now(),
    updated_at           TIMESTAMPTZ NOT NULL DEFAULT now(),
    deleted_at           TIMESTAMPTZ
);
CREATE INDEX idx_reports_institute ON reports (institute_id);
CREATE INDEX idx_reports_year      ON reports (institute_id, reporting_year);
CREATE INDEX idx_reports_active    ON reports (institute_id) WHERE deleted_at IS NULL;


CREATE TABLE report_department_deadlines (
    id                  UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    report_id           UUID        NOT NULL REFERENCES reports (id),
    department_id       UUID        NOT NULL REFERENCES departments (id),
    submission_deadline TIMESTAMPTZ NOT NULL,
    review_deadline     TIMESTAMPTZ,
    notes               TEXT,
    CONSTRAINT uq_report_dept_deadline UNIQUE (report_id, department_id)
);
CREATE INDEX idx_report_dept_dl_dept ON report_department_deadlines (department_id);


CREATE TABLE report_user_deadlines (
    id                  UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    report_id           UUID        NOT NULL REFERENCES reports (id),
    user_id             UUID        NOT NULL REFERENCES users (id),
    submission_deadline TIMESTAMPTZ NOT NULL,
    review_deadline     TIMESTAMPTZ,
    notes               TEXT,
    CONSTRAINT uq_report_user_deadline UNIQUE (report_id, user_id)
);
CREATE INDEX idx_report_user_dl_user ON report_user_deadlines (user_id);


-- ============================================================
-- DOMAIN 4 — SECTION HIERARCHY
-- ============================================================

CREATE TABLE section_nodes (
    id                 UUID              PRIMARY KEY DEFAULT gen_random_uuid(),
    report_id          UUID              NOT NULL REFERENCES reports (id),
    parent_id          UUID              REFERENCES section_nodes (id),
    node_type          section_node_type NOT NULL,
    name               TEXT              NOT NULL,
    description        TEXT,
    position           SMALLINT          NOT NULL DEFAULT 0,
    path               LTREE             NOT NULL,
    data_source_config JSONB,
    design_config      JSONB             NOT NULL DEFAULT '{}',
    is_locked          BOOLEAN           NOT NULL DEFAULT false,
    created_by         UUID              NOT NULL REFERENCES users (id),
    created_at         TIMESTAMPTZ       NOT NULL DEFAULT now(),
    updated_at         TIMESTAMPTZ       NOT NULL DEFAULT now(),
    deleted_at         TIMESTAMPTZ
);
CREATE INDEX idx_section_nodes_report   ON section_nodes (report_id);
CREATE INDEX idx_section_nodes_parent   ON section_nodes (parent_id);
CREATE INDEX idx_section_nodes_path     ON section_nodes USING GIST (path);
CREATE INDEX idx_section_nodes_position ON section_nodes (report_id, position);
CREATE INDEX idx_section_nodes_active   ON section_nodes (report_id) WHERE deleted_at IS NULL;


CREATE TABLE section_node_translations (
    id              UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    section_node_id UUID        NOT NULL REFERENCES section_nodes (id),
    language_id     UUID        NOT NULL REFERENCES languages (id),
    name            TEXT        NOT NULL,
    description     TEXT,
    created_at      TIMESTAMPTZ NOT NULL DEFAULT now(),
    updated_at      TIMESTAMPTZ NOT NULL DEFAULT now(),
    CONSTRAINT uq_section_node_lang UNIQUE (section_node_id, language_id)
);


CREATE TABLE section_node_assignments (
    id               UUID          PRIMARY KEY DEFAULT gen_random_uuid(),
    section_node_id  UUID          NOT NULL REFERENCES section_nodes (id),
    report_id        UUID          NOT NULL REFERENCES reports (id),
    assignee_type    assignee_type NOT NULL,
    assignee_user_id UUID          REFERENCES users (id),
    assignee_dept_id UUID          REFERENCES departments (id),
    deadline         TIMESTAMPTZ,
    status           work_status   NOT NULL DEFAULT 'not_started',
    assigned_by      UUID          NOT NULL REFERENCES users (id),
    assigned_at      TIMESTAMPTZ   NOT NULL DEFAULT now(),
    CONSTRAINT chk_assignee_set
        CHECK (assignee_user_id IS NOT NULL OR assignee_dept_id IS NOT NULL),
    CONSTRAINT chk_assignee_exclusive
        CHECK (NOT (assignee_user_id IS NOT NULL AND assignee_dept_id IS NOT NULL))
);
CREATE INDEX idx_sna_section_report ON section_node_assignments (section_node_id, report_id);
CREATE INDEX idx_sna_user           ON section_node_assignments (assignee_user_id, report_id);
CREATE INDEX idx_sna_dept           ON section_node_assignments (assignee_dept_id, report_id);
CREATE INDEX idx_sna_status         ON section_node_assignments (status);


CREATE TABLE section_node_access (
    id                UUID         PRIMARY KEY DEFAULT gen_random_uuid(),
    section_node_id   UUID         NOT NULL REFERENCES section_nodes (id),
    principal_type    assignee_type NOT NULL,
    principal_user_id UUID         REFERENCES users (id),
    principal_dept_id UUID         REFERENCES departments (id),
    access_level      access_level NOT NULL,
    granted_by        UUID         NOT NULL REFERENCES users (id),
    granted_at        TIMESTAMPTZ  NOT NULL DEFAULT now(),
    revoked_at        TIMESTAMPTZ,
    CONSTRAINT chk_principal_set
        CHECK (principal_user_id IS NOT NULL OR principal_dept_id IS NOT NULL),
    CONSTRAINT chk_principal_exclusive
        CHECK (NOT (principal_user_id IS NOT NULL AND principal_dept_id IS NOT NULL))
);
CREATE INDEX idx_sna_access_node ON section_node_access (section_node_id) WHERE revoked_at IS NULL;
CREATE INDEX idx_sna_access_user ON section_node_access (principal_user_id);
CREATE INDEX idx_sna_access_dept ON section_node_access (principal_dept_id);


-- ============================================================
-- DOMAIN 5 — CONTENT
-- ============================================================

CREATE TABLE content_blocks (
    id              UUID               PRIMARY KEY DEFAULT gen_random_uuid(),
    section_node_id UUID               NOT NULL REFERENCES section_nodes (id),
    block_type      content_block_type NOT NULL,
    position        SMALLINT           NOT NULL DEFAULT 0,
    header_config   JSONB,
    style_config    JSONB              NOT NULL DEFAULT '{}',
    is_required     BOOLEAN            NOT NULL DEFAULT false,
    created_by      UUID               NOT NULL REFERENCES users (id),
    created_at      TIMESTAMPTZ        NOT NULL DEFAULT now(),
    updated_at      TIMESTAMPTZ        NOT NULL DEFAULT now(),
    deleted_at      TIMESTAMPTZ
);
CREATE INDEX idx_content_blocks_section ON content_blocks (section_node_id, position);
CREATE INDEX idx_content_blocks_active  ON content_blocks (section_node_id) WHERE deleted_at IS NULL;


CREATE TABLE content_block_versions (
    id               UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    content_block_id UUID        NOT NULL REFERENCES content_blocks (id),
    version_number   INTEGER     NOT NULL,
    report_id        UUID        NOT NULL REFERENCES reports (id),
    assignment_id    UUID        REFERENCES section_node_assignments (id),
    content          JSONB       NOT NULL,
    plain_text_snapshot TEXT,
    language_id      UUID        NOT NULL REFERENCES languages (id),
    is_current       BOOLEAN     NOT NULL DEFAULT false,
    change_summary   TEXT,
    created_by       UUID        NOT NULL REFERENCES users (id),
    created_at       TIMESTAMPTZ NOT NULL DEFAULT now(),
    CONSTRAINT uq_block_version_lang UNIQUE (content_block_id, version_number, language_id)
);
CREATE INDEX idx_cbv_block_current
    ON content_block_versions (content_block_id) WHERE is_current = true;
CREATE INDEX idx_cbv_report ON content_block_versions (report_id);
CREATE INDEX idx_cbv_fts
    ON content_block_versions USING GIN (
        to_tsvector('english', coalesce(plain_text_snapshot, ''))
    );


CREATE TABLE content_block_translations (
    id                       UUID            PRIMARY KEY DEFAULT gen_random_uuid(),
    content_block_version_id UUID            NOT NULL REFERENCES content_block_versions (id),
    language_id              UUID            NOT NULL REFERENCES languages (id),
    content                  JSONB           NOT NULL,
    plain_text_snapshot      TEXT,
    status                   language_status NOT NULL DEFAULT 'draft',
    translated_by            UUID            REFERENCES users (id),
    reviewed_by              UUID            REFERENCES users (id),
    created_at               TIMESTAMPTZ     NOT NULL DEFAULT now(),
    updated_at               TIMESTAMPTZ     NOT NULL DEFAULT now(),
    CONSTRAINT uq_cbt_version_lang UNIQUE (content_block_version_id, language_id)
);
CREATE INDEX idx_cbt_language ON content_block_translations (language_id, status);


CREATE TABLE compiled_reports (
    id               UUID          PRIMARY KEY DEFAULT gen_random_uuid(),
    report_id        UUID          NOT NULL REFERENCES reports (id),
    language_id      UUID          NOT NULL REFERENCES languages (id),
    format           export_format NOT NULL,
    version_snapshot INTEGER       NOT NULL,
    storage_url      TEXT,
    compiled_at      TIMESTAMPTZ   NOT NULL DEFAULT now(),
    compiled_by      UUID          NOT NULL REFERENCES users (id),
    checksum         TEXT,
    metadata         JSONB         NOT NULL DEFAULT '{}',
    CONSTRAINT uq_compiled_report UNIQUE (report_id, language_id, format, version_snapshot)
);
CREATE INDEX idx_compiled_reports_report ON compiled_reports (report_id);


-- ============================================================
-- DOMAIN 6 — SUBMISSION REVIEWS
-- ============================================================

CREATE TABLE submission_reviews (
    id                  UUID          PRIMARY KEY DEFAULT gen_random_uuid(),
    assignment_id       UUID          NOT NULL REFERENCES section_node_assignments (id),
    workflow_step_id    UUID          REFERENCES approval_workflow_steps (id),
    report_id           UUID          NOT NULL REFERENCES reports (id),
    action              review_action NOT NULL,
    reviewed_by         UUID          NOT NULL REFERENCES users (id),
    reviewed_at         TIMESTAMPTZ   NOT NULL DEFAULT now(),
    comments            TEXT,
    reviewed_version_id UUID          REFERENCES content_block_versions (id),
    next_step_id        UUID          REFERENCES approval_workflow_steps (id)
);
CREATE INDEX idx_submission_reviews_assignment ON submission_reviews (assignment_id);
CREATE INDEX idx_submission_reviews_report     ON submission_reviews (report_id, reviewed_by);
CREATE INDEX idx_submission_reviews_action     ON submission_reviews (action, report_id);


-- ============================================================
-- DOMAIN 7 — COMMENTS & COLLABORATION
-- ============================================================

CREATE TABLE comments (
    id                       UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    content_block_version_id UUID        NOT NULL REFERENCES content_block_versions (id),
    parent_comment_id        UUID        REFERENCES comments (id),
    author_id                UUID        NOT NULL REFERENCES users (id),
    body                     TEXT        NOT NULL,
    is_resolved              BOOLEAN     NOT NULL DEFAULT false,
    resolved_by              UUID        REFERENCES users (id),
    resolved_at              TIMESTAMPTZ,
    created_at               TIMESTAMPTZ NOT NULL DEFAULT now(),
    updated_at               TIMESTAMPTZ NOT NULL DEFAULT now(),
    deleted_at               TIMESTAMPTZ
);
CREATE INDEX idx_comments_version  ON comments (content_block_version_id);
CREATE INDEX idx_comments_parent   ON comments (parent_comment_id);
CREATE INDEX idx_comments_author   ON comments (author_id);
CREATE INDEX idx_comments_resolved ON comments (is_resolved, content_block_version_id);


CREATE TABLE comment_mentions (
    id                UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    comment_id        UUID NOT NULL REFERENCES comments (id),
    mentioned_user_id UUID NOT NULL REFERENCES users (id),
    CONSTRAINT uq_comment_mention UNIQUE (comment_id, mentioned_user_id)
);
CREATE INDEX idx_comment_mentions_user ON comment_mentions (mentioned_user_id);


-- ============================================================
-- DOMAIN 8 — AUDIT & VERSION HISTORY
-- ============================================================

CREATE TABLE audit_logs (
    id           UUID             PRIMARY KEY DEFAULT gen_random_uuid(),
    institute_id UUID             NOT NULL REFERENCES institutes (id),
    event_type   audit_event_type NOT NULL,
    actor_id     UUID             REFERENCES users (id),
    entity_type  TEXT             NOT NULL,
    entity_id    UUID             NOT NULL,
    report_id    UUID             REFERENCES reports (id),
    before_state JSONB,
    after_state  JSONB,
    diff         JSONB,
    ip_address   INET,
    user_agent   TEXT,
    occurred_at  TIMESTAMPTZ      NOT NULL DEFAULT now()
) PARTITION BY RANGE (occurred_at);

CREATE TABLE audit_logs_2026_04 PARTITION OF audit_logs
    FOR VALUES FROM ('2026-04-01') TO ('2026-05-01');
CREATE TABLE audit_logs_2026_05 PARTITION OF audit_logs
    FOR VALUES FROM ('2026-05-01') TO ('2026-06-01');

CREATE INDEX idx_audit_institute ON audit_logs (institute_id, occurred_at DESC);
CREATE INDEX idx_audit_entity    ON audit_logs (entity_type, entity_id);
CREATE INDEX idx_audit_report    ON audit_logs (report_id, occurred_at DESC);
CREATE INDEX idx_audit_actor     ON audit_logs (actor_id);


CREATE TABLE report_version_snapshots (
    id              UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    report_id       UUID        NOT NULL REFERENCES reports (id),
    version_number  INTEGER     NOT NULL,
    snapshot        JSONB       NOT NULL,
    snapshot_reason TEXT,
    created_by      UUID        NOT NULL REFERENCES users (id),
    created_at      TIMESTAMPTZ NOT NULL DEFAULT now(),
    CONSTRAINT uq_report_version UNIQUE (report_id, version_number)
);
CREATE INDEX idx_rvs_report ON report_version_snapshots (report_id);


-- ============================================================
-- DOMAIN 9 — ANALYTICS & DASHBOARDS
-- ============================================================

CREATE TABLE section_completion_snapshots (
    id                    UUID         PRIMARY KEY DEFAULT gen_random_uuid(),
    report_id             UUID         NOT NULL REFERENCES reports (id),
    section_node_id       UUID         NOT NULL REFERENCES section_nodes (id),
    department_id         UUID         REFERENCES departments (id),
    total_assignments     INTEGER      NOT NULL DEFAULT 0,
    completed_assignments INTEGER      NOT NULL DEFAULT 0,
    overdue_assignments   INTEGER      NOT NULL DEFAULT 0,
    completion_pct        NUMERIC(5,2) NOT NULL DEFAULT 0.00,
    snapshot_at           TIMESTAMPTZ  NOT NULL DEFAULT now()
);
CREATE INDEX idx_scs_report     ON section_completion_snapshots (report_id, snapshot_at DESC);
CREATE INDEX idx_scs_section    ON section_completion_snapshots (section_node_id, report_id);
CREATE INDEX idx_scs_department ON section_completion_snapshots (department_id, report_id);


CREATE MATERIALIZED VIEW v_assignment_overdue AS
SELECT
    sna.id                                                  AS assignment_id,
    sna.section_node_id,
    sna.report_id,
    sna.assignee_type,
    sna.assignee_user_id,
    sna.assignee_dept_id,
    sna.deadline,
    sna.status,
    r.reporting_year,
    EXTRACT(EPOCH FROM (now() - sna.deadline)) / 3600       AS hours_overdue
FROM section_node_assignments sna
JOIN reports r ON r.id = sna.report_id
WHERE
    sna.status NOT IN ('approved', 'locked')
    AND sna.deadline < now()
    AND r.is_closed = false;

CREATE UNIQUE INDEX ON v_assignment_overdue (assignment_id);


-- ============================================================
-- DOMAIN 10 — NOTIFICATIONS
-- ============================================================

CREATE TABLE notifications (
    id                UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    institute_id      UUID        NOT NULL REFERENCES institutes (id),
    recipient_user_id UUID        NOT NULL REFERENCES users (id),
    event_type        TEXT        NOT NULL,
    payload           JSONB       NOT NULL DEFAULT '{}',
    is_read           BOOLEAN     NOT NULL DEFAULT false,
    read_at           TIMESTAMPTZ,
    created_at        TIMESTAMPTZ NOT NULL DEFAULT now()
);
CREATE INDEX idx_notifications_user
    ON notifications (recipient_user_id, is_read, created_at DESC);
CREATE INDEX idx_notifications_institute
    ON notifications (institute_id, created_at DESC);



Let me first update the plan file with the fix, then give you a full data walkthrough.

Now the full data walkthrough — I'll use a single realistic example traced through every table.

---

## The scenario

> **Institute:** AIIA (All India Institute of Ayurveda) **Report:** Annual Report 2026 **Structure:** Section → "Research Activities" → Subsection → "Publications" → Content Block → a table of publications **Assignee:** Dr. Sharma (user) fills it in. Dept of Research also assigned. **Language:** English (default) + Hindi

---

## Step 1 — `institutes`

One row per institution.

|id|name|code|
|---|---|---|
|`inst-001`|All India Institute of Ayurveda|AIIA|

---

## Step 2 — `users` & `departments`

```
departments
─────────────────────────────────────────────────────
id          institute_id   name                  code
dept-001    inst-001       Department of Research RES
```

```
users
─────────────────────────────────────────────────────────────────────
id          institute_id   department_id   full_name       role
user-001    inst-001       dept-001        Dr. Sharma      contributor
user-002    inst-001       dept-001        Dr. Mehta       reviewer
user-003    inst-001       NULL            Admin User      admin
```

---

## Step 3 — `reports`

One row = the entire annual report. Cycle dates live here directly.

```
reports
──────────────────────────────────────────────────────────────────────────────
id          institute_id  name                reporting_year  start_date  end_date    submission_deadline   status
rpt-001     inst-001      Annual Report 2026  2026            2026-01-01  2026-12-31  2026-11-30 23:59:00   in_progress
```

---

## Step 4 — `section_nodes`

This is where sections AND subsections both live — same table, distinguished by `node_type`. The `path` column (ltree) encodes the tree position.

```
section_nodes
────────────────────────────────────────────────────────────────────────────────────────────────
id          report_id  parent_id   node_type    name                  position  path
sn-001      rpt-001    NULL        section      Research Activities   1         rpt001.sn001
sn-002      rpt-001    sn-001      subsection   Publications          1         rpt001.sn001.sn002
sn-003      rpt-001    sn-001      subsection   Patents               2         rpt001.sn001.sn003
sn-004      rpt-001    NULL        section      Financial Summary     2         rpt001.sn004
```

**Key point the user raised:** `section_nodes` does NOT store the content blocks inside it. It only stores the label (name, position, hierarchy). The content blocks point back to the section via FK — explained next.

---

## Step 5 — `content_blocks`

Content blocks belong to a section node via `section_node_id`. A section node can have many blocks, ordered by `position`.

```
content_blocks
──────────────────────────────────────────────────────────────────────────
id       section_node_id  block_type  position  is_required  header_config
cb-001   sn-002           table       1         true         {"columns": ["Title","Journal","Year","Authors"]}
cb-002   sn-002           rich_text   2         false        NULL
cb-003   sn-004           table       1         true         {"columns": ["Head","Budget","Spent"]}
```

So `sn-002` (Publications subsection) owns two blocks: a publications table and a rich text block below it.

**The relationship is:** `section_nodes` ← `content_blocks.section_node_id` You get all blocks of a section by: `SELECT * FROM content_blocks WHERE section_node_id = 'sn-002'`

---

## Step 6 — `content_block_versions`

Every time someone saves a content block, a new **immutable row** is inserted here. The block itself (`content_blocks`) never stores the data — only versions do.

```
content_block_versions
──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
id       content_block_id  version_number  report_id  language_id  is_current  content                                          created_by
cbv-001  cb-001            1               rpt-001    lang-en      false        {"rows": []}                                     user-001
cbv-002  cb-001            2               rpt-001    lang-en      true         {"rows": [{"title":"Ayurveda Study","year":2025}]}  user-001
```

- `cbv-001` = first save (empty table)
- `cbv-002` = second save (Dr. Sharma added a row) — `is_current = true`
- `cbv-001` stays in the table forever → this is your version history

To get the **current content** of block `cb-001`:

```sql
SELECT * FROM content_block_versions
WHERE content_block_id = 'cb-001' AND is_current = true;
```

To **compare versions**:

```sql
SELECT * FROM content_block_versions
WHERE content_block_id = 'cb-001'
ORDER BY version_number;
```

---

## Step 7 — `content_block_translations`

For each version, each language gets its own row here.

```
content_block_translations
──────────────────────────────────────────────────────────────────────────────────
id       content_block_version_id  language_id  status    content
cbt-001  cbv-002                   lang-hi       draft     {"rows": [{"title":"आयुर्वेद अध्ययन","year":2025}]}
```

- Base English content lives in `content_block_versions.content`
- Hindi translation lives here in `content_block_translations`
- `status = draft` means translator hasn't marked it complete yet

---

## Step 8 — `section_node_assignments`

Same section node gets **multiple rows** — one per assignee. This is how multiple users and departments are handled.

```
section_node_assignments
────────────────────────────────────────────────────────────────────────────────────────────
id       section_node_id  report_id  assignee_type  assignee_user_id  assignee_dept_id  status        deadline
sna-001  sn-002           rpt-001    user           user-001          NULL              in_progress   2026-10-31
sna-002  sn-002           rpt-001    department     NULL              dept-001          not_started   2026-10-31
sna-003  sn-001           rpt-001    user           user-001          NULL              not_started   NULL
```

- `sna-001`: Dr. Sharma assigned to Publications subsection
- `sna-002`: Research Department also assigned to Publications subsection
- `sna-003`: Dr. Sharma assigned to the parent section too

The partial unique indexes ensure you can't accidentally assign Dr. Sharma to the same section twice.

---

## Step 9 — `section_node_translations`

Translates only the **section name and description** — not the content.

```
section_node_translations
────────────────────────────────────────────────────────────────────────
id       section_node_id  language_id  name                    description
snt-001  sn-001           lang-en      Research Activities     All research output for 2026
snt-002  sn-001           lang-hi      अनुसंधान गतिविधियाँ     2026 के लिए सभी शोध उत्पाद
snt-003  sn-002           lang-en      Publications            Peer-reviewed journals and books
snt-004  sn-002           lang-hi      प्रकाशन                 समीक्षित पत्रिकाएँ और पुस्तकें
```

---

## Step 10 — `submission_reviews`

When Dr. Mehta reviews Dr. Sharma's submission on assignment `sna-001`:

```
submission_reviews
──────────────────────────────────────────────────────────────────────────────────────────
id       assignment_id  report_id  action     reviewed_by  reviewed_at          comments
sr-001   sna-001        rpt-001    sent_back  user-002     2026-10-15 14:00:00  Please add DOI column
sr-002   sna-001        rpt-001    approved   user-002     2026-10-20 10:00:00  NULL
```

Full audit trail: sent back → corrected → approved. Both rows stay.

---

## Step 11 — `comments`

Dr. Mehta adds a comment on a specific version of the block:

```
comments
────────────────────────────────────────────────────────────────────────────────────────
id      content_block_version_id  parent_comment_id  author_id  body                          is_resolved
c-001   cbv-001                   NULL               user-002   The 2024 papers are missing   false
c-002   cbv-001                   c-001              user-001   Added in v2, please recheck   false
```

Anchored to `cbv-001` (version 1) — so even after version 2 exists, this comment context is preserved.

---

## Step 12 — `audit_logs`

Every change anywhere produces an append-only row:

```
audit_logs
───────────────────────────────────────────────────────────────────────────────────────────────────────────
id       institute_id  event_type     actor_id   entity_type            entity_id  before_state        after_state
al-001   inst-001      create         user-001   content_block_version  cbv-002    NULL                {"rows":[...]}
al-002   inst-001      status_change  user-002   section_node_assign    sna-001    {"status":"subm...} {"status":"under_review"}
```

---

## Full Picture — How it all connects

```
institutes
└── reports
      ├── section_nodes (the tree)
      │     ├── section_node_translations  (translated names)
      │     ├── section_node_assignments   (who is assigned — multiple rows per section)
      │     │     └── submission_reviews   (every review action)
      │     ├── section_node_access        (who can view/edit/review)
      │     └── content_blocks             (blocks inside the section)
      │           └── content_block_versions  (every save = new row)
      │                 ├── content          (JSONB — the actual data)
      │                 ├── content_block_translations  (per language)
      │                 └── comments         (anchored to this version)
      ├── report_department_deadlines
      ├── report_user_deadlines
      ├── compiled_reports               (final PDF/DOCX/HTML artifacts)
      └── report_version_snapshots       (structural snapshot on close)

audit_logs   — one row per change, forever
notifications — one row per event per recipient
```

---

## The key mental model

|Entity|Stores|Does NOT store|
|---|---|---|
|`section_nodes`|Section name, position, hierarchy, lock state|Content, who filled it|
|`content_blocks`|Block type, style config, column headers|The actual data|
|`content_block_versions`|The actual data (JSONB), per save, per language|Nothing mutable|
|`section_node_assignments`|Who is assigned, their status, deadline|Content|
|`submission_reviews`|Review actions taken|Content|

Does this make the data flow clear enough to validate? Let me know which part you'd like to dig into further.