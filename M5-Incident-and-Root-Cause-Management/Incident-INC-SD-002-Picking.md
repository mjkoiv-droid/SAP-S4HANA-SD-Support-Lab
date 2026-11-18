# INC-SD-002 — Delivery partial-picking mismatch blocks goods issue

| Field | Recorded result |
|---|---|
| Classification | **Executed; resolved for the training delivery** |
| System/client | JV2 / 100 |
| Transaction(s) | VA03, VL02N, document flow |
| Documents | Order `1059`, delivery `80000788`, material document `4900001491` |
| Material / quantity | TG11, **2 PC delivery**, initial **1 PC picked** |
| Severity / business ownership | Illustrative logistics incident; no measured business disruption or real SLA |
| Evidence | **EV-045–EV-050, EV-073** |

## Symptom and business impact

The delivery required **2 PC** but initially only **1 PC** was picked. SAP showed picking status **B — Partially Picked** and blocked PGI with **VLMOVE 030 — Delivery has not yet been picked (completely)**. If a real shipping delivery, this would delay goods issue until stock and picking are physically reconciled.

## Controlled reproduction

1. Order 1059 for 2 PC was established (**EV-045**).
2. Partial picking of 1 PC was retained against delivery 80000788; picking status B (**EV-046**).
3. Attempted PGI; SAP returned **VLMOVE 030** (**EV-047**).
4. Diagnosed picked-versus-delivery mismatch. No evidence of stock shortage was established; inventory balance was not measured.

## Remediation and verification

- **Executed corrective step:** Update the picked quantity to 2 PC in VL02N and save (save confirmation reported during the original workshop).
- **Executed retest:** Retry PGI; system created goods-issue material document **4900001491** (**EV-048**).
- **Independent read-only follow-up:** Order 1059 is **Completed**, picking request records **2 PC / Completed**, goods issue `4900001491` is **Complete** (**EV-073**). The outbound delivery row itself reads **In Process**, so we do not assert that the entire delivery-to-billing process has completed.
- **Not independently verified:** Inventory/stock balance, material movement type and subsequent billing.

## Cause, prevention and closure

**Cause:** Picked quantity below required delivery quantity. **System protection:** PGI rejection was appropriate, not defective behavior. **Preventive recommendation:** Warehouse reconciliation between physical picks, delivery quantity and SAP before PGI; never increase picked quantity without confirming real goods.

| Test | Actual evidence | Status |
|---|---|---|
| Negative PGI with 1/2 PC | VLMOVE 030 | Executed — expected rejection |
| Correction to 2/2 PC | Original workshop correction and save | Executed; screenshot of corrected picker field absent |
| PGI retest | Material document 4900001491 and completed GI | Executed — passed |
| Follow-up picking request | 2 PC Completed; GI Complete | Executed — passed |
| Stock reconciliation/billing | No direct evidence | Not verified |

**Closure:** Picking discrepancy resolved for this delivery; broader shipment/billing completion not claimed. Detailed analysis: [RCA-SD-002](RCA-SD-002-Picking.md).

## Investigation standard

- **Training context:** These are training-sandbox observations, not customer production incidents. Impact, severity, roles, and communications are scenarios unless a system effect was actually observed.
- **Evidence standard:** A screenshot of successful status alone does not prove how a prior failure was corrected. Where a previous module documented the negative test and correction, both are linked. No unexecuted action is described as complete.
