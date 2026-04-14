# Roadmap

## Phase 1 — Core MVP: Track 1 Contractor Platform

**Goal:** A complete, standalone compliance tool for a single defense contractor organization. Every core workflow is functional end-to-end.

### Auth & Organization Setup
- [ ] Signup and email verification
- [ ] Organization creation with name, EIN, and primary contact
- [ ] Invite team members with role assignment
- [ ] Session management and secure logout

### Smart Scoping Engine
- [ ] Multi-step scoping questionnaire (company size, contract type, CUI handling)
- [ ] Automatic CMMC Level 1 vs Level 2 determination
- [ ] Asset categorization flow (CUI Assets, Security Protection Assets, Out-of-Scope)
- [ ] System boundary narrative input
- [ ] Personalized readiness roadmap generation on completion

### Domain-by-Domain Assessment
- [ ] All 14 domains navigable from a single assessment hub
- [ ] Each control displays: practice ID, plain-English title, NIST discussion, example evidence
- [ ] Status toggle: Met / Partially Met / Not Met / Not Applicable
- [ ] Implementation statement rich text input (feeds SSP)
- [ ] Responsible owner assignment per control
- [ ] Domain completion percentage tracking

### Live SPRS Dashboard
- [ ] Real-time SPRS score gauge (0–110)
- [ ] Score history chart (progress over time)
- [ ] Domain completion rings (14 domains)
- [ ] Golden Path widget: top 3 controls by points available
- [ ] At-risk controls alert panel (overdue POA&Ms, expiring evidence)

### Evidence Locker
- [ ] File upload (PDF, PNG, DOCX, XLSX, TXT, log files)
- [ ] Multi-control tagging — one file to many controls
- [ ] Expiry date setting with 30-day warning flags
- [ ] Evidence status: current / expiring / expired
- [ ] Evidence search and filter by control, domain, type
- [ ] Delete and re-upload flow

### POA&M Tracker
- [ ] Auto-generation from Not Met and Partially Met controls
- [ ] Weakness description and remediation plan fields
- [ ] Owner assignment and due date setting
- [ ] Status transitions: Open → In Progress → Resolved / Accepted Risk
- [ ] Overdue item highlighting and notification triggers

---

## Phase 2 — Artifact Generation

**Goal:** Turn completed assessment data into professionally formatted compliance documents.

### SSP Auto-Assembly
- [ ] Background assembly as implementation statements are entered
- [ ] SSP preview mode within the application
- [ ] Section completeness indicator (which controls still need statements)

### Document Export
- [ ] SSP PDF export — DoD/NARA template compliant
- [ ] SSP Word export — editable .docx
- [ ] POA&M PDF export — OMB format compliant
- [ ] POA&M Excel export
- [ ] Evidence bundle ZIP export (structured by domain)
- [ ] Full assessment package export (SSP + POA&M + Evidence)

### Assessor View
- [ ] Toggle to simulate C3PAO assessment view
- [ ] Per-control view: Practice ID + Statement + Evidence + Owner + Status
- [ ] Print-optimized layout

---

## Phase 3 — Track 3: Consultancy / MSP Layer

**Goal:** A multi-tenant layer that lets consultancies manage compliance for multiple client organizations.

### Multi-Tenant Architecture
- [ ] Consultancy account type with child organization management
- [ ] Client invitation and onboarding flow
- [ ] Consultancy-scoped data isolation

### Client Health Map
- [ ] Aggregate dashboard: all clients, SPRS scores, assessment status
- [ ] At-risk client alerts (overdue POA&Ms, stale assessments, expiring evidence)
- [ ] Sort and filter by score, domain, assessment date, risk level

### Policy Template Library
- [ ] Create and version reusable policy document templates
- [ ] Push template to one or all clients simultaneously
- [ ] Client receives suggestion notification and can accept or customize

### RBAC Enforcement
- [ ] Consultant Reviewer role: view and comment only, no edits
- [ ] Consultant Admin role: full access across all client orgs
- [ ] Contractor Admin can grant/revoke consultant access
- [ ] Audit log of all consultant actions within client workspace

### Review Workflow
- [ ] Inline comments on control assessments and implementation statements
- [ ] Threaded replies between consultant and contractor
- [ ] Comment resolution and status tracking
- [ ] Email notification on new comments and replies

### Bulk Actions
- [ ] Select multiple clients and push a policy template
- [ ] Send a compliance task to all clients in a specific domain
- [ ] Bulk POA&M deadline extension with reason tracking

---

## Future Considerations (Post-Phase 3)

- **Track 2 — Assessor / C3PAO Tooling** — Portfolio management for certified assessors, interview checklists, finding documentation, and formal assessment report generation
- **CMMC Level 3** — Higher-assurance practices aligned to NIST SP 800-172
- **Multi-Framework Support** — FedRAMP, DFARS, NIST CSF mapping alongside CMMC
- **AI-Assisted Gap Analysis** — Suggest implementation approaches based on organization profile
- **Continuous Monitoring** — Automated evidence collection integrations (cloud providers, endpoint tools)
