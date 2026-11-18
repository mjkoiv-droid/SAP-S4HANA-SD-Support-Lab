
# SAP SD Lab — Requirement Coverage Matrix

**Project:** SAP S/4HANA SD Application Support Lab  
**Status:** All R01–R15 assessed; operational coverage remains partial (classification is not customer acceptance)

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
| R04 | Incidents and service requests | M5 | In Progress | Six evidence-qualified investigation records; 3 resolved training defects, 1 IDoc diagnosis only, 1 positive invoice-output baseline, 1 open CBC denial. Proposed SR-SD-001/002 not submitted. EV-014–EV-016, EV-045–EV-048, EV-021–EV-026, EV-053, EV-071–EV-082 |
| R05 | Root cause analysis and corrective actions | M5 | In Progress | Three completed, evidence-limited RCA documents: manual PPR0 override, partial picking/VLMOVE 030, missing customer company-code data. All three have case-level corrections/retests. Wider prevention, IDoc/CBC root cause and actual reopening remain unverified. |
| R06 | Business coordination: Sales, Logistics, Finance | M6 | Simulated | Fictional workshop / stakeholder viewpoints in M6 CHG-SD-001; no actual coordination or sign-off |
| R07 | Enhancements, configuration and impact assessment | M3, M6 | In Progress | CHG-M3-001 and CHG-SD-001 design/impact prepared; four relevant blocking levels examined pre-change (EV-027–EV-039, EV-051–EV-052, EV-083–EV-089). JV2 CBC diagnosis blocked; EV-082 is T41 only; **no change implemented** |
| R08 | Unit, integration and UAT testing | M6, M7 | In Progress | Seven heterogeneous pre-change M6 test cases (two new TC-SD-004/005, EV-083–EV-089; other prior evidence reused). M7 REL-SD-001 documents a **simulated UAT-readiness assessment**; TC-SD-008/009 and actual UAT, fix/retest and sign-off **not executed** |
| R09 | Release and post-release validation | M7 | In Progress | **Executed read-only T41/400 SE09/STMS inspection** (EV-090–EV-093) plus [simulated REL-SD-001 NO-GO/release packet](../M7-UAT-Release-and-Hypercare/Release-Readiness-REL-SD-001.md). No approved change, transport release/import, deployment, real UAT or post-release smoke testing |
| R10 | Functional, configuration and test documentation | M3, M6, M7 | In Progress | M3 analysis/proposal; M6 proposed functional specification, simulated workshop, traceability, impact and test/defect records; M7 release/UAT/smoke/rollback/hypercare **documented** in REL-SD-001; no approved or implemented change |
| R11 | User, role and authorization support | M5, M8 | In Progress | JV2 CBC Unauthorized reproduced (EV-079–EV-080); read-only JV2 IAM role/catalog and restriction assessment completed for four business roles (EV-094–EV-103; [M8-SD-001](../M8-Authorization-Access-and-Audit/M8-Access-Authorization-and-SoD-Review.md)). No trace, root-cause confirmation, role remediation, approved access request or retest |
| R12 | Access review, SoD and audit | M8 | In Progress | [M8-SD-001](../M8-Authorization-Access-and-Audit/M8-Access-Authorization-and-SoD-Review.md): training-scope four-persona review, two bounded potential SoD analyses and audit findings packet, supported by role assignment EV-001 and IAM screenshots EV-094–EV-103. Not a complete user-population certification, proven SoD violation, approved mitigation or formally closed audit |
| R13 | Key-user training | M9 | Simulated | [M9-TRN-001](../M9-Global-Support-and-Training/M9-Key-User-Training-Guide.md): screenshot-based O2C key-user walkthrough, safe actions, FAQ and unanswered trainee-assessment prompts; uses existing EV-014–EV-026, EV-045–EV-048, EV-073. No class delivered, recording, trainee attendance or sign-off |
| R14 | Global support environment | M9 | Simulated | [M9-SD-001](../M9-Global-Support-and-Training/M9-Global-Handover-and-Bilingual-Communication.md): fictional APAC/EMEA owner/escalation and handover based on historical INC-SD-003 EV-017–EV-026; [M9-CAP-001 KT/KPI plan](../M9-Global-Support-and-Training/M9-Capstone-Knowledge-Transfer-and-Improvement.md). No actual multinational support case, ownership acceptance, KPI sample or support transition |
| R15 | Japanese and English support | M9 | Simulated | [M9-SD-001](../M9-Global-Support-and-Training/M9-Global-Handover-and-Bilingual-Communication.md): actual drafted Japanese user communication and English technical escalation; recipient/reviewer, transmission and live bilingual support are unverified |

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

**All 15 requirements have a recorded, evidence-qualified classification; this satisfies documentation-level coverage review, not operational execution of all requirements.** **M1 demonstrates partial monitoring/incident/RCA coverage; M2 demonstrates the R02 O2C execution scope with two full FI chains; M4 has verified diagnostic, configuration and output evidence with simulated-only recovery. The unresolved M2 billing-block control is an explicit M3 follow-up, not a successful control test.**

Activities that cannot be performed in the training environment must be clearly identified as simulated or blocked.
