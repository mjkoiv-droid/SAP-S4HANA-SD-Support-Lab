# M2 — O2C Process Trace 01: Standard Stock Sale and FI Master-Data Correction

**Scenario ID:** O2C-SD-001  
**Execution classification:** Executed in SAP Learning Hub training sandbox, with explicitly noted unverified details  
**SAP system/client:** JV2 / 100 — SAP S/4HANA Cloud Public Edition sandbox  
**Execution dates:** Sales order created 16 November 2026; PGI, billing and FI recorded 17 November 2026  
**Requirement:** R02  
**Overall outcome:** **PASS** for sales order → picking → PGI → invoice → FI posting. Customer receipt/clearing not executed.

## 1. Business scenario

Fulfil one standard domestic sale for NPS Test Chemical GmbH. This order originated in the M1 controlled delivery-block lab; the block was removed and outbound delivery 80000784 had already been created. M2 resumed from that delivery to complete picking, post goods issue, billing and Financial Accounting verification.

A genuine SD–FI exception occurred: billing document 90000303 was saved without an accounting document because the customer lacked company-code data for 1010. The missing data was created and the invoice subsequently posted to FI.

## 2. Organizational and master data

| Field | Verified value / qualification |
|---|---|
| System/client | JV2 / 100 (previously documented sandbox context) |
| Company code | 1010 — DE Company Code (billing and journal entry) |
| Sales organization / distribution channel / division | 1010 / 10 / 00 (M1 sales order and billing context) |
| Customer / sold-to and ship-to | 1000193 — NPS Test Chemical GmbH |
| Customer company-code setup | Initially absent; subsequently added for 1010 |
| Customer reconciliation account | 12100000 — Receivables Domestic |
| Customer payment terms | NT30 — Net Due in 30 Days |
| Material / item category | TG11 — Trad.Good 11, PD, Reg.Trading / TAN |
| Plant / storage location | 1010 / 101A |
| Shipping point | 1010 — DE Shipping Point Standard |
| Currency | EUR |

## 3. Sales order (VA01/VA02/VA03)

| Field | Verified result |
|---|---|
| Order | 1055, type OR |
| Customer reference | M1-TEST-001 |
| Quantity | 1 PC |
| Net unit price / net order value | PPR0 EUR 17.55 / EUR 17.55 |
| Tax on invoice | EUR 3.33 (19% rounded) |
| Requested delivery date | 31 January 2027 as later displayed |
| Availability / confirmed quantity | Order successfully created delivery for 1 PC; exact schedule-line confirmation screenshot for order 1055 not retained in M2 |
| Original M1 delivery block | Political Reasons, deliberately tested and removed in M1 |
| Credit status | Not independently checked; delivery header earlier reported credit check not performed |
| Document flow | Order 1055 → delivery 80000784 |

**M1 prerequisite evidence:** [M1 delivery-block verification](../M1-Landscape-and-Monitoring/README.md), including EV-009–EV-013.

## 4. Outbound delivery and picking (VL02N)

| Field | Verified result |
|---|---|
| Delivery | 80000784 |
| Plant/storage location | 1010 / 101A |
| Delivered quantity | 1 PC TG11, item 10 |
| Picking quantity | 1 PC |
| Picking status | C — Fully Picked; save confirmation reported |
| Delivery type | Not captured (do not infer from standard workflow) |
| Before/after inventory totals | Not captured; stock depletion is expected, not separately verified |

**Evidence:** [EV-017 — picking quantity/status](evidence/m2-sc1-picking-fully-picked.png).

## 5. Post Goods Issue (VL02N)

| Field | Verified result |
|---|---|
| PGI outcome | Success message: delivery saved, material document created |
| Material document | 4900001488 |
| Reference delivery | 80000784 item 10 |
| Material / quantity | TG11 / 1 PC |
| Reference value in material document viewer | EUR 13.50 |
| Movement type | Not shown in captured views; 601 must not be asserted as verified |
| Plant / stock before and after | Plant 1010 previously confirmed; stock before/after not measured |
| PGI status | Complete in document flow |

**Evidence:** [EV-018 — document flow](evidence/m2-sc1-pgi-document-flow.png), [EV-019 — goods issue detail](evidence/m2-sc1-material-document.png).

## 6. Billing (VF01 / Manage Billing Documents)

| Field | Verified result |
|---|---|
| Billing document | 90000303 |
| Billing type | F2 — Invoice |
| Invoice date | 17 November 2026 |
| Billed quantity | 1 PC |
| Net / output tax / gross | EUR 17.55 / EUR 3.33 / EUR 20.88 |
| Initial result | Saved with no journal entry; status To Be Posted / Error in Accounting Interface |
| SAP posting error | `Document 90000303: Customer 1000193 is not defined in company code 1010` |
| Corrective action | Create the missing customer company-code 1010 data (reconciliation account 12100000; NT30) and save master data |
| Retest | Invoice subsequently showed Completed and FI journal entry created |

**Evidence:** [EV-020 — billing preview](evidence/m2-sc1-billing-f2-preview.png), [EV-021 — FI interface error](evidence/m2-sc1-fi-interface-error.png), [EV-022 — exact error](evidence/m2-sc1-fi-master-error.png), [EV-023 — missing company code](evidence/m2-sc1-customer-company-code-missing.png), [EV-024 — entered master data](evidence/m2-sc1-customer-company-code-draft.png). **EV-024 displays a draft, not independently the successful Save message; the subsequently created FI journal is the decisive end-to-end retest.**

## 7. FI accounting verification

| Entry | Account | Debit (EUR) | Credit (EUR) |
|---|---|---:|---:|
| Receivable | 12100000 — Receivables Domestic | 20.88 | 0.00 |
| Domestic product revenue | 41000000 — Revenue Domestic Products | 0.00 | 17.55 |
| Output tax | 22000000 — Output Tax | 0.00 | 3.33 |
| **Total** | | **20.88** | **20.88** |

**Journal entry:** 9400000057; type **RV** (billing document transfer); posting date **17 November 2026**; company code **1010**; transaction currency **EUR**. Invoice clearing remains **Not Cleared**; payment was not processed.

**Evidence:** [EV-025 — billing→FI document chain](evidence/m2-sc1-billing-fi-success.png), [EV-026 — actual balanced FI lines](evidence/m2-sc1-fi-ledger-redacted.png).

## 8. Complete O2C document flow

| Step | SAP document | Observed outcome |
|---|---|---|
| Sales order | 1055 | Completed |
| Outbound delivery | 80000784 | Shipped after PGI |
| Picking | Item 10, 1 PC | Fully Picked |
| Goods issue | 4900001488 | Complete |
| Billing | 90000303 | Completed after master-data correction |
| FI journal | 9400000057 | Posted, balanced; receivable not cleared |

**Ordered / delivered / billed:** **1 / 1 / 1 PC**, supported by order/delivery/billing screens and document-flow references. Customer receipt/payment not performed.

## 9. Exception: FI customer master-data gap

**Symptom:** Billing saved; no FI journal entry.  
**Reproduction:** Attempted invoice posting, received explicit missing-company-code error.  
**Diagnosis:** Business partner 1000193 had no entries on Company Codes tab for 1010.  
**Correction:** Added customer company-code 1010, reconciliation account 12100000 and terms NT30.  
**Retest:** Invoice 90000303 posted successfully; journal 9400000057 created and validated.  
**Status:** **Resolved in sandbox**. No assertion about production incidents.

## 10. Test and process control checklist

| Control | Result | Status |
|---|---|---|
| Valid customer/material/order price | TG11, 1 PC, EUR 17.55 | PASS |
| Picking matches delivery | 1 PC / 1 PC; status C | PASS |
| PGI produces material document | 4900001488 | PASS |
| Independent stock before/after reconciliation | Not captured | NOT VERIFIED |
| Invoice quantity matches delivery | 1 PC / 1 PC | PASS |
| FI document created and balanced | 9400000057; 20.88 debit = 20.88 credit | PASS |
| Customer open receivable | Not cleared | OBSERVED (not payment processing) |
| Movement type, delivery type, credit check | Not independently recorded | NOT VERIFIED |

## 11. Sales → Logistics → Finance assessment

- **Sales:** Correct pricing and standard TAN item, but customer accounting extension had not been maintained when the sales order was created.
- **Logistics:** Picking and PGI completed; SAP created the goods-issue material document.
- **Finance:** Billing transfer initially failed because the customer had no company-code data. The correction enabled a balanced receivable/revenue/tax posting.
- **Control improvement:** Check FI customer company-code view and reconciliation account during customer onboarding, rather than discovering the omission only after billing.

## 12. Final result and evidence limitations

**PASS:** Full training-system sales order → delivery → picking → PGI → billing → FI journal chain, with resolved real SAP accounting-interface error. **Not performed:** customer payment, cash application, AR clearing, movement-type inspection, inventory balance before/after and transport/configuration changes.

See [M2 Evidence Register](../00-Project-Tracking/Evidence-Register.md) for EV-017–EV-026.
