# CFG-SD-001 — Configuration and SD/MM/FI Dependency Analysis

| Field | Value |
|---|---|
| Analysis ID | CFG-SD-001 |
| Module / original requirement | M3.01–M3.02, R07 / R10 |
| Environment | SAP S/4HANA Cloud Public Edition; training system JV2 / client 100 (as recorded in M1 inventory) |
| Analysis date | 17 November 2026 |
| Execution | Read-only SAP observations plus previously completed controlled transactions; **no customizing performed** |
| Status | Partially completed / CBC inspection blocked |

## 1. Actual organizational and master-data scope

| Object | Observed value | Verification |
|---|---|---|
| Company code | 1010 — DE Company Code | M2 invoice/journal EV-025, EV-026, EV-033 |
| Sales organization | 1010 — DE Sales Org. | Sales order / pricing context (EV-042) |
| Distribution channel | 10 | PPR0 variable key (EV-042) |
| Division | 00 | M2 order and invoice evidence (EV-034) |
| Plant | 1010 — DE Plant 1 | [EV-043](evidence/m3-order1058-shipping.png) |
| Shipping condition | 01 — Standard | M1 [EV-012](../M1-Landscape-and-Monitoring/evidence/delivery-shipping-point.png) and M2 delivery details |
| Loading group | Crane (description; technical key not displayed) | [EV-044](evidence/m3-material-tg11-loading-group.png) |
| Determined shipping point | 1010 — DE Shipping Point Standard | [EV-043](evidence/m3-order1058-shipping.png) |
| Material | TG11 — Trad.Good 11, PD, Reg.Trading | EV-042–EV-044 |
| Product availability check | Stock and Rel. Rec. (SR) | [EV-044](evidence/m3-material-tg11-loading-group.png) |
| Customer | 1000193 — NPS Test Chemical GmbH | EV-043, M2 |

**Determination limitation:** The inputs and resulting shipping point were verified across compatible material/customer/sales-area transaction observations, not in one customizing mapping view. The actual shipping-point determination mapping in customizing was **not** opened; do not represent this as a configuration-table verification.

## 2. Sales document, item and schedule-line behavior

| Area | Observed behavior | Customizing verification |
|---|---|---|
| Sales order | Standard Order OR, order 1058 / 1059 | Document type used successfully; VOV8 not inspected |
| Item category | TAN — Standard Item | EV-043 and order 1059; VOV7/VOV4 not inspected |
| Schedule line | CP — MRP, 1 PC confirmed on order 1056 | M2 executed screenshot; VOV5/VOV6 not inspected |
| Delivery | Outbound delivery 80000787; 80000788 | Delivery type and item-category customizing not independently inspected |
| Picking | Partial: B; full: corrected saved | [EV-046](evidence/m3-picking-half-delivery.png), [EV-047](evidence/m3-pgi-error-vlmove030.png), [EV-048](evidence/m3-pgi-post-correction-document-flow.png) |
| Copy control | OR sales order → delivery → F2 invoice successfully executed | **Inferred functioning path**, not VTLA/VTFL configuration inspection |
| GI movement type | Material documents 4900001490 and 4900001491 created | Movement type not independently confirmed |

## 3. Pricing condition technique

| Parameter | Observed value |
|---|---|
| Pricing procedure | Y10101 — Materials (Germany), observed in order 1056 pricing analysis (M1 EV-015) |
| Price condition | PPR0 |
| Condition key | Sales org 1010 / distribution channel 10 / material TG11 |
| Condition record | EUR 17.55 per 1 PC, scale starting at 0 |
| Validity | 07 September 2023 to 31 December 9999 |
| Tax pricing in order | TTX1 19%, EUR 3.33 |
| Internal price condition | PCIP EUR 13.50 |
| Gross/net price | EUR 17.55; inclusive of displayed output tax EUR 20.88 |

[Price record and validity screenshot](evidence/m3-ppr0-condition-record.png) · [Order condition breakdown](evidence/m3-order1058-pricing-values.png).

**Pricing exception (actual controlled test):** Order 1056 PPR0 manually overridden from EUR 17.55 to EUR 15.55 and saved. SAP pricing analysis message **203** reported a found condition record changed manually; original EUR 17.55 was restored and verified (EV-014–EV-016). This was a **business-value discrepancy**, not a technical pricing-engine failure.

## 4. SD–FI account determination — observed postings, not customizing

For invoices 90000303 and 90000304, actual posted RV entries in company code 1010 showed:

| G/L account | Debit | Credit |
|---|---:|---:|
| 12100000 Domestic Receivables | EUR 20.88 | — |
| 41000000 Domestic Product Revenue | — | EUR 17.55 |
| 22000000 Output Tax | — | EUR 3.33 |
| Total | **EUR 20.88** | **EUR 20.88** |

Source: M2 EV-026 / EV-033. No revenue account determination configuration (VKOA or cloud equivalent) was opened, and no assumption about its key combination is made.

**M2 master-data dependency:** Invoice 90000303 initially failed FI posting because customer 1000193 was not defined for company code 1010. Company-code data was added with reconciliation account 12100000 and payment terms NT30; RV journal 9400000057 was then created. This is a master-data fix, **not an implemented customizing change**.

## 5. Billing block / copy-control exception

- Order 1056 had header billing block **04 — Check Payment Terms** and a blank item-level billing block. Delivery 80000785 had blank delivery header billing block; F2 invoice **90000304** and FI journal **9400000058** were nevertheless created.
- Separately, delivery **80000787** had delivery-header block **Check Payment Terms** entered, saved and confirmed by the user; later invoice **90000305** was saved via the billing transaction and FI posting reported created. Its billing-type field is not independently shown in the retained M3 screenshot. The journal-entry ID was **not captured**.
- Therefore block 04 **did not prevent billing in either tested transaction path**. The current assignment of block 04 to billing type F2 and detailed copy-control requirements were **not inspected**.
- SAP CBC was reported as **Unauthorized**; Manage Your Solution explicitly pointed to CBC ([EV-040](evidence/m3-cbc-tenant-managed.png)).

Read [billing-block investigation](Billing-Block-Behavior-Investigation.md) and [proposed change](Change-Proposal-CHG-M3-001.md). Official SAP KBA 2991828 describes a similar symptom; SAP KBA 3147488 points to configuration activity 102401. These are **external diagnostic pointers, not evidence of the tenant's current settings**.

## 6. Shipping and delivery exceptions

Order 1059: 2 PC TG11; delivery 80000788 2 PC with only 1 PC picked, picking status **B — Partially Picked**. PGI was rejected by **VLMOVE 030**, message “Delivery has not yet been picked (completely)”. Picked quantity corrected to 2 PC, saved; posting created material document **4900001491**, final SAP document flow marked GI **Complete** (EV-045–EV-048). The document's actual picking-status C after correction was not captured in an independent screenshot and must not be invented.

Read [picking exception record](Incident-M3-Picking-Exception.md).

## 7. Incompletion observation

- Delivery 80000788: no entries shown in incompletion list ([EV-049](evidence/m3-delivery-incompletion-blank.png)).
- Order 1059: “Document is complete” ([EV-050](evidence/m3-sales-order-complete-message.png)).
- Invoice 90000305: item values visible, but **no independent billing incompletion evaluation demonstrated** ([EV-052](evidence/m3-billing90000305-item-values.png)).

## 8. Configuration and authorization boundaries

| Configuration object | Observed in SAP? | Change status |
|---|---|---|
| VOV8 / sales order definition | No | Not changed |
| VOV4/VOV7 item category | Actual item TAN only | Not changed |
| VOV5/VOV6 schedule lines | Actual category CP only | Not changed |
| VTLA/VTFL copy control | Workflow succeeded; customizing unavailable | Not changed |
| SSCUI 102358 billing blocking reason | Actual reason 04 only; definition not inspected | Not changed |
| SSCUI 102401 billing-block-to-billing-type assignment | No — CBC denied | **Proposed verification** |
| Shipping point determination mapping | Result verified, mapping not inspected | Not changed |
| FI revenue account determination | Ledger entries observed, customizing not inspected | Not changed |

**Conclusion:** Tested pricing, shipping and picking behavior is supported by SAP evidence. Billing-block enforcement remains unresolved at configuration level. No SAP customizing changes, transports, approvals or regression verification of a future configuration change have occurred.
