
# SAP SD Lab — Requirement Coverage Matrix

**Project:** SAP S/4HANA SD Application Support Lab  
**Status:** In progress

## Purpose

Track progress against the 15 SAP SD application support job requirements and link each requirement to verifiable lab evidence.

## Status Definitions

- **Not Started:** No relevant exercise completed
- **In Progress:** Partial evidence exists; the full job requirement is not yet met
- **Executed:** The *full requirement* was demonstrated in SAP with evidence
- **Simulated:** Documented exercise without actual SAP execution
- **Blocked:** Cannot execute due to system or authorization limitations

## Requirement Coverage

| ID | Job Requirement | Module | Status | Evidence |
|---|---|---|---|---|
| R01 | Daily support and monitoring | M1, M5 | In Progress | M1 monitoring baseline and runbook: EV-003–EV-007; no repeated daily production monitoring |
| R02 | Sales orders, picking, shipment and billing | M2, M3 | In Progress | Order 1055 → delivery 80000784 verified (EV-009–EV-013); no picking, PGI, billing or FI chain yet |
| R03 | IDocs, interfaces, logs and output | M4 | Not Started | TBD |
| R04 | Incidents and service requests | M5 | In Progress | Two *controlled sandbox* cases M1-TRIAGE-001/002 (EV-009–EV-016); 6-case queue and SRs pending |
| R05 | Root cause analysis and corrective actions | M5 | In Progress | Two known root causes + corrections + retests (EV-010–EV-016); formal 3× RCA still pending |
| R06 | Business coordination: Sales, Logistics, Finance | M6 | Not Started | TBD |
| R07 | Enhancements, configuration and impact assessment | M3, M6 | Not Started | TBD |
| R08 | Unit, integration and UAT testing | M6, M7 | Not Started | TBD |
| R09 | Release and post-release validation | M7 | Not Started | TBD |
| R10 | Functional, configuration and test documentation | M3, M6, M7 | Not Started | TBD |
| R11 | User, role and authorization support | M8 | Not Started | TBD |
| R12 | Access review, SoD and audit | M8 | Not Started | TBD |
| R13 | Key-user training | M9 | Not Started | TBD |
| R14 | Global support environment | M9 | Not Started | TBD |
| R15 | Japanese and English support | M9 | Not Started | TBD |

## Evidence Tracking

Each completed exercise should include:

- Evidence ID (EV-001, EV-002, etc.)
- Related module and requirement
- SAP transaction or Fiori application
- System/client information
- Description of the activity
- Expected and actual results
- Screenshot or document reference
- Execution date
- Verification status

## Completion Criteria

The lab is complete when all 15 requirements have been assessed and their execution status accurately recorded. **M1-only evidence gives partial coverage of R01/R02/R04/R05; it does not complete these requirements.**

Activities that cannot be performed in the training environment must be clearly identified as simulated or blocked.
