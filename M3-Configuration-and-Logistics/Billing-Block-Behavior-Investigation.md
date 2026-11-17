# CFG-ISS-001 — Billing block 04 did not stop F2 delivery-related invoicing

**State:** Reproduced in two actual sandbox scenarios, **unresolved configuration cause**; CBC access Unauthorized. This is an investigation, **not** a successfully validated billing-block control.

## Case A — Sales-order header billing block

- VA02 saved header **04 — Check Payment Terms** on order **1056**.
- VA03 final status still showed block 04 while order 1056 was fully delivered, GI complete and fully invoiced — [EV-051](evidence/m3-order1056-billing-block-final-status.png).
- Order item 10 had a **blank** billing block — [EV-037](evidence/m3-order1056-item-no-billing-block.png).
- Delivery **80000785** had a **blank** delivery header block — [EV-036](evidence/m3-order1056-delivery-no-billing-block.png).
- Delivery-related invoice **90000304** was created; FI journal **9400000058** posted and balanced (M2 EV-031–EV-035).

## Case B — Delivery header billing block

- New sales order **1058**, delivery **80000787** were created.
- In VL02N delivery header financial processing, **04 — Check Payment Terms** was selected, then saved; the user later independently confirmed that the block remained on delivery 80000787. Screenshot [EV-038](evidence/m3-delivery80000787-billing-block.png) captures the selection before saving; the confirmation after saving is in the conversation and was not separately captured.
- Picking and PGI were performed; material document **4900001490** shows GI **Complete** in document flow — [EV-039](evidence/m3-delivery80000787-post-goods-issue.png).
- VF01 then saved delivery-related **F2 invoice 90000305**. Manage Billing Documents showed **Completed**, Accounting Data showed **Journal entry has been created**. **FI journal number and ledger lines for this invoice were not captured.** [EV-052](evidence/m3-billing90000305-item-values.png) shows invoice item data, not posting proof.

## What is and is not established

| Question | Status |
|---|---|
| Did block 04 remain on order 1056? | **Yes**, screenshot |
| Was order item billing block blank? | **Yes**, screenshot |
| Was delivery 80000785 header block blank? | **Yes**, screenshot |
| Did order header block prevent F2 delivery-related billing? | **No** in this tested path |
| Was delivery 80000787 header block selected and saved? | **Yes** based on screenshot + user confirmation |
| Did delivery block prevent billing in the tested flow? | **No** in this tested path |
| Is block 04 assigned to F2 under config 102401? | **Unknown**; CBC Unauthorized |
| Do copy-control requirements explain observed behavior? | **Unknown**; customizing unavailable |
| Do header vs item vs delivery blocks have globally defined enforcement semantics in this tenant? | **Not established** |

## Diagnostic pointers and next steps, without access

- SAP KBA [2991828](https://userapps.support.sap.com/sap/support/knowledge/en/2991828) documents a similar billing-success-despite-block symptom.
- SAP KBA [3147488](https://userapps.support.sap.com/sap/support/knowledge/en/3147488) points to configuration activity **102401 — Assign Blocking Reasons to Billing Types**.
- SAP KBA [3579778](https://userapps.support.sap.com/sap/support/knowledge/en/3579778) highlights that even maintained assignments may not always appear as expected in billing application list behavior. Consequently, **missing 102401 assignment is a hypothesis, not a confirmed root cause**.
- Manage Your Solution explicitly indicated configuration was CBC-managed — [EV-040](evidence/m3-cbc-tenant-managed.png). The user reported an **Unauthorized** response opening CBC.

**Proposed follow-up:** Authorized CBC specialist review of 102401, block 04 definition, delivery-related F2 billing requirements and due-list behavior; approve design and retest in dedicated sandbox before claiming resolution. See [CHG-M3-001](Change-Proposal-CHG-M3-001.md).
