# Roadmap

## Phase 1: Contractor Platform

The goal of Phase 1 is a working end-to-end workflow for a single contractor organization: scope the assessment, assess all controls, track evidence, manage the POA&M, and see the SPRS score update as work progresses.

### Auth and Setup
- [ ] Signup, email verification, login
- [ ] Organization creation with name and EIN
- [ ] Team member invitations with role assignment

### Scoping
- [ ] Multi-step questionnaire to determine Level 1 or Level 2
- [ ] Asset categorization: CUI Assets, Security Protection Assets, Out-of-Scope
- [ ] System boundary input
- [ ] Readiness roadmap generated on completion

### Control Assessment
- [ ] Assessment hub showing all 14 domains with completion status
- [ ] Per-control view with plain-English description, NIST guidance, and example evidence
- [ ] Status options: Met, Partially Met, Not Met, Not Applicable
- [ ] Implementation statement field (feeds SSP)
- [ ] Owner assignment per control

### Dashboard
- [ ] Live SPRS score
- [ ] Score breakdown by domain
- [ ] Top controls by point recovery (highest impact actions)
- [ ] Overdue POA&M items and expiring evidence alerts

### Evidence
- [ ] File upload (PDF, PNG, DOCX, XLSX, logs)
- [ ] Tag files to one or many controls
- [ ] Expiry date tracking with warning flags at 30 days
- [ ] Search and filter by control, domain, or file type

### POA&M
- [ ] Auto-creation from Not Met and Partially Met controls
- [ ] Weakness description and remediation plan fields
- [ ] Owner and due date assignment
- [ ] Status: Open, In Progress, Resolved, Accepted Risk

---

## Phase 2: Document Export

Phase 2 makes the assessment output portable and suitable for a formal assessment.

- [ ] SSP PDF export in DoD and NARA template format
- [ ] SSP Word export as editable docx
- [ ] POA&M PDF in OMB format
- [ ] Evidence bundle as a structured ZIP
- [ ] Full assessment package export (SSP + POA&M + evidence)
- [ ] Assessor view toggle showing control, statement, evidence, and owner

---

## Phase 3: Consultancy Layer

Phase 3 adds multi-tenant support for consultancies and MSPs managing multiple client organizations.

- [ ] Consultancy account type with client organization management
- [ ] Client onboarding and invitation flow
- [ ] Aggregate dashboard: all clients with SPRS scores and status
- [ ] At-risk alerts for overdue POA&Ms and stale assessments
- [ ] Policy template library: create, version, and push to clients
- [ ] Four-role RBAC enforced throughout
- [ ] Inline comments on assessments with threaded replies
- [ ] Bulk actions: push a template or task to multiple clients at once
- [ ] Audit log of consultant actions within client workspaces

---

## Future Work

- Track 2: C3PAO assessor tooling
- CMMC Level 3 controls (NIST SP 800-172)
- Support for additional frameworks: FedRAMP, DFARS, NIST CSF
- Automated evidence collection from cloud providers and endpoint tools
