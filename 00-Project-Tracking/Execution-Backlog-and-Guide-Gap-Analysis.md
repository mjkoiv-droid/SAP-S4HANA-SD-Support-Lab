# Execution Backlog and Word-Guide Gap Analysis

**Source of requirements:** `SAP_SD_Complete_2_Week_Lab_and_Interview_Guide.docx` (original Word guide, sections 1, 2, 4–9).  
**Working structure:** repository contents as received.  
**Project state:** No SAP exercises have been performed or verified at the start of this execution phase.  
**Scheduling:** No daily, weekly, or duration-based schedule is imposed. Work proceeds as soon as individual results are verified.

## Evidence and completion rules

- A prepared template or fictional example is **documentation**, not evidence of SAP execution.
- Mark an SAP task **Executed** only after the actual step is performed in an authorized SAP training system and the result is verified and logged (transaction/Fiori app, client, timestamp, document IDs where applicable, expected versus actual, anonymized screenshot or system output).
- **Simulated** = worked through on paper, explicitly without claiming SAP execution. **Blocked** = confirmed infeasible because of access, data, or tenant constraints. **Not Started** = no outcome yet.
- A read-only system inspection may be an executed *inspection*, but does not imply that the related corrective action, configuration change, or end-to-end transaction has been executed.
- The 15 requirement rows stay Not Started until supported outcomes are assessed; later mark each row by the actual level of coverage and link evidence. Do not call a partly completed module complete.
- Preserve all existing templates. Copy/fill them for concrete case deliverables; do not overwrite examples with fabricated client results.
- Do not run destructive activities, modify shared configuration, reprocess shared IDocs, transport changes or change other users' roles without explicit permission.
- Do not publish the repository until all exercises, classification, anonymization, and final portfolio validation are finished. Repository privacy cannot be inferred from the local ZIP.

## Gate A — SAP access audit (required before M1)

Use [M1 Access Audit and Baseline](../M1-Landscape-and-Monitoring/Access-Audit-and-Baseline.md).

- [ ] **A01** System → Status: system, release, client, own user context, permitted scope and sandbox access restrictions.
- [ ] **A02** Read/display feasibility for VA01, VA03, VL03N, VF03 and a complete O2C chain; distinguish display rights from transaction-creation rights.
- [ ] **A03** Read-only SPRO/VOV8/V/08 and confirm whether dedicated authorized configuration changes are possible.
- [ ] **A04** WE02/WE05, WE19, BD87: establish IDoc sample availability and safe reprocessing boundary.
- [ ] **A05** SLG1, output monitoring and logs: establish whether representative messages can be inspected.
- [ ] **A06** SU53, SU01/PFCG (if permitted): confirm own-user troubleshooting and read-only role visibility.
- [ ] **A07** SE09/SE10/STMS: establish transport read-access and confirm that unauthorized imports are prohibited.
- [ ] **A08** Test data isolation: verify training-only customer/material/user data, shared-client limits, reset policy, and prohibition on modifying other learners' data.

**Decision:** use permitted training exercises; classify truly inaccessible operations as simulated or blocked. Do not infer permissions from a transaction being visible on a menu.

## M1 — Environment, monitoring and support operations (R01)

Existing: M1 README only. Missing: execution-specific inventory, monitoring, runbook and triage records. New M1 working files address this documentary gap without claiming results.

- [ ] **M1.01** Record release/client, user permissions and access matrix (Gate A).
- [ ] **M1.02** Inspect org and sample data: company code, sales org, distribution channel, division, plant, shipping point, billing setup, customer/material, stock and approved scenario.
- [ ] **M1.03** Monitoring sweep: incomplete sales docs; blocked orders, deliveries or invoices; IDoc statuses; SLG1; interface/output queues; record accessible views and explicit access failures.
- [ ] **M1.04** Define severity, impact, urgency, response/SLA *illustrations*, escalation owners, ticket states, evidence standards and daily handover format for the fictional company.
- [ ] **M1.05** Create **two triage tickets**, based on observed conditions if available; otherwise label fictional scenarios as simulated. Distinguish incident, service request and problem.
- [ ] **M1.06** Baseline KPIs: incident volume and age, failed interfaces, billing backlog, mean resolution time. Label every unmeasurable value as N/A or illustrative, never observed.

Deliverables: **access audit**, **support runbook**, **baseline monitoring sheet**, **2 triage tickets**, anonymized EV references. Files: `M1/Access-Audit-and-Baseline.md`, `M1/Support-Runbook-and-Triage.md` (actual folder is `M1-Landscape-and-Monitoring`).

## M2 — Two complete order-to-cash chains (R02)

Existing: `M2-Order-to-Cash/O2C-Process-Trace-Template.md`.

- [ ] **M2.01** Inspect customer/material, sales area, partner functions, shipping conditions, plant, stock and missing-master-data effects.
- [ ] **M2.02** Create standard sales order (VA01/equivalent); inspect pricing, tax, schedule lines, ATP/availability, credit/status and document flow; change an authorized field and evaluate downstream impact.
- [ ] **M2.03** Create outbound delivery (VL01N/equivalent); pick, post goods issue, verify stock movement and delivery status.
- [ ] **M2.04** Create invoice (VF01/equivalent); inspect billing and FI accounting document, ordered/delivered/billed quantity reconciliation.
- [ ] **M2.05** Run a **second distinct** tenant-supported variation (partial delivery, billing block, return or export) through the available O2C process; identify exceptions.
- [ ] **M2.06** Prepare Sales → Logistics → Finance swimlane with real document IDs, control checks and exception points.

Deliverables: **2 fully evidenced O2C traces**, annotated document-flow/swimlane, process-control checklist, screenshots; reuse process-trace template per case.

## M3 — Configuration and logistics exceptions (R02, R07, R10)

Existing: `M3-Configuration-and-Logistics/Configuration-Analysis-Template.md`.

- [ ] **M3.01** Inspect document type, item-category and schedule-line determination, copy control, shipping-point determination, delivery and billing settings.
- [ ] **M3.02** Inspect pricing procedure/condition technique, condition records and SD–FI account determination; identify authorized safe reproduction test.
- [ ] **M3.03** Baseline/propose one change (e.g. pricing/billing block) with dependencies, authorization, approval, expected delta, impact and rollback.
- [ ] **M3.04** Implement only if authorized in a dedicated training client; otherwise preserve read-only inspection and label proposed settings simulated.
- [ ] **M3.05** Reproduce and diagnose **missing/wrong price** and **delivery/picking block** with negative, positive and regression tests, if supported.
- [ ] **M3.06** Assess Sales, Logistics, FI, outputs, interfaces, reporting, roles, risk and regression coverage.

Deliverables: filled configuration workbook, controlled change proposal, impact matrix, **2 exception investigation records**, before/after test evidence.

## M4 — IDoc, interfaces, logs and output (R03)

Existing: `M4-IDocs-Interfaces-and-Output/IDoc-Diagnostic-Template.md`.

- [ ] **M4.01** WE02/WE05: examine IDoc control/data/status and functional versus technical errors.
- [ ] **M4.02** Inspect approved WE20 partner profile/WE21 port; WE19/BD87 only when separately authorized.
- [ ] **M4.03** Diagnose sample failed sales/delivery IDoc: sender, receiver, message/basic type, status, error, root cause and corrective proposal.
- [ ] **M4.04** SLG1 application logs plus invoice/output determination and processing trace where available.
- [ ] **M4.05** Write interface monitoring/alert, ownership, approval, deduplication and reconciliation procedure.
- [ ] **M4.06** Validate negative → corrected/reprocessed → positive scenario **only** in approved isolated test data; otherwise explicitly simulate with no fictitious SAP result.

Deliverables: IDoc diagnosis, message/interface trace, output checklist, recovery runbook, negative/positive evidence.

## M5 — Incident, problem and RCA (R01, R04, R05)

Existing: `M5-Incident-and-Root-Cause-Management/Incident-Template.md`, `RCA-Template.md`.

- [ ] **M5.01** Investigate **INC-SD-001** incorrect pricing, including procedure/condition cause and cross-customer regression.
- [ ] **M5.02** Investigate **INC-SD-002** picking/delivery quantity mismatch with schedule, stock, status and control-safe reconciliation.
- [ ] **M5.03** Investigate **INC-SD-003** billing creation failure: block, incompletion, copy control, SD–FI posting.
- [ ] **M5.04** Investigate **INC-SD-004** failed IDoc; reprocessing and duplicate avoidance if permitted.
- [ ] **M5.05** Investigate **INC-SD-005** invoice output failure, processing logs and approved recovery.
- [ ] **M5.06** Investigate **INC-SD-006** authorization failure with SU53/trace; no unapproved role change.
- [ ] **M5.07** Each incident: impact, scope, reproduction, document IDs, logs, hypotheses, tests, cause, workaround, permanent action, owner, validation and closure.
- [ ] **M5.08** Produce **3 full 5-Whys or fault-tree RCAs**, separating symptom, trigger, defect and preventive control.
- [ ] **M5.09** Draft **SR-SD-001** new billing variant and **SR-SD-002** access request with scope, approval and acceptance criteria.
- [ ] **M5.10** High-priority incident communication sequence (initial/30-minute update, escalation, workaround, restored confirmation) as fictional or actual as applicable.
- [ ] **M5.11** Demonstrate **reopening one incident after failed regression** and document a **problem record**.

Deliverables: **6 incidents**, **2 service requests**, **3 RCAs**, communication log, problem record and retest evidence. A drafted incident is not a resolved real incident.

## M6 — Requirements, enhancement and testing (R06, R07, R08, R10)

Existing: functional specification, change impact and test case templates in `M6-Requirements-Enhancements-and-Testing/`.

- [ ] **M6.01** Role-play Sales/Logistics/Finance workshop: pain point, goal, constraints, assumptions, in/out scope and fictional sign-off.
- [ ] **M6.02** **CHG-SD-001**: functional specification with as-is/to-be, config/data, output/interfaces, role impacts, exceptions, acceptance and rollback.
- [ ] **M6.03** Map requirements ↔ design ↔ test IDs ↔ evidence in a **traceability matrix**.
- [ ] **M6.04** Design unit, integration (SD/MM/FI/interface) and UAT scripts incl. negative/boundary tests.
- [ ] **M6.05** Execute **6+ test cases** where feasible; record actual results, defects, regression and simulated cross-module steps separately.
- [ ] **M6.06** Complete change impact, effort/risk, dependencies, approval-style record and knowledge transfer.

Deliverables: workshop notes, CHG-SD-001, filled FS, traceability matrix, **6+ tested cases**, defect log and approvals clearly labeled as fictional where simulated.

## M7 — UAT, release control and hypercare (R08, R09, R10)

Existing: `M7-UAT-Release-and-Hypercare/Release-and-Validation-Template.md`.

- [ ] **M7.01** Prepare controlled **mock DEV → QAS → PRD** plan, approvals, dependencies, prechecks, ownership and go/no-go.
- [ ] **M7.02** Inspect SE09/SE10/STMS if authorized. Never claim or execute production imports; optionally authorized training transport.
- [ ] **M7.03** Conduct fictional UAT role-play with scripts, defects, retests and conditional/final simulated business sign-off.
- [ ] **M7.04** Define and, where possible, run smoke checks: order, delivery, PGI, billing, FI posting, output, IDoc status; reconcile.
- [ ] **M7.05** Document rollback versus forward-fix, incident escalation, hypercare handover and lessons learned.
- [ ] **M7.06** Separate an actually observed SAP transport from a paper-based release simulation.

Deliverables: release packet, UAT sign-off (simulated if role-play), smoke-test results, rollback plan, hypercare checklist.

## M8 — Authorization, SoD and audit (R11, R12)

Existing: access-review, authorization, SoD, incident-example and audit templates/examples in `M8-Authorization-Access-and-Audit/`. Existing examples are **already clearly hypothetical**; keep them as examples.

- [ ] **M8.01** Investigate actual own-user SU53/authorization trace only if feasible and appropriate; no unauthorized denial induction.
- [ ] **M8.02** SU01/PFCG role inspection only where permitted; propose least-privilege and maker-checker access request.
- [ ] **M8.03** Access review covering Sales Clerk, Warehouse Operator, Billing Specialist, SD Support Analyst, flagging risks.
- [ ] **M8.04** Evaluate **2 SoD conflicts** and compensating controls, distinguishing potential from confirmed effective access.
- [ ] **M8.05** Compile audit packet: request, approval, role review, SoD, mitigation, change log, periodic sign-off (fictional approval not real).

Deliverables: authorization case, access matrix, **2 SoD assessments**, audit packet; retain original fictional example labels.

## M9 — Global support, bilingual, training and capstone (R13, R14, R15)

Existing: detailed global operations model, handover, training, knowledge-transfer and KPI templates in `M9-Global-Support-and-Training/` (documentation preparation does not count as executed training).

- [ ] **M9.01** Fictional Japan Sales → Singapore Logistics → UK Finance dependency and timezone/owner/escalation/handover exercise.
- [ ] **M9.02** Write an actual Japanese response and English escalation/handover for the chosen case; language review where available.
- [ ] **M9.03** Prepare and deliver/record a **15-minute key-user demo** using validated SAP order-to-billing screenshots, FAQ and safe actions; if only scripted, label simulated.
- [ ] **M9.04** Diagnose an unfamiliar O2C failure as capstone: impact, reproduction, competing hypotheses, corrective proposal, authorized validation and closure.
- [ ] **M9.05** Prepare **5-minute mock hiring-manager portfolio demonstration**: landscape, 3 incidents, change, security/controls, limits.
- [ ] **M9.06** Finalize each of **R01–R15** with true classification and evidence IDs; complete final sign-off review.

Deliverables: bilingual messages, training demonstration/guide, capstone, evidence index, requirement coverage and interview portfolio.

## Post-execution closure (guide sections 5–9)

- [ ] Verify acceptance conditions for the six prescribed incidents and CHG-SD-001/AUD-SD-001 (guide section 5).
- [ ] Check ticket/FS/test deliverables against guide section 6 fields and evidence-quality rubric.
- [ ] Prepare **24 interview scenarios** with only defensible case-specific answers (guide section 7).
- [ ] Draft CV/profile language **only after** verifying completed exercise counts; do not claim a two-week program or commercial production experience (guide section 8).
- [ ] Check final quantitative gate: **2 O2C traces, 6 incident records, 3 RCAs, 1 enhancement, at least 6 tests, 1 UAT/release packet, 1 access review, 2 SoD analyses, 1 bilingual handover, 1 training guide, all 15 requirements** (guide section 9).
- [ ] Execute `PORTFOLIO-VALIDATION.md` checklist, inspect all relative links and screenshots, anonymize, verify privacy settings before any public release.

## Existing repository mapping / missing deliverables

| Area | Existing material | Missing actual output or specifically missing working document |
|---|---|---|
| Gate A + M1 | Short README | All audit and monitoring results; M1 forms newly prepared in this package |
| M2 | O2C process trace template | 2 instantiated, executed traces, flow/swimlane and control checklist |
| M3 | Configuration analysis template | Configuration evidence, 2 incident investigations, change/impact and retests |
| M4 | IDoc diagnostic template | Failed IDoc evidence, logs/output, safe recovery trace/checklist |
| M5 | Incident and RCA templates | 6 filled incidents, 2 SRs, 3 RCAs, communication log, reopened ticket/problem record |
| M6 | FS, impact and test templates | Workshop record, CHG-SD-001, traceability matrix, 6+ actual test results, defects/sign-off |
| M7 | Release/validation template | UAT acceptance, transport observation or mock release, smoke results, rollback/hypercare |
| M8 | 5 templates/examples and README | Actual SU53/role evidence if accessible, 4-persona access review, 2 assessed SoD cases; examples remain simulations |
| M9 | 5 substantive guides/templates and README | Specific JP/EN case, demo delivery evidence, capstone, presentation, final coverage evidence |
| Project-wide | `Requirement-Coverage.md`, `Evidence-Register.md`, `PORTFOLIO-VALIDATION.md` | Actual EV references, all 15 R-status decisions, final validation/sign-off |

**Current verified SAP exercise count: 0.** No screenshots, live document numbers, real SAP incident diagnoses or live configuration changes are present in the uploaded repository.
