# CHG-SD-001 — Functional specification: payment-terms billing hold

| Field | Value |
|---|---|
| Reference | CHG-SD-001; continuation of [CHG-M3-001](../M3-Configuration-and-Logistics/Change-Proposal-CHG-M3-001.md) |
| Module | SAP SD, delivery-related F2 and SD–MM–FI integration |
| Environment | JV2 / client 100 (target); T41 / 400 (independent read-only reference only) |
| Author | Mikko Koivistoinen |
| Status | **Functional design proposed; no implementation or authorization** |
| Execution basis | Actual negative/baseline tests and documented/simulated design |

## 1. Executive summary

**Need:** A hypothetical controlled payment-terms review should prevent an in-scope F2 invoice until authorized release. Existing sandbox tests show billing block 04 did not stop the tested F2 invoices. **Solution concept:** Confirm the intended business source/level and billing type; inspect the **actual JV2** configuration; only then propose the smallest authorized adjustment or an alternative control. No specific customizing edit has been established as the root-cause fix.

## 2. Requirements

Use [REQ-M6-01–REQ-M6-06](Requirements-Workshop-and-CHG-SD-001.md) and their [traceability matrix](Requirements-Traceability-Matrix.md). Sales defines what constitutes a payment-term exception; Logistics defines whether picking/PGI remain allowed; Finance specifies billing/AR hold semantics and release authorization. These are **proposed** responsibilities, not actual interviews or approvals.

## 3. As-is / to-be process

| Stage | As-is observed in JV2 | To-be proposed (not implemented) |
|---|---|---|
| Sales order | OR, TAN item, TG11 and sales area 1010/10/00 used successfully; order header/item block 04 entered in independent cases | Relevant block set only for a valid approved business reason |
| Delivery | Item 10; delivery and PGI were allowed in observed negative tests | Shipment/PGI relationship to invoice hold explicitly approved by Logistics |
| Billing | F2 invoice created in all tested active-04 variants: 90000304, 90000305, 90000306, 90000307 | Prevent F2 if active hold is within the **approved** applicable source/level; notify user why |
| Finance | 90000304 and M6 invoices 90000306/307 had accounting documents | No FI posting should arise for an invoice prevented by the proposed control; after release, normal posting |
| Release | No controlled 04 release demonstrated | Authorized user removes applicable hold after business approval; one invoice, no duplicates |

**Do not generalize:** The observations demonstrate JV2 behavior for these training document paths, not all SAP S/4HANA systems or billing methods. Order-related/direct billing (e.g. service items) was not tested.

## 4. Organizational and data scope

| Element | Verified/used example |
|---|---|
| Company code | 1010 (earlier M2 FI scenario; not inferred from the new invoice link alone) |
| Sales organization / distribution channel / division | 1010 / 10 / 00 |
| Plant / shipping point | 1010 / 1010 (from M1/M3) |
| Customer / ship-to | 1000193 |
| Order type / item category / material | OR / TAN / TG11 |
| Billing | F2, EUR 17.55 net for 1 PC in observed examples |
| Billing reason | 04 — Check Payment Terms |

### Design objects — **investigation candidates, not verified JV2 settings**

| Candidate object | Observed / known | Required decision or check |
|---|---|---|
| Block reason definition | Reason 04 selectable in document fields | Validate intended function and applicability in JV2 |
| CBC activity 102401, assignment of blocking reasons to billing types | JV2 access **Unauthorized** (EV-079–EV-080) | Authorized read-only review for F2 / reason 04 before deciding any change |
| Delivery/order billing source logic and F2 copy control | Not established | Evaluate how header/item blocks affect delivery-based billing in this tenant |
| Billing type F2 | Used for tested invoices | Verify explicit eligibility and exception behavior |
| Pricing, partner, credit, tax, account determination | Baseline transaction worked; no change indicated | Confirm no unexpected effect; do not modify without design justification |
| Output/IDoc processes | M4/M5 provide separate observations only | Evaluate future held/issued invoice messaging; no new M6 interface test |

### Proposed functional logic

1. At the **agreed** source-document level, a permitted Sales/Finance role applies reason 04 for a real payment-term exception.
2. When delivery-related billing is requested, the system evaluates the **approved** blocking rule and prevents F2 invoice creation for the affected scope if an active hold is present.
3. The system provides a visible reason/status; no FI entry or billing output should be generated from a **prevented** invoice.
4. Only a permitted role may clear the hold after documented business release.
5. The same eligible delivery can then be invoiced **once**, and the correct FI documents/output follow; duplicate invoice creation is checked.
6. Unblocked orders, items and deliveries continue as existing baseline.

This is a **target design**, not a description of functionality verified in JV2. Source-level enforcement must be determined by owner and configuration analysis. A different workflow control may be required if billing block 04 is not the correct mechanism.

## 5. Exception handling / authorization

A blocked billing attempt should show an actionable reason or exclude the document from a due list in a traceable way. Authorization to set or clear hold requires least-privilege role design, maker/checker where applicable and audit history. No user-role changes or operational approvals have been made. Risk of bypass, overblocking and duplicate post-release invoices must be included in testing.

## 6. Integration impact

| Component | Design consideration | Current evidence |
|---|---|---|
| SD sales | Maintain source and block semantics | EV-027, EV-034, EV-051, EV-083 |
| Delivery / MM | PGI may complete without invoice; do not accidentally prevent authorized shipping | EV-047–EV-048, EV-085 |
| SD billing | Ensure blocked vs unblocked F2 eligibility | EV-031–EV-035, EV-052, EV-086, EV-088 |
| FI | Avoid AR/revenue/tax postings from disallowed invoice | EV-025–EV-026, EV-087, EV-089 |
| Output | Invoice output must correspond to legitimate invoice, no premature/duplicate dispatch | EV-077–EV-078, **no new M6 output retest** |
| IDoc/interface | Review downstream messages and deduplication if in scope | M4 configurations only; no new integration execution |
| Reports | Review billing-due lists, blocked volume and aging | No M6 report executed |

## 7. Test design and acceptance

| Test | Type | Scope | Current status |
|---|---|---|---|
| TC-SD-001 | Integration / baseline | Unblocked OR→delivery→PGI→F2→FI | **Executed earlier, positive** |
| TC-SD-002 | Negative | Order-header 04 vs delivery-related F2 | **Executed earlier, proposed control failed** |
| TC-SD-003 | Negative | Delivery-header 04 vs F2 | **Executed earlier, proposed control failed** |
| TC-SD-004 | Negative/boundary | Order-item 04; delivery item blank | **Executed in M6, proposed control failed** |
| TC-SD-005 | Negative/boundary | Delivery-item 04; order unblocked | **Executed in M6, proposed control failed** |
| TC-SD-006 | Unit / logistics guard | Partial picking prevents PGI; fix and retry | **Executed earlier, passed its own logistics control** |
| TC-SD-007 | Integration / output reference | Successfully billed invoice has output processing | **Executed earlier; not post-change** |
| TC-SD-008 | Release/regression | After approved fix, blocked→approved release→single invoice/FI | **Not executed; depends on actual fix** |
| TC-SD-009 | UAT | Sales/Logistics/Finance sign-off on agreed billing hold | **Not executed; planned fictional script only** |

Detailed steps/results: [Test Execution and Defect Register](Test-Execution-and-Defect-Register.md). **No post-change test** is possible yet because no change was implemented.

## 8. Implementation and recovery — NOT EXECUTED

**Preconditions:** actual business decision, authorized JV2 CBC access, verified before-state, technical owner decision and approved change. **Sequence (proposed only):** inspect JV2 settings → decide minimal valid control → record approval → change an authorized sandbox → run unit/integration/regression and UAT → consider release with rollback/forward-fix instructions. No transport/CBC activation/rollback occurred.

**Rollback concept:** retain exact before-state, reapply only the approved previous configuration if the validated change causes issues; reconcile billing queues/invoices/FI/output; retest. Exact operational mechanism unknown pending authorizations.

## 9. Author review and proposed-change boundary

| Review / operational role | Portfolio outcome |
|---|---|
| Portfolio author | **Training functional specification reviewed and accepted as a completed proposal** |
| Sales, Logistics and Finance | Fictional stakeholders for the training exercise; no real business participants |
| SAP configuration owner | JV2 CBC inspection denied; actual configuration decision was not possible in this sandbox |
| Change manager | Operational implementation/change authorization not applicable to this independent portfolio |

**Conclusion:** The functional specification and associated test analysis are **complete and author-accepted as portfolio documents**. The enhancement itself remains a proposal; no SAP implementation, production business approval or post-change retest is claimed.
