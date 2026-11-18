# M6 — Executed test register, open tests and defect record

**Classification:** Seven relevant **executed historical/pre-change training test cases** reused or extended; two new JV2 test chains are TC-SD-004 and 005. There has been **no SAP configuration change, no post-change regression and no actual UAT**. A test's **FAIL** refers to the *proposed* business control expectation, not a verified SAP software defect.

## 1. Test summary

| ID | Type | Starting condition / expected result | Actual SAP result | Status / evidence |
|---|---|---|---|---|
| TC-SD-001 | Positive integration baseline | Unblocked standard TG11 item: order→pick→PGI→F2→FI should work | Order 1055→delivery 80000784→PGI 4900001488→invoice 90000303→FI 9400000057 | **PASS baseline (earlier M2)** · EV-017–EV-026 |
| TC-SD-002 | Negative order-header hold | Order 1056 header 04 should stop F2 **if business control applies** | F2 90000304 and FI 9400000058 created with block retained | **FAIL proposed hold (earlier M2/M3)** · EV-027, EV-031–EV-035, EV-051 |
| TC-SD-003 | Negative delivery-header hold | Delivery 80000787 header 04 expected to stop F2 in proposed design | Delivery PGI 4900001490; invoice 90000305 created | **FAIL proposed hold (earlier M3)** · EV-038–EV-039, EV-052; no independent saved-block screenshot / FI posting detail |
| TC-SD-004 | Negative / source-level boundary | Order item 10 block 04 with delivery-item block blank expected to prevent F2 **if applicable** | Order 1060→delivery 80000789→PGI 4900001496→F2 90000306→accounting docs | **FAIL proposed hold (new M6)** · EV-083–EV-087 |
| TC-SD-005 | Negative / source-level boundary | Unblocked order, delivery item 10 block 04 expected to prevent F2 in proposed design | Order 1061→delivery 80000790→PGI 4900001497→invoice 90000307→accounting docs | **FAIL proposed hold (new M6)** · EV-088–EV-089 plus save confirmations |
| TC-SD-006 | Negative → correction, logistics baseline | Delivery 80000788, 2 PC, picked 1 PC; PGI should reject until picking complete | PGI error VLMOVE 030; after correction PGI 4900001491 posted | **PASS logistics guard (earlier M3)** · EV-045–EV-050, EV-073 |
| TC-SD-007 | Downstream output baseline | Existing valid F2 invoice produces expected output records | Invoice 90000303 output BILLING_DOCUMENT/PRINT Completed, ADS/queue log observed | **PASS output baseline (earlier M5)** · EV-077–EV-078; not related to a corrected billing hold |
| TC-SD-008 | Post-change release/integration/regression | Under an **implemented approved rule**, active hold blocks; approval/release permits exactly one F2/FI | No change or approved release; cannot test | **NOT EXECUTED / BLOCKED** by JV2 access and approval |
| TC-SD-009 | Business UAT | Sales/Finance/Logistics validate agreed rule and sign acceptance | No real business participants or UAT | **NOT EXECUTED**; scripted design only |

**Do not report seven post-change regression passes:** TC-SD-001–007 are heterogeneous relevant **before-change** historical baselines, negative cases and downstream observations. TC-SD-008/009 are explicitly unexecuted.

## 2. Detailed new executed cases

### TC-SD-004 — Sales-order item 04; delivery item blank

**Environment:** JV2 / client 100, VA01/VA03, VL01N/VL02N, VF01/invoice display. **Data:** OR, 1010/10/00, customer 1000193, material TG11, 1 PC, plant 1010; customer reference M6-TC004.

| Step | Expected or setup | Actual observed | Evidence / limitation |
|---|---|---|---|
| 1 | Header block blank; item 10 block 04 | Item 10 block 04 visible before save; user confirmed header cleared and order 1060 saved | EV-083; no screenshot of saved header clearance |
| 2 | Create delivery; inspect delivery-item block | Delivery 80000789 saved; delivery-item block visibly blank | EV-084, user confirmation |
| 3 | Pick 1 PC, post goods issue | Delivery 80000789 linked to material document 4900001496 | EV-085, user confirmation |
| 4 | Test delivery-related F2 | Saved invoice 90000306, 1 PC net EUR 17.55 | EV-086 |
| 5 | Inspect accounting links | 0L document **0100000736**, 2L **7000000127** (other accounting/CO records listed) | EV-087; ledger balances not separately inspected |

**Verdict:** **FAIL proposed invoice hold** (invoice and accounting documents created). The block was seen on the sales-order item *before saving* and its persistence after save was not separately imaged. Do not claim a configuration root cause or a completed post-fix retest.

### TC-SD-005 — Delivery-item 04 with unblocked sales order

**Environment/data:** JV2 / 100, OR, 1010/10/00, customer 1000193, TG11 1 PC, plant 1010; customer reference M6-TC005. Sales order 1061 user-confirmed saved with all sales-order blocks blank; no screenshot of those final blank states.

| Step | Expected or setup | Actual observed | Evidence / limitation |
|---|---|---|---|
| 1 | Create unblocked order and delivery | Order 1061, delivery 80000790 user-confirmed saved | Chat save confirmations; screenshot of initial saved order not retained |
| 2 | Apply item 10 billing block 04 at delivery | Delivery item Financial Processing shows “Check Payment Terms” | EV-088; user confirmed save, no independent post-save reopen screenshot |
| 3 | Pick and post PGI | Material document **4900001497** user-confirmed created | User save confirmation; no separate PGI screenshot |
| 4 | Attempt F2 with active item block | User confirmed saved invoice **90000307** | User save confirmation; no invoice-overview screenshot |
| 5 | Inspect accounting links | 0L **0100000737**, 2L **7000000128** (additional accounting/CO documents listed) | EV-089; no ledger balance review |

**Verdict:** **FAIL proposed delivery-item invoice hold** under the reported saved-block state. FI accounting documents are visibly listed. A separate re-opened saved item and invoice overview would strengthen independently reproduced evidence; avoid overstating screenshot scope.

## 3. Defect/problem register

| ID | Symptom and impact | Root cause / status | Next action |
|---|---|---|---|
| DEF-M6-001 / PRB-SD-001 | Delivery-related F2 invoice created in four observed active 04 header/item scenarios; potential payment-control bypass in this training business scenario | **Open; actual JV2 root cause unknown; no authorized CBC inspection**. T41 assignments unrelated to JV2 settings | Confirm business expectation; authorize JV2 CBC review; select valid control design; approve change and retest |
| DEF-M6-002 | Source-state screenshot depth: saved order-item header clearance and delivery-item block persistence not independently recaptured | **Evidence limitation, not a proven SAP defect** | If further evidence required, revisit existing saved orders/deliveries read-only; do not generate random new transactions |

## 4. Planned, unexecuted post-change unit / integration / UAT scripts

| Test | Procedure after approval and implementation | Required verification |
|---|---|---|
| Unit — block eligibility | Use fresh controlled applicable source, activate 04, request F2 | Billing rejected/withheld with actionable reason, no invoice created |
| Integration — authorized release | Obtain mock or real approved business authorization as applicable, release 04, bill same reference | Exactly one invoice, SD–FI links correct, no duplicate |
| Negative/boundary | Compare order-header, order-item, delivery-header and delivery-item; other reasons and document types | Each combination follows **approved source-level design**, not blanket assumptions |
| Regression | Unblocked order→delivery→PGI→F2→FI; output; due list/interface if relevant | No unintended blocking, FI/output reconciliation |
| UAT | Actual Sales, Logistics and Finance representatives review use cases and approval controls | Real signed acceptance only if actual participants approve; otherwise **simulated script** |

**All procedures in this section are NOT EXECUTED.** No remediation, approval, transport, post-release monitoring or business acceptance is claimed.
