Here is the complete, final schema for all identity and auth tables with clear operational notes on when each gets written.

---

```sql
-- ============================================================
-- ENUM TYPES
-- ============================================================

CREATE TYPE auth_action AS ENUM (
    'login_success',
    'login_failed',
    'logout',
    'session_expired',
    'password_changed',
    'password_reset_requested',
    'password_reset_used',
    'account_locked',
    'account_unlocked'
);


-- ============================================================
-- TABLE: institutes
-- Already defined in the report module. Shown here for reference.
-- INSERT: When Super Admin onboards a new institute.
-- ============================================================

-- ============================================================
-- TABLE: user_credentials
--
-- Stores authentication data for each user.
-- NOT scoped to institute — auth is a system-level concern.
-- One row per user (1:1 with users).
--
-- INSERT: Immediately after a user row is created.
--         Admin provides a temporary password.
--         is_temporary = true, must_change_password = true.
--
-- UPDATE:
--   - User resets/changes their password
--     → password_hash updated, is_temporary = false,
--       must_change_password = false, password_changed_at = now()
--   - Failed login attempt
--     → failed_attempts incremented
--   - Too many failed attempts
--     → locked_until set to now() + lockout_duration
--   - Successful login
--     → failed_attempts reset to 0, last_login_at = now()
--   - Admin deactivates account
--     → is_active = false
-- ============================================================
CREATE TABLE users (
    id                   UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    institute_id         UUID        NOT NULL REFERENCES institutes (id),
    department_id        UUID        REFERENCES departments (id),
    full_name            TEXT        NOT NULL,
    email                TEXT        NOT NULL,
    profile_image_url    TEXT,
    password_hash        TEXT        NOT NULL,
    must_change_password BOOLEAN     NOT NULL DEFAULT true,
    locked_until         TIMESTAMPTZ,
    last_login_at        TIMESTAMPTZ,
    password_changed_at  TIMESTAMPTZ,
    is_active            BOOLEAN     NOT NULL DEFAULT true,
    created_by           UUID        REFERENCES users (id),
    created_at           TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE UNIQUE INDEX uq_users_email
    ON users (institute_id, email)
    WHERE is_active = true;

CREATE INDEX idx_users_institute  ON users (institute_id);
CREATE INDEX idx_users_department ON users (department_id);

-- ============================================================
-- TABLE: password_reset_tokens
--
-- Stores one-time tokens for password resets.
-- Used both for admin-created accounts (first login link)
-- and user-initiated forgot-password flows.
--
-- INSERT: When admin creates a user (initial temp token)
--         OR when a user requests a password reset.
--         Raw token is sent to user; only the SHA-256 hash
--         is stored here.
--
-- UPDATE: used_at set when the token is successfully consumed.
--         Token becomes invalid after use or after expires_at.
--
-- NOTE: Old/expired tokens can be purged periodically.
-- ============================================================

CREATE TABLE password_reset_tokens (
    id         UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id    UUID        NOT NULL REFERENCES users (id),
    token_hash TEXT        NOT NULL,
    expires_at TIMESTAMPTZ NOT NULL,
    used_at    TIMESTAMPTZ,
    created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE INDEX idx_prt_user    ON password_reset_tokens (user_id);
CREATE INDEX idx_prt_token   ON password_reset_tokens (token_hash);
CREATE INDEX idx_prt_active  ON password_reset_tokens (expires_at)
    WHERE used_at IS NULL;

-- ============================================================
-- TABLE: login_audit_logs
--
-- Immutable, append-only log of every auth event.
-- Self-contained — no JOINs needed for audit queries.
-- Retained for at least 7 years (NFR-6).
-- Partitioned monthly for archive performance.
--
-- INSERT: On EVERY auth event — success, failure, logout,
--         password change, account lock, etc.
--         Never updated or deleted.
--
-- COVERS:
--   login_success          → user authenticated, session created
--   login_failed           → wrong password or unknown email
--   logout                 → user explicitly logged out
--   session_expired        → token found but expires_at passed
--   password_changed       → user set a new password
--   password_reset_requested → forgot-password triggered
--   password_reset_used    → reset token consumed
--   account_locked         → too many failed attempts
--   account_unlocked       → admin manually unlocked
-- ============================================================

CREATE TABLE login_audit_logs (
    id              UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id         UUID        REFERENCES users (id), -- NULL for unknown-email login attempts
    email_attempted TEXT,                              -- what was typed, even if user not found
    action          auth_action NOT NULL,
    ip_address      INET,
    user_agent      TEXT,
    failure_reason  TEXT,                              -- 'wrong_password', 'account_locked', etc.
    occurred_at     TIMESTAMPTZ NOT NULL DEFAULT now()
) PARTITION BY RANGE (occurred_at);

-- Create one partition per month (add each month in advance via migration)
CREATE TABLE login_audit_logs_2026_04 PARTITION OF login_audit_logs
    FOR VALUES FROM ('2026-04-01') TO ('2026-05-01');
CREATE TABLE login_audit_logs_2026_05 PARTITION OF login_audit_logs
    FOR VALUES FROM ('2026-05-01') TO ('2026-06-01');

CREATE INDEX idx_lal_user     ON login_audit_logs (user_id, occurred_at DESC);
CREATE INDEX idx_lal_action   ON login_audit_logs (action,  occurred_at DESC);
CREATE INDEX idx_lal_occurred ON login_audit_logs (occurred_at DESC);


-- ============================================================
-- TABLE: roles
--
-- Predefined system roles. Seeded at deployment time.
-- These rows are never created by end users.
-- is_system = true means the row cannot be deleted via UI.
--
-- INSERT: Only at migration/deployment time (seed data below).
-- UPDATE: display_name, description, permissions JSONB can be
--         updated by Super Admin to adjust feature flags.
-- DELETE: Not allowed for system roles.
-- ============================================================

CREATE TABLE roles (
    id           UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    name         TEXT        NOT NULL,          -- machine key, never changes
    display_name TEXT        NOT NULL,          -- shown in UI
    description  TEXT,
    permissions  JSONB       NOT NULL DEFAULT '{}',
    is_system    BOOLEAN     NOT NULL DEFAULT true,
    created_at   TIMESTAMPTZ NOT NULL DEFAULT now()
);

CREATE UNIQUE INDEX uq_roles_name ON roles (name);

/*
── SEED DATA — run at migration time ──────────────────────────

INSERT INTO roles (name, display_name, description, is_system) VALUES
  ('super_admin',
   'Super Admin',
   'Assigns users to roles, owns master data, manages institutes.',
   true),

  ('institute_admin',
   'Institute Admin',
   'Creates reporting cycles, defines timelines and section structure.',
   true),

  ('publication_cell',
   'Publication Cell',
   'Manages templates, compiles the final report, owns bilingual output.',
   true),

  ('department_admin',
   'Department Admin',
   'Adds, updates, and deactivates users within their own department.',
   true),

  ('head_of_department',
   'Head of Department',
   'Delegates nodal-officer rights; signs off on department content.',
   true),

  ('department_nodal_officer',
   'Department Nodal Officer',
   'Responsible for their section; submits content for review.',
   true),

  ('contributor',
   'Contributor',
   'Fills forms, writes narrative, uploads tables and annexures.',
   true),

  ('reviewer',
   'Reviewer',
   'Reviews content, adds comments, approves or sends back.',
   true),

  ('finance_officer',
   'Finance Officer',
   'Handles finance data and audited-statement uploads.',
   true),

  ('directors_office',
   'Director''s Office',
   'Final sign-off in the review chain.',
   true);
*/


-- ============================================================
-- TABLE: user_roles
--
-- Assigns one or more roles to a user.
-- Every role assignment for every user lives here —
-- including Contributor, Reviewer, Finance Officer, etc.
--
-- INSERT: When an admin assigns a role to a user.
--         This happens:
--           (a) At account creation — admin sets the initial role
--           (b) Later — admin grants an additional role
--         department_id is set for dept-scoped roles
--         (Contributor, HoD, Nodal Officer, Dept Admin).
--         department_id is NULL for institute-wide roles
--         (Institute Admin, Publication Cell, Super Admin).
--
-- UPDATE: expires_at can be set to time-bound a role.
-- SOFT REVOKE: revoked_at set when a role is removed.
--              Row is never hard-deleted (audit trail).
-- ============================================================
CREATE TABLE user_roles (
    id          UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id     UUID        NOT NULL REFERENCES users (id),
    role_id     UUID        NOT NULL REFERENCES roles (id),
    assigned_by UUID        NOT NULL REFERENCES users (id),
    assigned_at TIMESTAMPTZ NOT NULL DEFAULT now(),
    expires_at  TIMESTAMPTZ,
    revoked_at  TIMESTAMPTZ,
    notes       TEXT
);

CREATE INDEX idx_user_roles_user
    ON user_roles (user_id) WHERE revoked_at IS NULL;

-- A user cannot be assigned the same role twice
CREATE UNIQUE INDEX uq_user_role
    ON user_roles (user_id, role_id)
    WHERE revoked_at IS NULL;

-- ============================================================
-- TABLE: role_delegations
--
-- ONLY used for one specific scenario:
-- A Head of Department (or Institute Admin) temporarily
-- delegates the Department Nodal Officer responsibility
-- to another staff member for a specific reporting year.
--
-- This is NOT for general role assignment — use user_roles for that.
--
-- INSERT: When HoD delegates nodal officer duties.
--         e.g. HoD going on leave delegates to Dr. X
--              for Annual Report 2026.
--
-- UPDATE: revoked_at set when delegation is withdrawn.
--
-- The delegatee gets nodal officer permissions derived from
-- this table (in addition to whatever is in user_roles).
-- ============================================================

CREATE TABLE role_delegations (
    id            UUID        PRIMARY KEY DEFAULT gen_random_uuid(),
    delegator_id  UUID        NOT NULL REFERENCES users (id),   -- HoD
    delegatee_id  UUID        NOT NULL REFERENCES users (id),   -- staff receiving the duty
    role_id       UUID        NOT NULL REFERENCES roles (id),   -- always 'department_nodal_officer'
    department_id UUID        NOT NULL REFERENCES departments (id),
    report_id     UUID        NOT NULL REFERENCES reports (id), -- scoped to one reporting year
    delegated_at  TIMESTAMPTZ NOT NULL DEFAULT now(),
    revoked_at    TIMESTAMPTZ,
    notes         TEXT,
    CONSTRAINT uq_delegation
        UNIQUE (delegatee_id, role_id, department_id, report_id)
);

CREATE INDEX idx_delegations_report
    ON role_delegations (report_id) WHERE revoked_at IS NULL;
CREATE INDEX idx_delegations_delegatee
    ON role_delegations (delegatee_id) WHERE revoked_at IS NULL;
```

---

## When data flows — one complete lifecycle

```
1. Super Admin onboards Dr. Sharma as a Contributor
   → INSERT users             (profile)
   → INSERT user_credentials  (temp password, must_change = true)
   → INSERT user_roles        (role = contributor, dept = Research)
   → INSERT password_reset_tokens (one-time setup link sent to Dr. Sharma)

2. Dr. Sharma clicks the link and sets his password
   → UPDATE user_credentials  (new hash, is_temporary = false, must_change = false)
   → UPDATE password_reset_tokens (used_at = now())
   → INSERT login_audit_logs  (action = password_reset_used)

3. Dr. Sharma logs in
   → UPSERT user_sessions     (new token, ip, user_agent)
   → UPDATE user_credentials  (last_login_at = now(), failed_attempts = 0)
   → INSERT login_audit_logs  (action = login_success)

4. Dr. Sharma types wrong password 3 times
   → UPDATE user_credentials  (failed_attempts = 3, locked_until = now() + 30 min)
   → INSERT login_audit_logs  (action = login_failed) × 3
   → INSERT login_audit_logs  (action = account_locked)

5. HoD goes on leave, delegates nodal officer to Dr. Sharma for Report 2026
   → INSERT role_delegations  (delegator=HoD, delegatee=Sharma, report=2026)

6. Dr. Sharma logs out
   → DELETE user_sessions     (row removed)
   → INSERT login_audit_logs  (action = logout)
```


Q & A

why is it better to store user roles in a separate table rather than saving it along with the user credentials?

Good question. Here are the concrete reasons.

---

## Reason 1 — A user can hold more than one role

If roles were stored in `user_credentials`, you'd need either a text column or an array:

```sql
-- Storing in credentials (wrong approach)
user_credentials
───────────────────────────────────────────
user_id   role
u-001     'contributor'         ← only one role possible

-- Or worse, an array
user_id   roles
u-001     ['contributor', 'reviewer']  ← can't index, can't query cleanly
```

With `user_roles` as a separate table:

```sql
user_roles
───────────────────────────────────────────────────────────
user_id   role_id                  department_id
u-001     contributor              dept-research
u-001     reviewer                 dept-clinical   ← same user, two roles, different depts
```

Dr. Sharma can be a **Contributor in Research** and a **Reviewer in Clinical** simultaneously. You cannot model this in a single column.

---

## Reason 2 — Roles are scoped to departments

A role is not just a label — it carries context: **which department** it applies to.

```sql
-- Can't express this in a credentials column
u-001  contributor  →  Research Department
u-001  reviewer     →  Clinical Department
```

`user_credentials` is about authentication (password, lock state). It has no concept of departments. Mixing department scope into credentials breaks separation of concerns entirely.

---

## Reason 3 — Role assignments have their own lifecycle

Each role assignment has metadata that belongs to it, not to the user or their password:

```sql
user_roles
────────────────────────────────────────────────────────────────────
user_id  role_id      assigned_by  assigned_at   expires_at   revoked_at
u-001    contributor  admin-001    Jan 1 2026     NULL         NULL
u-001    reviewer     admin-001    Mar 1 2026     Dec 31 2026  NULL  ← time-bound
u-001    contributor  admin-001    Jan 1 2025     NULL         Dec 31 2025 ← revoked
```

- Who assigned the role?
- When was it assigned?
- Does it expire?
- Was it revoked and when?

None of this belongs in `user_credentials`. Credentials track **authentication state** — password hash, lock status, last login. Roles track **authorization state** — who gave access to what and when.

---

## Reason 4 — Querying becomes clean and efficient

With a separate table you can answer operational questions with simple indexed queries:

```sql
-- All contributors in Research Department
SELECT u.full_name FROM users u
JOIN user_roles ur ON ur.user_id = u.id
JOIN roles r ON r.id = ur.role_id
WHERE r.name = 'contributor'
  AND ur.department_id = 'dept-research'
  AND ur.revoked_at IS NULL;

-- All roles held by Dr. Sharma
SELECT r.display_name, ur.department_id
FROM user_roles ur
JOIN roles r ON r.id = ur.role_id
WHERE ur.user_id = 'u-001' AND ur.revoked_at IS NULL;
```

If roles were stored as an array in `user_credentials`, both queries would require scanning every row and unpacking arrays — no index can help you.

---

## Reason 5 — Separation of concerns

The three tables each have one clear job:

```
user_credentials  →  Authentication   "Is this password correct? Is the account locked?"
                      Changes when:    password changes, login fails, account locked

user_roles        →  Authorization    "What is this user allowed to do and where?"
                      Changes when:    admin assigns/revokes a role

users             →  Identity         "Who is this person?"
                      Changes when:    name, email, department changes
```

Mixing any two of these together means a change in one reason forces you to touch a table that belongs to another concern — a violation of the Single Responsibility Principle that causes bugs and confusion over time.

---

## The simple test

Ask: _"Can this user have more than one value of this thing?"_

|Thing|Multiple per user?|Separate table needed?|
|---|---|---|
|Password|No — one password|No — column in user_credentials|
|Role|Yes — multiple roles, multiple depts|Yes — user_roles table|
|Email|No — one email|No — column in users|
|Session|No — one active session|No — column in user_sessions|

The moment the answer is **yes**, a column can't model it correctly — you need a table.



