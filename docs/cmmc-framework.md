# CMMC Framework Reference

## What is CMMC?

The Cybersecurity Maturity Model Certification (CMMC) is a Department of Defense (DoD) framework that ensures defense contractors and their subcontractors protect Federal Contract Information (FCI) and Controlled Unclassified Information (CUI) at levels appropriate to the risk and sensitivity of the information.

CMMC 2.0 (the current version) streamlined the original 5-level model into 3 levels:

| Level | Name | Basis | Assessment |
|---|---|---|---|
| 1 | Foundational | 17 practices (FAR 52.204-21) | Annual self-assessment |
| 2 | Advanced | 110 practices (NIST SP 800-171 Rev 2) | Triennial third-party (C3PAO) |
| 3 | Expert | 110+ practices (NIST SP 800-172) | Government-led assessment |

CMMC Compass supports **Level 1** and **Level 2**.

---

## The 14 Domains

CMMC Level 2 organizes 110 practices across 14 domains, each mapped from NIST SP 800-171:

| # | Domain | Code | L1 | L2 |
|---|---|---|---|---|
| 1 | Access Control | AC | 2 | 22 |
| 2 | Awareness & Training | AT | 0 | 3 |
| 3 | Audit & Accountability | AU | 0 | 9 |
| 4 | Configuration Management | CM | 0 | 9 |
| 5 | Identification & Authentication | IA | 2 | 11 |
| 6 | Incident Response | IR | 0 | 3 |
| 7 | Maintenance | MA | 0 | 6 |
| 8 | Media Protection | MP | 1 | 8 |
| 9 | Personnel Security | PS | 0 | 2 |
| 10 | Physical Protection | PE | 4 | 6 |
| 11 | Risk Assessment | RA | 0 | 3 |
| 12 | Security Assessment | CA | 0 | 4 |
| 13 | System & Communications Protection | SC | 2 | 14 |
| 14 | System & Information Integrity | SI | 4 | 7 |

---

## The SPRS Score

The Supplier Performance Risk System (SPRS) score is how the DoD quantifies a contractor's cybersecurity posture. It is submitted to the SPRS database and visible to contracting officers.

- **Maximum score:** 110 (all practices implemented)
- **Starting point:** 110, with deductions for each unimplemented control
- **Deduction values:** Each practice is worth 1, 3, or 5 points depending on severity

A score below 110 is acceptable if a POA&M is in place. A score of 110 with a clean SSP means full implementation.

### Score Formula

```
SPRS Score = 110 − Σ(point_value for each NOT MET or PARTIALLY MET practice)
```

---

## Key Compliance Artifacts

### System Security Plan (SSP)
The SSP documents how each of the 110 NIST SP 800-171 requirements is implemented within your organization. It is the primary document a C3PAO assessor reviews. A good SSP:
- Has an implementation statement for every applicable control
- Describes responsible roles and owners
- References the evidence that supports each claim
- Defines the system boundary and what is in scope

### Plan of Action & Milestones (POA&M)
The POA&M documents controls that are not yet fully implemented, with:
- A description of the gap (weakness)
- A remediation plan
- A responsible owner
- A target completion date

The DoD allows contractors to submit a score with a POA&M, signaling intent to remediate. Critical controls may not be deferred.

### Evidence Package
For each control marked as Met, there must be supporting evidence. Common types include:
- Policy documents (Access Control Policy, Incident Response Plan)
- Configuration screenshots
- System logs and audit trails
- Training completion records
- Vendor contracts and agreements
- Network diagrams and system inventories

---

## Assessment Process (Level 2)

1. **Scoping** — Define the Assessment Data Environment (ADE): systems, personnel, facilities, and data flows that touch CUI
2. **Self-Assessment / Gap Analysis** — Evaluate current state against all 110 practices
3. **SSP Development** — Document implementation for every in-scope control
4. **POA&M Development** — Document all gaps with remediation timelines
5. **C3PAO Assessment** — A certified third-party assessor reviews documentation, conducts interviews, and tests controls
6. **Score Submission** — Final SPRS score and assessment results entered into the CMMC eMASS system
7. **Certification** — Valid for 3 years; annual affirmations required

---

## Reference Documents

- [CMMC 2.0 Model Overview](https://www.acq.osd.mil/cmmc/)
- [NIST SP 800-171 Rev 2](https://csrc.nist.gov/publications/detail/sp/800-171/rev-2/final)
- [NIST SP 800-171A](https://csrc.nist.gov/publications/detail/sp/800-171a/final) — Assessment procedures
- [NIST SP 800-172](https://csrc.nist.gov/publications/detail/sp/800-172/final) — Enhanced requirements (Level 3)
- [DFARS 252.204-7012](https://www.acq.osd.mil/dpap/dars/dfars/html/current/252204.htm) — Safeguarding CUI clause
