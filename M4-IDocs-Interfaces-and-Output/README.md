# M4 — IDocs, Interfaces, Application Logs and Output

**Module outcome:** Completed as an evidence-backed SAP interface and output investigation. Live configuration inspection, historical IDoc error diagnosis and positive sales-order output are verified. A controlled IDoc correction/reprocessing cycle was **not performed**; the recovery procedure is explicitly a documented simulation, not a successful SAP retest.

## SAP environments and scope

- **T41 / client 400 (SAP S/4HANA practice system):** SAP GUI transaction monitoring and configuration inspection (`WE02`, `WE20`, `WE21`, `WE41`, `WEL1`, `VV33`, `OPD`, `OBCB`, `OBCE`, `FB03`), plus output processing of sales order `374`.
- **Integration subjects:** SD-to-FI intercompany `INVOIC` configuration, outbound sales-order output, pre-existing IDoc error classification and application-log investigation.
- **Evidence boundary:** Historical IDocs are background diagnostics, not defects deliberately created for this exercise. No shared IDoc was reprocessed; no new `INVOIC` IDoc or related FI invoice in company code `90FR` was verified.

## M4 deliverables

| Deliverable | Record | Status |
|---|---|---|
| IDoc diagnostic record | [IDoc-Diagnostic-Record](IDoc-Diagnostic-Record.md) | Completed — historical error analyzed, not corrected |
| Interface configuration and tracing | [Intercompany-INVOIC-Configuration-Trace](Intercompany-INVOIC-Configuration-Trace.md) | Completed — inspected configuration, processing not proven |
| Output monitoring checklist | [Output-Monitoring-Checklist](Output-Monitoring-Checklist.md) | Completed — positive order output confirmed |
| Recovery and escalation runbook | [Interface-Recovery-Runbook](Interface-Recovery-Runbook.md) | Completed as documented operating procedure; no executed recovery |
| Reusable blank case template | [IDoc-Diagnostic-Template](IDoc-Diagnostic-Template.md) | Template only |

## Main observed results

- An existing inbound `DELFOR` IDoc `180016` had status `56` — **“EDI: Inbound partner profile does not exist”**. Its IDoc structure, control information and status record were examined. This is real diagnostic evidence, not a newly induced failure. [Error evidence](evidence/idoc-inbound-delfor-partner-profile-error.png).
- The `INVOIC` intercompany interface has an `IV` billing rule producing output type `S4680_BILLING_DOCUMENT` via channel `IDOC`; outbound partner `C680-90FR` (`KU`) and inbound supplier `S680-1010` (`LI`) are configured as detailed in the [interface trace](Intercompany-INVOIC-Configuration-Trace.md).
- Sales order `374`, customer reference `M4-OUTPUT-001`, contains **two completed** order-confirmation outputs. Verified channel `PRINT`, form `SD_SLS_ORDER_CONFIRM`, queue `LP01`. [Output overview](evidence/sales-order-374-output-completed.png).
- In `FB03`, searching company code `90FR` for `KR` accounting documents returned no matching result with own-document filtering, and the broader available result set contained `KR` documents in other company codes, not `90FR`. Therefore automatic intercompany FI posting was **not** verified; no substitute historical invoice was modified. [No-match screen](evidence/fb03-company-90fr-no-kr-result.png).

## Validation boundary

This module demonstrates actual monitoring, diagnosis, cross-module settings and output verification. It does **not** establish a successful `INVOIC` posting, a tested partner-profile repair or an end-to-end failed → fixed → reprocessed IDoc. Those outcomes remain unverified.

Supporting screenshots are SAP training-system records presented for illustration in the **public-facing independent portfolio**; see the [author review and attribution](../PORTFOLIO-VALIDATION.md).
