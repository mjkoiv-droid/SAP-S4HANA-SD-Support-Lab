# M6 — Requirements, enhancements and testing

**Portfolio status:** **Documentation completed; SAP execution partial (7 relevant historical/pre-change cases, including 2 new M6 tests); corrective change open and unimplemented.** No real stakeholder workshop, actual UAT or post-change regression.

## Objective and chosen business scenario

Develop a traceable functional design and test package for **CHG-SD-001 — payment-terms billing-block 04 for delivery-related F2 billing**. Extend verified M2–M5 work without repeating successful O2C exercises unnecessarily. The observed JV2 control gap is tracked in [PRB-SD-001](../M5-Incident-and-Root-Cause-Management/Problem-Record-PRB-SD-001.md); root cause is **not confirmed**.

## Deliverables

| File | Content | Classification |
|---|---|---|
| [Workshop and CHG-SD-001](Requirements-Workshop-and-CHG-SD-001.md) | Simulated stakeholder positions, requirement IDs, acceptance conditions, open approvals | **Documented role-play / proposed change** |
| [Functional Specification](Functional-Specification-CHG-SD-001.md) | As-is/to-be, billing and integration logic, config candidates, controls, test design | **Proposed**, not implemented |
| [Change Impact Assessment](Change-Impact-Assessment-CHG-SD-001.md) | SD/MM/FI, output, risks, approvals, rollback and dependencies | **Analytical**, no config changed |
| [Traceability Matrix](Requirements-Traceability-Matrix.md) | Requirements ↔ design ↔ test ↔ EV references | **Documented**, actual statuses maintained |
| [Test Execution and Defect Register](Test-Execution-and-Defect-Register.md) | Seven evidence-backed pre-change cases, two new M6 test chains, two planned unexecuted cases | **Mixed actual execution and unexecuted designs** |
| [Knowledge Transfer and Approval Record](Knowledge-Transfer-and-Approval-Record.md) | Handover, owner actions, pending sign-off | **Written only**, not delivered |
| [Functional Specification Template](Functional-Specification-Template.md) | Reusable blank working template | Template |
| [Change Impact Template](Change-Impact-Assessment-Template.md) | Reusable blank working template | Template |
| [Test Case Template](Test-Case-Template.md) | Reusable blank working template | Template |

## Actual new M6 SAP tests — JV2/100

| Test | Controlled starting condition | Actual result | Evidence |
|---|---|---|---|
| TC-SD-004 | Order `1060`, item 10 block 04; delivery `80000789` item block blank; PGI `4900001496` | F2 invoice `90000306` created; accounting links 0L `0100000736`, 2L `7000000127` | [EV-083–EV-087](Test-Execution-and-Defect-Register.md) |
| TC-SD-005 | Order `1061` unblocked; delivery `80000790` item 10 block 04; PGI `4900001497` | F2 invoice `90000307` user-confirmed saved; accounting links 0L `0100000737`, 2L `7000000128` | [EV-088–EV-089](Test-Execution-and-Defect-Register.md) |

Both cases **failed the proposed business-control expectation**. They do not prove that JV2 has a defective or misconfigured SAP billing rule. Evidence detail and screenshot limitations are recorded in the [test register](Test-Execution-and-Defect-Register.md).

## Reused executed evidence (no redundant new transactions)

- **TC-SD-001:** Unblocked order `1055` through FI, M2 EV-017–EV-026 — positive O2C baseline.
- **TC-SD-002:** Order-header billing block 04 on order `1056` failed to prevent F2/ FI, M2/M3 EV-027–EV-035, EV-051.
- **TC-SD-003:** Delivery-header billing block 04 on delivery `80000787` failed expected F2 hold, M3 EV-038–EV-039, EV-052; saved-block screenshot depth limited.
- **TC-SD-006:** Partial-picking negative/repair test, M3 EV-045–EV-050 — separate logistics baseline.
- **TC-SD-007:** Successful invoice output baseline, M5 EV-077–EV-078 — **not** post-change output validation.

**Outstanding:** TC-SD-008 controlled authorized block release + single-invoice retest, TC-SD-009 real UAT, JV2 CBC diagnosis, approved fix, actual change approvals and post-change regression. T41/400 IMG [EV-082](../M5-Incident-and-Root-Cause-Management/evidence/t41-img-billing-block04-f2.png) concerns **T41 only**, not the JV2 target tenant.

**Evidence folder:** [M6 screenshots](evidence/). **Important:** Some save/block persistence states were confirmed in the actual workshop chat, not independently captured after-save; see specific test descriptions. All images are SAP training screenshots, not customer-production evidence.
