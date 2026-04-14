# CMMC Framework Reference

## What is CMMC?

CMMC (Cybersecurity Maturity Model Certification) is a DoD framework that requires defense contractors to demonstrate cybersecurity compliance in order to handle Federal Contract Information (FCI) or Controlled Unclassified Information (CUI).

CMMC 2.0 has three levels:

| Level | Name | Controls | Assessment type |
|---|---|---|---|
| 1 | Foundational | 17 practices | Annual self-assessment |
| 2 | Advanced | 110 practices (NIST SP 800-171) | Third-party (C3PAO) every 3 years |
| 3 | Expert | 110+ practices (NIST SP 800-172) | Government-led |

CMMC Compass covers Level 1 and Level 2.

---

## The 14 Domains

| # | Domain | Code | L1 | L2 |
|---|---|---|---|---|
| 1 | Access Control | AC | 2 | 22 |
| 2 | Awareness and Training | AT | 0 | 3 |
| 3 | Audit and Accountability | AU | 0 | 9 |
| 4 | Configuration Management | CM | 0 | 9 |
| 5 | Identification and Authentication | IA | 2 | 11 |
| 6 | Incident Response | IR | 0 | 3 |
| 7 | Maintenance | MA | 0 | 6 |
| 8 | Media Protection | MP | 1 | 8 |
| 9 | Personnel Security | PS | 0 | 2 |
| 10 | Physical Protection | PE | 4 | 6 |
| 11 | Risk Assessment | RA | 0 | 3 |
| 12 | Security Assessment | CA | 0 | 4 |
| 13 | System and Communications Protection | SC | 2 | 14 |
| 14 | System and Information Integrity | SI | 4 | 7 |

---

## The SPRS Score

SPRS (Supplier Performance Risk System) is the score contractors submit to the DoD database. It represents how fully they have implemented the 110 NIST SP 800-171 controls.

The score starts at 110 and deducts points for each control that is not implemented. Each control is worth 1, 3, or 5 points depending on severity. A perfect score is 110.

```
SPRS Score = 110 - sum of point values for all not-implemented controls
```

Contractors can submit a score below 110 if a POA&M is in place for the gaps. Some critical controls cannot be deferred.

---

## Key Documents

### System Security Plan (SSP)

The SSP documents how each NIST SP 800-171 requirement is implemented. It is the main artifact a C3PAO assessor reviews. A complete SSP has an implementation statement for every in-scope control, identifies responsible personnel, references supporting evidence, and defines the system boundary.

### Plan of Action and Milestones (POA&M)

The POA&M lists controls that are not yet implemented, with a description of the gap, a remediation plan, a responsible owner, and a target date. It is submitted alongside the SSP score.

### Evidence

For each control marked as Met, there must be supporting evidence. Common types include policies (Access Control Policy, Incident Response Plan), configuration screenshots, audit logs, training completion records, and network diagrams.

---

## Assessment Process (Level 2)

1. Define the assessment boundary (which systems, people, and locations touch CUI)
2. Assess current state against all 110 controls
3. Write implementation statements for the SSP
4. Document gaps in the POA&M with remediation timelines
5. A C3PAO assessor reviews documentation, interviews personnel, and tests controls
6. Final score and results go into the CMMC eMASS system
7. Certification is valid for 3 years with annual affirmations

---

## Reference Documents

- [CMMC 2.0 Model](https://www.acq.osd.mil/cmmc/)
- [NIST SP 800-171 Rev 2](https://csrc.nist.gov/publications/detail/sp/800-171/rev-2/final)
- [NIST SP 800-171A](https://csrc.nist.gov/publications/detail/sp/800-171a/final) (assessment procedures)
- [NIST SP 800-172](https://csrc.nist.gov/publications/detail/sp/800-172/final) (Level 3)
- [DFARS 252.204-7012](https://www.acq.osd.mil/dpap/dars/dfars/html/current/252204.htm)
