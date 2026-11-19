# M5 — Incident, Problem and Root Cause Management

**State: DOCUMENTED with evidence-qualified partial execution.** Three controlled/resolved SAP cases have verified corrective outcomes; a fourth case has IDoc diagnosis only, a fifth records a successful invoice-output baseline rather than a failed output incident, and a sixth captures an open CBC authorization denial. **Six case records are not six resolved incidents.** No production client work is claimed.

## Objective and classifications

Demonstrate an SD support investigation process: problem definition → initial hypotheses → targeted SAP checks → evidence-based diagnosis → authorization-aware correction (where actually executed) → retest → closure or escalation. Reuse M1–M4 evidence instead of manufacturing failures. The independent T41/400 IMG inspection is **not** evidence of JV2/100 customizing.

## Six case investigations

| ID | Case and link | System | Verified status | Scope boundary |
|---|---|---|---|---|
| INC-SD-001 | [Manual PPR0 pricing override](Incident-INC-SD-001-Pricing.md) | JV2/100 | **Corrected and retested** | Single order, no cross-customer regression |
| INC-SD-002 | [Partial picking / PGI rejection](Incident-INC-SD-002-Picking.md) | JV2/100 | **Corrected and retested** | GI complete; overall delivery In Process and billing unverified |
| INC-SD-003 | [Billing-to-FI posting failure](Incident-INC-SD-003-Billing-FI.md) | JV2/100 | **Corrected and FI journal verified** | Not an invoice-creation failure; AR not cleared |
| INC-SD-004 | [Inbound DELFOR IDoc error](Incident-INC-SD-004-IDoc.md) | T41/400 | **Diagnosed only** | Existing shared IDoc; no replay or reprocessing |
| INC-SD-005 | [Invoice output assessment](Incident-INC-SD-005-Output.md) | JV2/100 | **Positive baseline verified** | No failure reproduced; no output fix or physical print confirmation |
| INC-SD-006 | [CBC Unauthorized](Incident-INC-SD-006-CBC-Access.md) | JV2/100 | **Denied; still open** | Root cause/permissions not verified; no role change |

## Detailed RCA reports

1. [RCA-SD-001 — Pricing override](RCA-SD-001-Pricing.md): Confirmed manual override, corrected order; governance/prevention not implemented.
2. [RCA-SD-002 — Picking discrepancy](RCA-SD-002-Picking.md): PGI control correctly rejected partial pick; picked quantity fixed and GI passed.
3. [RCA-SD-003 — Billing/FI master gap](RCA-SD-003-Billing-FI.md): Missing customer company-code data; FI posting passed after extension.

Each RCA contains an **evidence-limited 5 Whys**. Unknown deeper organizational causes are explicitly unknown rather than invented.

## Support operations deliverables

- [Service Requests — SR-SD-001 billing variant, SR-SD-002 CBC access](Service-Requests.md): **Proposed only, not submitted**.
- [Incident Communication Log](Incident-Communication-Log.md): **Draft communications, not sent; priority illustrative**.
- [Problem Record PRB-SD-001 — billing block 04 / F2](Problem-Record-PRB-SD-001.md): Actual JV2 negative control tests, root cause open. T41 block `04`→`F2` assignment observed read-only, not transferable as JV2 evidence.
- [Regression and Reopening Exercise](Regression-and-Reopening-Exercise.md): Failed JV2 billing-block negative test **executed**; hypothetical service-desk reopening **simulated**.
- [Incident Template](Incident-Template.md) and [RCA Template](RCA-Template.md): Retained for reuse.

## Module quality review

- [M5 Acceptance and Evidence-Boundary Review](M5-Acceptance-Review.md): distinguishes prepared documents, actual SAP verification, proposed actions and unexecuted tests.

## New actual-system evidence

**EV-071–EV-082** are follow-up screenshots captured during M5. Detailed system results, client qualifications, and links are registered centrally in [Evidence Register](../00-Project-Tracking/Evidence-Register.md). Original M1–M4 evidence is referenced by its original IDs and has **not** been double-counted as new activity.

## Closed portfolio scope review — operational limits

- Pricing cross-customer regression was not performed.
- Picking stock-balance reconciliation and delivery-to-billing outcome are unverified.
- M5's planned **billing creation failure** was not reproduced; the real corrected failure was **billing-to-FI transfer**, and a separate billing-block *negative control* unexpectedly allowed invoicing.
- Inbound IDoc was **pre-existing**. No approved reprocessing / duplicate-prevention validation took place.
- Invoice output was **successful** (ADS rendering/print-channel handoff); no failure-recovery cycle was performed.
- CBC denial is actual, but `SU53`/security trace, role root cause and remediation are **not** verified.
- Formal reopening and incident communications are **simulations**, not actual service-desk system records or delivered stakeholder messages.

**Completion decision: M5 portfolio package COMPLETE with evidence-qualified limits.** R04 and R05 have **Executed with comments** classifications in the final requirement matrix. The unperformed operational tests listed above are scope differences, not outstanding portfolio tasks. No extra random/error-hunting sandbox actions are warranted; open SAP technical findings are preserved.
