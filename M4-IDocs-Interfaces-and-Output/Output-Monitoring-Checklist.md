# M4 — Output Monitoring and Verification

## Verified positive output: sales order 374

A dedicated standard sales order `374` for customer `T-C400`, with customer reference `M4-OUTPUT-001`, produced two **Completed** order-confirmation output entries visible in its SAP output overview. The detail view of the first output confirms:

| Field | Verified value |
|---|---|
| Output type | `ORDER_CONFIRMATION` |
| Receiver | `T-C400` (Sold-to Party `AG`) |
| Sales organization | `1010` |
| Channel | `PRINT` |
| Form | `SD_SLS_ORDER_CONFIRM` |
| Status | `4` — Completed |
| Print queue | `LP01` |
| Number of copies | `1` |

Evidence: [two completed outputs](evidence/sales-order-374-output-completed.png), [output detail with metadata hidden](evidence/sales-order-374-output-details.png).

This is proof of completed *sales-order print output* in the training system. It is **not** proof of an `INVOIC` IDoc, a successfully delivered physical printout, or a failed/recovered output test.

## Checkpoints for a support analyst

| Check | Actual finding / support action | Classification |
|---|---|---|
| Output existence | Two completed entries for order `374` | Verified |
| Partner / recipient | Role `AG`, customer `T-C400` | Verified |
| Channel and form | `PRINT`, `SD_SLS_ORDER_CONFIRM` | Verified |
| Print routing | Queue `LP01` | Verified |
| Processing outcome | SAP status `Completed` | Verified in SAP |
| Billing `INVOIC` channel | `OPD`: billing output via `IDOC` | Verified configuration, no IDoc posting |
| Failed output / reprocess | Inspect status details, error text and routing; retry only after authorization | Documented control, not executed |
| Duplicate/recipient validation | Verify reference, output count, partner and downstream handling before reissue | Documented control, not executed |

## Exception triage design

1. Determine which document/output type and business partner are affected.
2. Compare intended channel and output rule with actual output record. Distinguish `PRINT` sales-order output from `IDOC` billing integration.
3. Inspect processing status, failed-job/queue reason and applicable system logs.
4. If output is wrong or missing, document the specific mismatch and obtain authorization for any reprocessing or recipient/routing changes.
5. Validate the resulting output record and guard against duplicate dispatch or duplicate business posting.

**Execution boundary:** No intentionally broken print queue or negative-to-positive output retry was executed. This is a positive verification and a support checklist.
