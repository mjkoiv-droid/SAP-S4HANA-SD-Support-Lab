# M3-INC-002 — Partial picking blocks post goods issue

| Field | Result |
|---|---|
| System | SAP S/4HANA Cloud Public Edition, JV2 / 100 training |
| Sales order | **1059**, TG11, 2 PC, net EUR 35.10 |
| Outbound delivery | **80000788**, plant 1010, storage location 101A |
| Intended negative-test defect | Delivery 2 PC, **picked only 1 PC** |
| Actual picking status | **B — Partially Picked** before save |
| Failure | PGI rejected with **VLMOVE 030** |
| SAP message | `Delivery has not yet been picked (completely)` |
| Correction | Picked quantity updated to 2 PC, saved |
| Positive retest | PGI successful; material document **4900001491** created |
| Independent verification | Sales-order document flow shows material document 4900001491 **Complete** |
| Status | **Resolved / PASS** |

## Executed negative / positive test

| Stage | What was done | Actual SAP evidence | Outcome |
|---|---|---|---|
| Initial state | Create order 1059, 2 PC TG11 | [EV-045](evidence/m3-order1059-2pc-redacted.png) | Saved |
| Defect introduction | Open delivery creation, pick 1 of 2 | [EV-046](evidence/m3-picking-half-delivery.png) | Status B — Partially Picked |
| Negative test | Save delivery 80000788 and attempt PGI | [EV-047](evidence/m3-pgi-error-vlmove030.png) | **FAIL posting as intended**, VLMOVE 030 |
| Corrective action | In VL02N change picked quantity 1 → 2 PC and save | Save success reported in workshop | Saved; no separate corrected status screenshot |
| Positive retest | Reattempt PGI | `Outbound Delivery 80000788 saved, material document 4900001491 created` (user-reported SAP message) | **PASS** |
| Verification | Review document flow | [EV-048](evidence/m3-pgi-post-correction-document-flow.png) | GI document Complete |

## Root cause, impact and prevention

**Root cause:** Partial picking quantity (1 PC) did not satisfy full delivery quantity (2 PC). **Business impact:** Shipping/PGI processing delayed until physically/logically picked quantity is aligned. **Control:** VLMOVE 030 correctly prevents goods issue of incompletely picked delivery in this tested process. **Corrective action:** Complete picking, save, repeat PGI. **Risk:** For a real shipment, validate physical pick/stock movement before adjusting SAP, and never falsify picked quantity.

**Further evidence:** Delivery incompletion list empty [EV-049](evidence/m3-delivery-incompletion-blank.png); order 1059 complete [EV-050](evidence/m3-sales-order-complete-message.png). No invoice was created for delivery 80000788 as part of this M3 incident. Movement type, before/after stock and billing/AR status were not verified. This is not represented as a full O2C chain.
