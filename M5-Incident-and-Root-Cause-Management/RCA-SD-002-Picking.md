# RCA-SD-002 — Picking quantity mismatch and PGI rejection

| Field | Result |
|---|---|
| Related incident | [INC-SD-002](Incident-INC-SD-002-Picking.md) |
| Context | JV2 / 100; order `1059`, delivery `80000788`, TG11 2 PC |
| Outcome | **Confirmed negative-test cause and corrected PGI; wider shipment scope unverified** |
| Evidence | EV-045–EV-050, EV-073 |

## Executive conclusion

The 2 PC delivery was deliberately left with 1 PC picked. Picking status **B — Partially Picked** and the attempted goods issue produced **VLMOVE 030 — Delivery has not yet been picked (completely)**. The operator then aligned the picked quantity to 2 PC and retried PGI. Material document **4900001491** was created. Independent follow-up shows the picking request **2 PC Completed** and goods issue **Complete**.

**Key diagnostic distinction:** SAP behaved correctly by stopping PGI while picking was incomplete. This was a controlled warehouse process mismatch, **not a defect in the SAP goods-issue program**.

## Hypothesis tests

| Hypothesis | Test/finding | Conclusion |
|---|---|---|
| Picked quantity less than delivery quantity | Delivery 2 PC; picked 1 PC and status B, EV-046 | Confirmed |
| Delivery blocked by incompletion | Later delivery incompletion list empty, EV-049 | Not supported for recorded failure |
| Inventory shortage caused the exception | No inventory before/after or availability error recorded | Unverified |
| Posting validation rejects partial picking | Negative PGI yielded VLMOVE 030, EV-047 | Confirmed in tested process |

### Evidence-limited 5 Whys

1. **Why was PGI rejected?** SAP issued VLMOVE 030 indicating picking was incomplete.
2. **Why was the delivery incomplete for PGI?** Only 1 of 2 PC was picked.
3. **Why was just 1 PC picked?** The operator deliberately left a partial pick for the lab scenario.
4. **Why was this not automatically resolved?** PGI requires a consistent delivery/picking state; no automated completion process was investigated.
5. **Why would a real operation encounter this mismatch?** **Not established in this training test.** No warehouse procedure, physical stock check or user-error record exists; avoid inventing a broader operational root cause.

## Correction and validation

| Action | Actual outcome | Status |
|---|---|---|
| Maintain initial 1/2 PC picked and attempt PGI | Expected VLMOVE 030 failure | Executed |
| Adjust picked quantity to 2/2 PC | Saved, original workshop confirmation | Executed, save screenshot not separately archived |
| Repeat PGI | Material doc 4900001491 created; GI Complete (EV-048) | Executed — passed |
| Reinspect picking | Picking request 2 PC Completed; GI Complete (EV-073) | Executed — passed |
| Reconcile physical stock quantities | No inventory count or stock movement-type audit | Not verified |
| Complete billing and FI for 1059 | No billing evidence in this case | Not tested |

## Prevention and impact

In real operations, require a pick-versus-delivery quantity check and physical reconciliation before PGI. Never align SAP quantities solely to bypass a validation message. The observed impact in the lab was a rejected goods issue until the quantity was corrected; no actual shipment delay or cost was measured.

**RCA closure:** Specific test-case cause/correction verified. Broader warehouse, inventory and downstream completion remain outside evidence scope.
