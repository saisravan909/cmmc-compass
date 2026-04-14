# Data Model

## Design Principles

1. **Evidence is a first-class entity** — not a file attachment. It has its own table, its own lifecycle, and a many-to-many relationship to controls.
2. **Multi-tenancy is structural, not bolted on** — every organization optionally belongs to a consultancy. All queries are scoped at the ORM level.
3. **Controls are seed data, not user data** — the 127 CMMC practice definitions live in `data/CMMC_CONTROLS.json` and are seeded once into the `controls` table. Users create `control_assessments` referencing these.
4. **The SSP assembles itself** — `implementation_statement` on each `control_assessment` is the raw material. The SSP builder queries all assessed controls and renders the document on demand.

## Entity Reference

### `consultancies`
Parent account for consultancy firms managing multiple contractor clients.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| name | varchar | Firm name |
| domain | varchar | Email domain for auto-provisioning |
| created_at | timestamptz | |

### `organizations`
A defense contractor company. Belongs to a consultancy (optional).

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| consultancy_id | uuid | FK → consultancies (nullable) |
| name | varchar | Company name |
| ein | varchar | Employer Identification Number |
| cmmc_level | int | 1 or 2, set during scoping |
| created_at | timestamptz | |

### `scope_profiles`
One per organization. Captures the assessment boundary.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK → organizations |
| handles_cui | boolean | Drives Level 1 vs Level 2 selection |
| handles_fci | boolean | |
| cui_asset_types | text[] | e.g. ["Engineering drawings", "Contracts"] |
| system_boundary | text | Narrative description of the ADE |

### `controls` (seed data)
Static table seeded from `CMMC_CONTROLS.json`. Never modified by users.

| Column | Type | Notes |
|---|---|---|
| practice_id | varchar | PK e.g. "AC.L2-3.1.1" |
| level | int | 1 or 2 |
| domain | varchar | e.g. "Access Control" |
| domain_code | varchar | e.g. "AC" |
| title | varchar | Official CMMC practice title |
| plain_english | text | Plain-language explanation |
| discussion | text | NIST assessment guidance |
| example_evidence | text[] | Suggested evidence types |
| sprs_point_value | int | Points deducted if not met (1, 3, or 5) |

### `control_assessments`
One per (organization × control). Tracks implementation status.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK → organizations |
| practice_id | varchar | FK → controls |
| status | enum | met / partially_met / not_met / not_applicable |
| implementation_statement | text | Feeds the SSP |
| owner_id | uuid | FK → users |
| assessed_at | timestamptz | Last update |

### `evidence_files`
Independently stored files, tagged to one or many control assessments.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK → organizations |
| filename | varchar | Original file name |
| storage_key | varchar | Object storage key |
| mime_type | varchar | |
| expires_at | date | Nullable; flagged when approaching |
| uploaded_at | timestamptz | |

### `evidence_control_map` (junction)
Many-to-many between evidence files and control assessments.

| Column | Type |
|---|---|
| evidence_id | uuid FK → evidence_files |
| assessment_id | uuid FK → control_assessments |

### `poam_items`
Auto-generated from not_met or partially_met control assessments.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK → organizations |
| assessment_id | uuid | FK → control_assessments |
| weakness_description | text | What is missing |
| remediation_plan | text | How it will be fixed |
| owner_id | uuid | FK → users |
| due_date | date | Target remediation date |
| status | enum | open / in_progress / resolved / accepted_risk |

### `users`

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK → organizations |
| email | varchar | Unique |
| name | varchar | |
| role | enum | contractor_admin / contractor_user / consultant_reviewer / consultant_admin |
| created_at | timestamptz | |
