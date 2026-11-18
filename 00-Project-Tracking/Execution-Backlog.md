# SAP SD Support Lab — Execution Backlog and Coverage Review

**Project state:** M1 has verified monitoring observations and two corrected, controlled sandbox incidents (EV-001–EV-016); its broader mandatory access audit remains **partially open**. M2 has two fully executed O2C chains through balanced FI postings (EV-017–EV-035). Billing-block negative test failed. M3 now has read-only configuration observations, two executed incident reproductions with corrected pricing/picking, and a proposed change/impact design; CBC inspection is blocked. M4 includes verified IDoc and output inspections, configured intercompany invoice routing, and documented-only recovery. M5 now has six evidence-qualified case records, three RCAs, proposed SRs, a simulated communication/reopening exercise and an open problem record; several planned negative/fix/retest cases remain unexecuted. M6–M9 retain templates and backlog work.  

## Evidence and completion rules

- A prepared template or fictional example is **documentation**, not evidence of SAP execution.
- Mark an SAP task **Executed** only after the actual step is performed in an authorized SAP training system and the result is verified and logged (transaction/Fiori app, client and document IDs where applicable, expected versus actual, anonymized screenshot or system output).
- **Simulated** = worked through on paper, explicitly without claiming SAP execution. **Blocked** = confirmed infeasible because of access, data, or tenant constraints. **Not Started** = no outcome yet.
- A read-only system inspection may be an executed *inspection*, but does not imply that the related corrective action, configuration change, or end-to-end transaction has been executed.
- Update requirement rows as evidence is produced; use **In Progress** for partial coverage and link to exact evidence. Do not present a partly covered job requirement as fully executed.
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

M1 evidence now captured in the access/baseline, support runbook and triage files. Some access-audit capabilities are explicitly deferred to the applicable later modules; these are not implicitly verified.

- [ ] **M1.01 — Partial:** Record release/client, user permissions and access matrix (Gate A). User-specific 14-role snapshot was verified, but System → Status, release and complete client/permission boundaries were not independently rechecked. Gate A remains open.
- [ ] **M1.02 — Partial:** Inspect org and sample data: sales org, distribution channel, division, plant, shipping point, billing setup, customer/material, stock and approved scenario. Verified fields are recorded. **Company code 1010 was independently confirmed later in M2 (EV-025–EV-026); actual delivery type remains unverified.**
- [ ] **M1.03 — Partial:** Monitoring sweep: verified accessible sales fulfillment, deliveries, billing, output and SIT logs; **incomplete-document, blocked-delivery and IDoc/interface/general SD log totals were not measured** (scope limitations documented).
- [x] **M1.04** Define severity, impact, urgency, response/SLA *illustrations*, escalation owners, ticket states, evidence standards and daily handover format for the fictional company. **Completed as simulated operating design.**
- [x] **M1.05** Create **two triage tickets**. **Completed with two deliberately reproduced, diagnosed, corrected and retested sandbox cases: order 1055 delivery block and order 1056 PPR0 manual pricing override.**
- [x] **M1.06** Baseline KPIs: incident volume and age, failed interfaces, billing backlog, resolution performance. **Completed where measurable; remaining values explicitly N/A, not invented.**

Deliverables: **access audit**, **support runbook**, **baseline monitoring sheet**, **2 triage tickets**, anonymized EV references. Files: `M1-Landscape-and-Monitoring/Access-Audit-and-Baseline.md` and `M1-Landscape-and-Monitoring/Support-Runbook-and-Triage.md`.

## M2 — Two complete order-to-cash chains (R02)

 **Two O2C chains complete through FI** (EV-017–EV-035). Distinguish O2C passes from the **failed** billing-block negative test, open for M3.

- [ ] **M2.01 — Partial, core data checks executed:** Customer 1000193, material TG11, sales area 1010/10/00, plant 1010, shipping point 1010, 1 PC order, missing customer company-code 1010 error and corrective extension. Comprehensive stock balance and all master-field checks were not collected.
- [ ] **M2.02 — Partial, core order/pricing/ATP executed:** Orders 1055 and 1056, item TAN, PPR0 EUR 17.55, 1 PC, tax EUR 3.33; order 1056 confirmed 1 PC. Credit check and complete ATP details for order 1055 not independently evidenced.
- [ ] **M2.03 — Partial, picking/PGI executed:** Deliveries 80000784/80000785 fully picked and goods issues 4900001488/4900001489 created. **Movement type and stock before/after remain unverified**; do not claim those checks passed.
- [x] **M2.04 — Executed billing/FI:** F2 invoices 90000303/90000304; RV journals 9400000057/9400000058; each balanced EUR 20.88 debit/credit. Ordered/delivered/billed 1/1/1 PC.
- [x] **M2.05 — Executed second O2C variation:** Order 1056 with persisted header billing block 04. Invoice was nonetheless generated via delivery-related billing; **negative enforcement test FAIL**, root configuration cause **OPEN** for M3. Never describe the billing block as having worked.
- [x] **M2.06 — Documentation completed:** Two case-specific O2C traces, executed Sales → Logistics → Finance swimlane, process-control checklist and 19 screenshot evidence files.

**Deliverables:** [M2 README](../M2-Order-to-Cash/README.md), [Scenario 1](../M2-Order-to-Cash/O2C-Scenario-01-Standard-and-FI-Correction.md), [Scenario 2](../M2-Order-to-Cash/O2C-Scenario-02-Billing-Block-Exception.md), [swimlane](../M2-Order-to-Cash/O2C-Executed-Swimlane-and-Controls.md), [controls](../M2-Order-to-Cash/O2C-Process-Control-Checklist.md). Additional checks expressly remain **not verified**, despite core chain completion.

## M3 — Configuration and logistics exceptions (R02, R07, R10)

Existing: `M3-Configuration-and-Logistics/Configuration-Analysis-Template.md`.

- [ ] **M3.01** **Partial:** OR/TAN/CP, shipping-point inputs and transaction outcomes observed; VOV* and copy-control customizing not inspected (CBC blocked).
- [ ] **M3.02** **Partial:** PPR0 condition record/procedure and posted FI accounts inspected, but account determination customizing not inspected.
- [x] **M3.03** CHG-M3-001 proposed for billing block 04 / F2; baseline, dependencies, authorization, test and rollback documented; **proposal only**.
- [x] **M3.04** **Blocked:** CBC reported Unauthorized, so no setting was edited. Read-only and proposal status retained; **no implementation claimed**.
- [ ] **M3.05** **Partial:** wrong price 1056 (M1), partial picking 1059/80000788 (M3) reproduced, diagnosed, corrected with successful retests; **broader regression not executed**.
- [x] **M3.06** Change impact and regression test matrix **prepared** for Sales, Logistics, FI, outputs, interfaces, reporting and roles; **proposed** analysis, not executed regression.

Deliverables: filled configuration workbook, controlled change proposal, impact matrix, **2 exception investigation records**, before/after test evidence.

## M4 — IDoc, interfaces, logs and output (R03)

Evidence-backed deliverables are linked from [M4 README](../M4-IDocs-Interfaces-and-Output/README.md).

- [x] **M4.01** WE02/WE05: examined historical IDoc control/data/status, including `DELFOR` `180016` status `56` partner-profile error.
- [x] **M4.02** Inspected `WE20` partner profiles and port parameters; `WE19`/`BD87` available, but no live reprocessing or partner-profile change claimed.
- [x] **M4.03** Documented historical inbound `DELFOR` error with sender, message/basic type, status, diagnosis and proposed remediation. Root cause configuration change and recovery not verified.
- [x] **M4.04** Reviewed available application-log navigation, output status and intercompany `OPD`/`WE41`/`WE20`/`WEL1`/MM/FI-EDI configuration; verified order `374` output `Completed`. No linked `SLG1` invoice log or posted `INVOIC` IDoc established.
- [x] **M4.05** Completed interface/output monitoring checklist, escalation ownership, change approval and deduplication/reconciliation controls.
- [x] **M4.06** Documented the recovery process as a **simulation only**. No actual IDoc failed → repaired → reprocessed cycle executed or claimed.

Deliverables: actual IDoc diagnosis, intercompany configuration trace, positive output evidence, monitoring checklist and simulated recovery runbook. No verified IDoc failure-to-success retest.

## M5 — Incident, problem and RCA (R01, R04, R05)

**Current state:** Documentation deliverables prepared, SAP execution **partial**, limitations identified in [M5 README](../M5-Incident-and-Root-Cause-Management/README.md). Two templates retained as original blank working forms.

- [ ] **M5.01 — Partial:** INC-SD-001 investigated, corrected and retested; cross-customer regression not executed (EV-014–EV-016, EV-042, EV-071–EV-072).
- [ ] **M5.02 — Partial:** INC-SD-002 negative PGI, correction and positive GI verified; stock and wider shipment/billing checks not executed (EV-045–EV-050, EV-073).
- [ ] **M5.03 — Partial:** INC-SD-003 **billing-to-FI** failure corrected; billing-creation failure not reproduced. Separate JV2 billing-block control problem remains unresolved (EV-021–EV-026, EV-074–EV-076, PRB-SD-001).
- [ ] **M5.04 — Partial:** INC-SD-004 earlier DELFOR status 56 diagnosed; no approved WE20 change, IDoc reprocessing or target retest (EV-053).
- [ ] **M5.05 — Partial:** INC-SD-005 successful invoice PRINT output/ADS log inspected; no failure, correction or print confirmation (EV-077–EV-078).
- [ ] **M5.06 — Partial:** INC-SD-006 actual CBC Unauthorized reproduced (EV-079–EV-080); T41 IMG inspected read-only (EV-081–EV-082), which does not establish JV2 configuration. No trace/root-cause verification or role change.
- [x] **M5.07 — Documentation completed, technical closure mixed:** Six separate case records include symptom, investigation, action or unexecuted action, limits and appropriate status; not six successfully closed actual incidents.
- [x] **M5.08 — Documentation completed:** Three detailed evidence-limited 5-Whys RCAs for pricing, picking, FI master data. Deeper unknown causes not invented.
- [x] **M5.09 — Documentation completed:** SR-SD-001 billing variant and SR-SD-002 CBC access. Neither request submitted or approved.
- [x] **M5.10 — Simulated/documented:** Communications sequence drafted using real FI symptom, not sent or assigned actual priority.
- [ ] **M5.11 — Mixed:** Actual JV2 billing-block negative tests failed expected control; problem record prepared. Service-desk reopening is simulated, not executed in a ticketing system.

Deliverables: **Six investigation records, two proposed SRs, three RCAs, a simulated communication log, one open problem record, evidence-based failed-control and simulated reopening record**. The unexecuted failure/fix/retest scopes are explicitly open.

## M6 — Requirements, enhancement and testing (R06, R07, R08, R10)

**Document package prepared; actual SAP tests partial/pre-change; business control and change open.** See [M6 README](../M6-Requirements-Enhancements-and-Testing/README.md).

- [x] **M6.01 — Simulated/documented:** Role-play Sales/Logistics/Finance viewpoints, goal, constraints, assumptions and business decisions. **No real meeting or sign-off**.
- [x] **M6.02 — Proposed functional design:** CHG-SD-001 and completed functional specification, as-is/to-be, configuration unknowns, outputs/interfaces, roles, exceptions, acceptance and recovery. **No implementation**.
- [x] **M6.03 — Documentation completed:** Requirement/design/test/evidence traceability matrix with actual status distinctions.
- [x] **M6.04 — Test design completed:** Unit, integration, negative, source-level boundary, regression and UAT scripts; post-change/UAT unexecuted.
- [x] **M6.05 — Seven evidence-backed pre-change cases, mixed results:** TC-SD-001–007 documented. New JV2 TC-SD-004 and 005 demonstrate failure of expected block 04 control; earlier M2/M3/M5 tests reused. **No post-fix regression**; TC-SD-008/009 not executed. EV-083–EV-089 plus cited earlier evidence.
- [x] **M6.06 — Analytical record completed:** Cross-module impact, risk/complexity, pending authorization/approval, proposed rollback and written knowledge-transfer. **No actual approval, delivery or corrective action**.

Deliverables: [workshop/change](../M6-Requirements-Enhancements-and-Testing/Requirements-Workshop-and-CHG-SD-001.md), [functional specification](../M6-Requirements-Enhancements-and-Testing/Functional-Specification-CHG-SD-001.md), [impact assessment](../M6-Requirements-Enhancements-and-Testing/Change-Impact-Assessment-CHG-SD-001.md), [traceability](../M6-Requirements-Enhancements-and-Testing/Requirements-Traceability-Matrix.md), [test/defect register](../M6-Requirements-Enhancements-and-Testing/Test-Execution-and-Defect-Register.md), [handover](../M6-Requirements-Enhancements-and-Testing/Knowledge-Transfer-and-Approval-Record.md). **Problem PRB-SD-001 remains open**.

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
- [ ] **M9.03** Prepare and deliver/record a **key-user demo** using validated SAP order-to-billing screenshots, FAQ and safe actions; if only scripted, label simulated.
- [ ] **M9.04** Diagnose an unfamiliar O2C failure as capstone: impact, reproduction, competing hypotheses, corrective proposal, authorized validation and closure.
- [ ] **M9.05** Prepare **mock hiring-manager portfolio demonstration**: landscape, 3 incidents, change, security/controls, limits.
- [ ] **M9.06** Finalize each of **R01–R15** with true classification and evidence IDs; complete final sign-off review.

Deliverables: bilingual messages, training demonstration/guide, capstone, evidence index, requirement coverage and interview portfolio.

## Portfolio completion review

- [ ] Verify acceptance conditions for the incident, change and audit case set.
- [ ] Check incident, functional specification and test-case completeness and evidence quality.
- [ ] Prepare interview scenarios with defensible case-specific answers.
- [ ] Draft CV/profile language only after verifying completed exercises; do not claim commercial production experience based on lab work.
- [ ] Check final quantitative gate: **2 O2C traces, 6 incident records, 3 RCAs, 1 enhancement, at least 6 tests, 1 UAT/release packet, 1 access review, 2 SoD analyses, 1 bilingual handover, 1 training guide, all 15 requirements**.
- [ ] Execute `PORTFOLIO-VALIDATION.md` checklist, inspect all relative links and screenshots, anonymize, verify privacy settings before any public release.

## Existing repository mapping / missing deliverables

| Area | Existing material | Missing actual output or specifically missing working document |
|---|---|---|
| Gate A + M1 | Access audit/monitoring baseline, support runbook, two actual controlled cases, 16 evidence images; module README | Company code 1010 was verified subsequently in M2; delivery type, incomplete/blocked-delivery counts and specialist access checks remain open or deferred; publication permissions still require final review |
| M2 | O2C process trace template | 2 instantiated, executed traces, flow/swimlane and control checklist |
| M3 | Configuration analysis template; filled CFG-SD-001, 2 actual incident investigations, billing-block observation, CHG-M3-001 proposal, impact matrix, EV-036–EV-052 | CBC settings and copy-control customizing inaccessible; proposed configuration not implemented; broad regression not executed |
| M4 | Completed IDoc diagnostic record, interface trace, output checklist, recovery runbook and screenshots | Live IDoc reprocessing and target `90FR` invoice remain unverified; no extra work is claimed |
| M5 | Six filled case records, 2 proposed SRs, 3 RCAs, simulated communications/reopening, open problem record, EV-071–EV-082 | Unverified cross-customer regression, billing-creation failure, IDoc recovery, output-failure recovery, CBC trace/fix, actual ticket reopening |
| M6 | FS, impact and test templates | Workshop record, CHG-SD-001, traceability matrix, 6+ actual test results, defects/sign-off |
| M7 | Release/validation template | UAT acceptance, transport observation or mock release, smoke results, rollback/hypercare |
| M8 | 5 templates/examples and README | Actual SU53/role evidence if accessible, 4-persona access review, 2 assessed SoD cases; examples remain simulations |
| M9 | 5 substantive guides/templates and README | Specific JP/EN case, demo delivery evidence, capstone, presentation, final coverage evidence |
| Project-wide | `Requirement-Coverage.md`, `Evidence-Register.md`, `PORTFOLIO-VALIDATION.md` | Actual EV references, all 15 R-status decisions, final validation/sign-off |

**Current verified M1 controlled incident exercises: 2.** Orders 1055 and 1056 were intentionally faulted, diagnosed and corrected in SAP, with verified retests; see EV-009–EV-016. Monitoring/authorization inspections are separately evidenced in EV-001–EV-007. **Two M2 O2C chains through FI are executed and evidenced (EV-017–EV-035). The billing-block negative test failed. No M3 live configuration change, production support or M4 IDoc recovery is claimed. M4 inspections and positive sales-order output are evidenced.**
