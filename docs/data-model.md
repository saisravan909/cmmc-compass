# Data Model

## Design Notes

Evidence is stored as a separate entity with a many-to-many relationship to control assessments. A single policy document can satisfy multiple controls without being duplicated.

The `controls` table is seed data from `data/CMMC_CONTROLS.json`. It is populated once on first run and not modified by users. Users interact with `control_assessments`, which reference control records.

Multi-tenancy is built into the schema. Organizations optionally belong to a consultancy. All API queries scope to the requesting user's organization or consultancy.

## Tables

### consultancies

Parent account for firms managing multiple contractor clients.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| name | varchar | Firm name |
| domain | varchar | Email domain for auto-provisioning |
| created_at | timestamptz | |

### organizations

A defense contractor company.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| consultancy_id | uuid | FK to consultancies, nullable |
| name | varchar | |
| ein | varchar | Employer Identification Number |
| cmmc_level | int | 1 or 2, set during scoping |
| created_at | timestamptz | |

### scope_profiles

One per organization. Captures the assessment boundary.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK to organizations |
| handles_cui | boolean | Determines Level 1 vs Level 2 |
| handles_fci | boolean | |
| cui_asset_types | text[] | e.g. ["Engineering drawings", "Contracts"] |
| system_boundary | text | Narrative description of the ADE |

### controls

Seed data. Not modified by users.

| Column | Type | Notes |
|---|---|---|
| practice_id | varchar | PK, e.g. "AC.L2-3.1.1" |
| level | int | 1 or 2 |
| domain | varchar | e.g. "Access Control" |
| domain_code | varchar | e.g. "AC" |
| title | varchar | Official practice title |
| plain_english | text | Plain-language summary |
| discussion | text | NIST assessment guidance |
| example_evidence | text[] | Suggested evidence types |
| sprs_point_value | int | Points deducted if not met |

### control_assessments

One row per organization per control. This is where the user's work lives.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK to organizations |
| practice_id | varchar | FK to controls |
| status | enum | met / partially_met / not_met / not_applicable |
| implementation_statement | text | Used to generate the SSP |
| owner_id | uuid | FK to users |
| assessed_at | timestamptz | |

### evidence_files

Files uploaded by the organization.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK to organizations |
| filename | varchar | Original file name |
| storage_key | varchar | Object storage key |
| mime_type | varchar | |
| expires_at | date | Nullable, flagged when approaching |
| uploaded_at | timestamptz | |

### evidence_control_map

Junction table linking files to control assessments.

| Column | Type |
|---|---|
| evidence_id | uuid FK to evidence_files |
| assessment_id | uuid FK to control_assessments |

### poam_items

Auto-generated from not_met or partially_met assessments.

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK to organizations |
| assessment_id | uuid | FK to control_assessments |
| weakness_description | text | What is not implemented |
| remediation_plan | text | How it will be addressed |
| owner_id | uuid | FK to users |
| due_date | date | Target remediation date |
| status | enum | open / in_progress / resolved / accepted_risk |

### users

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key |
| org_id | uuid | FK to organizations |
| email | varchar | Unique |
| name | varchar | |
| role | enum | contractor_admin / contractor_user / consultant_reviewer / consultant_admin |
| created_at | timestamptz | |
