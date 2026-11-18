# Intercompany Billing-to-FI INVOIC — Configuration Trace

**System:** SAP S/4HANA practice system T41, client 400  
**Method:** Verified read-only SAP GUI and Fiori inspection  
**Result:** End-to-end integration settings observed; no new invoice IDoc execution or FI posting verified.

## Intended integration flow

`IV` intercompany billing → `OPD` output `S4680_BILLING_DOCUMENT` → `IDOC` channel → `INVOIC` outbound partner `KU / C680-90FR` → transactional RFC port `A000000003` → inbound partner `LI / S680-1010` / `INVF` → FI supplier invoice in company code `90FR`.

This is a *configuration-supported intended flow*. It is **not** a claim that all transitions were actually exercised.

## Observed configuration checkpoints

| Area / application | Observed configuration | Evidence |
|---|---|---|
| BP / supplier master | BP `S680-1010`; `FLVN00` FI Vendor and `FLVN01` Supplier roles; company `90FR`; reconciliation account `21200000`; payment terms `0002`; posting block `No` | [Company codes](evidence/bp-company-code.png) |
| `VV33` | `RD04` record for sales organization `1010`, customer `C680-90FR`, medium `6` (EDI), dispatch `4` | [Condition record](evidence/invoice-output-condition.png) |
| `OPD`, Output Type | Billing type `IV` → `S4680_BILLING_DOCUMENT`; dispatch `1` (Immediately) | [Output type rule](evidence/opd-output-type.png) |
| `OPD`, Channel | `S4680_BILLING_DOCUMENT` → `IDOC` | [Channel rule](evidence/opd-channel.png) |
| `WE41` | Outbound process code `SD08` — Intercompany Billing; function module `IDOC_OUTPUT_INVOIC_IV_MM` | [Process code](evidence/outbound-process-code.png) |
| `WE20`, outbound | Partner `C680-90FR` (`KU`), role `BP`, message `INVOIC`, code `FI`, port `A000000003` (tRFC), basic type `INVOIC01`, pass immediately | [Outbound parameters](evidence/outbound-partner-parameters.png) |
| `WE20`, Message Control | Application `V3`, output type `RD00`, process code `SD08` | [Message control](evidence/outbound-message-control.png) |
| `WE20`, inbound | Partner `S680-1010` (`LI`), message `INVOIC`/code `FI`, process code `INVF`, trigger immediately, cancel after syntax error | [Inbound parameters](evidence/inbound-partner-parameters.png) |
| Intercompany billing IMG | Billing type `IV`: `AAIB` (account assignment) selected | UI inspection, reported and verified by operator |
| `WEL1` | Application `V3`, logical address `1010C680-90FR` → company `90FR`, supplier `S680-1010` | [Supplier assignment](evidence/supplier-assignment.png) |
| MM EDI tax conversion | `LI / S680-1010`, tax type `10`; mapping to internal tax code `1I` shown | [Tax conversion](evidence/tax-code-mapping.png) |
| MM EDI program parameters | `LI / S680-1010 / 90FR`, supplier invoice type `KR`, credit memo type `KG` | [Invoice parameters](evidence/invoice-program-parameters.png) |
| `OBCB`, FI-EDI G/L accounts | `LI / S680-1010 / 90FR`, goods/services `*` → G/L `51600000` | [G/L account mapping](evidence/fi-edi-gl-accounts.png) |
| `OBCE`, EDI invoice parameters | G/L debit `40`, G/L credit `50`, vendor debit `21`, vendor credit `31`, invoice `KR`, credit memo `KG`, tax code `1I` | [Posting parameters](evidence/fi-edi-program-parameters.png) |

The `VV33` / `RD04` entry is a legacy condition record present in the training system. The actual inspected `OPD` rules independently show the `IDOC` channel for the `S4680_BILLING_DOCUMENT` output type. Do not equate the existence of these settings with actual delivery or posting.

## Transaction / reconciliation result

- `FB03` document-list search in company code `90FR`, document type `KR`, **Own documents only** checked: **No corresponding items exist**.
- With own-document filtering removed, existing `KR` entries appeared in other company codes (`1010`, `1710`, `TA98`), not `90FR`.
- Evidence: [no matching own KR documents in 90FR](evidence/fb03-company-90fr-no-kr-result.png) and [KR entries limited to other company codes, cropped to hide document dates](evidence/fb03-other-company-kr-documents-crop.png).

**No existing target `90FR` invoice was verified and no new invoice or INVOIC IDoc was created**. No FI posting, document amount reconciliation or end-to-end recovery claim is made.

## Error-analysis relevance

For a real incoming-invoice error, support should correlate `INVOIC` message/control data to the matching sender `KU` and receiver `LI` partners, output condition, port, `INVF` process, supplier mapping, tax conversion, `OBCB` G/L mapping, and `OBCE` document/posting keys. `WLF_IDOC` can be used for analysis where that workflow is available. Actual message diagnostics must precede any proposed correction.
