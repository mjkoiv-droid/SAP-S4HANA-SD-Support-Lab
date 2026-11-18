
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
| R02 | Sales orders, picking, shipment and billing | M2, M3 | Executed | Two training-sandbox O2C chains through balanced FI: 1055→80000784→4900001488→90000303→9400000057 and 1056→80000785→4900001489→90000304→9400000058 (EV-017–EV-035); billing-block control failed/open for M3; inventory balance/movement type unverified |
| R03 | IDocs, interfaces, logs and output | M4 | In Progress | Existing `DELFOR` status `56` error diagnosis, `INVOIC` configuration inspection and completed order `374` output (EV-053–EV-070); successful IDoc reprocessing and target FI invoice not verified |
| R04 | Incidents and service requests | M5 | In Progress | Two *controlled sandbox* cases M1-TRIAGE-001/002 (EV-009–EV-016); 6-case queue and SRs pending |
| R05 | Root cause analysis and corrective actions | M5 | In Progress | Two known root causes + corrections + retests (EV-010–EV-016); formal 3× RCA still pending |
| R06 | Business coordination: Sales, Logistics, Finance | M6 | Not Started | TBD |
| R07 | Enhancements, configuration and impact assessment | M3, M6 | In Progress | Read-only M3 pricing/shipping inspection EV-041–EV-044, picking exception EV-045–EV-048, billing block 04 negative tests EV-036–EV-039 / EV-051–EV-052; CHG-M3-001 proposed and impact matrix prepared; CBC configuration unverified, no implementation |
| R08 | Unit, integration and UAT testing | M6, M7 | Not Started | TBD |
| R09 | Release and post-release validation | M7 | Not Started | TBD |
| R10 | Functional, configuration and test documentation | M3, M6, M7 | In Progress | Filled M3 CFG-SD-001, CHG-M3-001 proposal, incident investigations and impact/regression matrix; M6/M7 not started |
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
- Verification status

## Completion Criteria

The lab is complete when all 15 requirements have been assessed and their execution status accurately recorded. **M1 demonstrates partial monitoring/incident/RCA coverage; M2 demonstrates the R02 O2C execution scope with two full FI chains; M4 has verified diagnostic, configuration and output evidence with simulated-only recovery. The unresolved M2 billing-block control is an explicit M3 follow-up, not a successful control test.**

Activities that cannot be performed in the training environment must be clearly identified as simulated or blocked.
