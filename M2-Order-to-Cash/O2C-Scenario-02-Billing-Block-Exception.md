# M2 — O2C Process Trace 02: Delivery-Related Billing with Header Billing Block

**Scenario ID:** O2C-SD-002  
**Execution classification:** Executed in SAP training sandbox; **negative blocking test FAILED**  
**SAP system/client:** JV2 / 100 — SAP S/4HANA Cloud Public Edition sandbox  
**Requirement:** R02  
**Overall outcome:** **PASS** for second complete O2C chain; **FAIL/OPEN** for expected billing-block enforcement (separate test verdict).

## 1. Business scenario

Re-use M1 sales order **1056**, which already has corrected price **EUR 17.55**. Set **header billing block 04 — Check Payment Terms** to create a controlled variation. Process a standard delivery and PGI, then test whether the block prevents F2 invoicing of delivery **80000785**.

**Observed:** VF01 still allowed delivery-related invoice **90000304** and FI posting **9400000058**. The header block remained on the order in VA03 after invoicing. This is an observed control exception; root configuration cause is **not established**. Investigate in M3, without making up a fix.

## 2. Organizational and master data

| Field | Verified value |
|---|---|
| Company code | 1010 — DE Company Code |
| Sales area | 1010 / 10 / 00 |
| Customer/ship-to | 1000193 — NPS Test Chemical GmbH |
| FI customer master | Company code 1010 established in Scenario 1, reconciliation 12100000, NT30 |
| Material / item category | TG11 / TAN |
| Plant / storage location | 1010 / 101A (existing stock setup; storage location from Scenario 1) |
| Shipping point | 1010 — DE Shipping Point Standard |
| Currency | EUR |

## 3. Sales order and pricing

| Field | Actual |
|---|---|
| Order | 1056, type OR |
| Customer reference | REF TT0234 (as shown in VA03) |
| Quantity and net value | 1 PC, EUR 17.55 |
| Pricing condition | PPR0, restored to EUR 17.55 during M1 |
| Item category | TAN |
| Confirmed quantity | 1 PC, schedule line category CP |
| Schedule-line delivery block | Blank |
| **Header billing block** | **04 — Check Payment Terms**, saved in VA02, still displayed after billing |
| Credit check | Not independently verified |

**Evidence:** [EV-027 — block selected](evidence/m2-sc2-order-billing-block.png), [EV-028 — confirmed schedule line](evidence/m2-sc2-atp-confirmed.png), [EV-034 — block still displayed](evidence/m2-sc2-header-block-retained.png), [EV-035 — final status with block](evidence/m2-sc2-final-status-with-block.png).

## 4. Outbound delivery, picking and PGI

| Step | Actual / qualification |
|---|---|
| VL01N selection | Shipping point 1010; order 1056 |
| Delivery created | 80000785, 1 PC TG11 |
| Delivery type | Not captured; cannot claim LF was verified |
| Picking | 1 PC; user confirmed **Fully Picked** |
| PGI | Successful, material document 4900001489 |
| Goods movement status | Complete in document flow and final VA03 overview |
| Movement type | Not captured |
| Stock before/after | Not captured |

**Evidence:** [EV-029 — delivery creation overview](evidence/m2-sc2-delivery-draft.png), [EV-030 — PGI document chain](evidence/m2-sc2-pgi-document-flow.png), [EV-035 — final order status](evidence/m2-sc2-final-status-with-block.png).

## 5. Controlled billing-block negative test

**Precondition:** Header billing block 04 saved on order 1056 before delivery/PGI.

**Hypothesis / expected outcome:** F2 delivery-related invoice creation is prevented while block 04 is active.

**Observed execution:**

1. Delivery 80000785 and PGI 4900001489 were created successfully.
2. VF01 with reference to delivery 80000785 reached F2 invoice overview with 1 PC TG11, net EUR 17.55 and tax EUR 3.33.
3. The deliberate negative test continued to Save; SAP returned `Document 90000304 has been saved.`
4. FI journal 9400000058 was created and posted.
5. VA03 continued to show **Billing Block 04 — Check Payment Terms**, while delivery and billing were **Fully Delivered / Fully Invoiced**.

**Verdict:** **FAIL** — the anticipated prohibition was not enforced in this observed path. It is **not** a successful billing-block test. The observed facts do not by themselves establish whether configuration, delivery-level propagation or a billing-type assignment explains the behavior.

**Evidence:** [EV-031 — VF01 draft](evidence/m2-sc2-billing-f2-preview.png), [EV-032 — invoice/FI document flow](evidence/m2-sc2-invoice-fi-document-flow.png), [EV-034 — block retained](evidence/m2-sc2-header-block-retained.png), [EV-035 — final status](evidence/m2-sc2-final-status-with-block.png).

## 6. Billing and accounting (F2 / FI RV)

| Field | Verified result |
|---|---|
| Invoice | 90000304, F2 |
| Billed quantity | 1 PC |
| Net / output tax / gross | EUR 17.55 / EUR 3.33 / EUR 20.88 |
| FI journal | 9400000058, type RV (billing document transfer) |
| Company code | 1010 |
| FI tax code | A1 — Output Tax Domestic (Full Tax Rate), 19% |
| AR clearing | Not Cleared |

| FI account | Debit (EUR) | Credit (EUR) |
|---|---:|---:|
| 12100000 — Receivables Domestic | 20.88 | 0.00 |
| 41000000 — Revenue Domestic Products | 0.00 | 17.55 |
| 22000000 — Output Tax (MWS) | 0.00 | 3.33 |
| **Total** | **20.88** | **20.88** |

Additional entries **7100000727** and **7000000124** appeared in the order's document flow with status Cleared. Their accounting nature was **not investigated**; do not describe them as specific movements without supporting evidence.

**Evidence:** [EV-032 — invoice and FI flow](evidence/m2-sc2-invoice-fi-document-flow.png), [EV-033 — balanced journal ledger](evidence/m2-sc2-fi-ledger-redacted.png).

## 7. End-to-end document flow

| Step | Document | Verified result |
|---|---|---|
| Sales order | 1056 | Completed |
| Outbound delivery | 80000785 | Completed |
| Picking | Item 10, 1 PC | Fully Picked (reported); picking request in document flow |
| PGI material document | 4900001489 | Complete |
| Billing document | 90000304 | Completed despite header block |
| FI journal | 9400000058 | Posted, balanced, not cleared |

**Ordered / delivered / billed:** 1 / 1 / 1 PC, with 0 PC open at order item level in final VA03 overview.

## 8. Test and control checklist

| Control / test | Actual | Verdict |
|---|---|---|
| Sales order price | PPR0 EUR 17.55 | PASS |
| ATP / confirmed quantity | 1 PC schedule line CP | PASS |
| Delivery creation | 80000785 | PASS |
| Picking and PGI | Fully Picked; material document 4900001489 | PASS |
| Header billing block is present | Code 04 persisted after invoicing | PASS (presence confirmed) |
| Billing block prevents F2 delivery billing | F2 invoice 90000304 was created | **FAIL** |
| Invoice/quantity/tax | 1 PC, EUR 17.55 + EUR 3.33 | PASS |
| FI posting and journal balance | 9400000058; debit = credit = EUR 20.88 | PASS |
| Delivery type/movement type, stock before/after | Not captured | NOT VERIFIED |

## 9. Cross-functional assessment and next investigation

- **Sales:** Header billing block 04 was saved, yet Sales Order 1056 reached Completed/Fully Invoiced.
- **Logistics:** The order had 1 PC ATP confirmation and no schedule-line delivery block, so delivery and goods issue proceeded.
- **Finance:** Billing and FI postings were successful; no payment/clearing completed.
- **Risk / control:** A user may assume a sales-order billing block prevents all invoice creation routes when the tested route demonstrably did not.
- **M3 handoff:** Read-only inspect billing block 04 enforcement / billing type F2 and header/item/delivery block behavior; recreate a **new** controlled negative test if necessary. Do not change shared configuration without approval or fabricate a root cause.

## 10. Final result and evidence limitations

**O2C chain: PASS.** **Billing-block control: FAIL / OPEN**. Neither result cancels the other. No claim of successful billing-block remediation, FI clearing, movement type 601 inspection, stock-balance reconciliation or production client impact is made.

See [M2 Evidence Register](../00-Project-Tracking/Evidence-Register.md) for EV-027–EV-035.
