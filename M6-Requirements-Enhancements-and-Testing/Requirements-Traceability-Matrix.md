# M6 — Requirements-to-design-to-test traceability

**Change:** CHG-SD-001 (proposed only) · **System evidence:** JV2/100 unless specified · **No implementation or post-change UAT executed**.

| Requirement | Design / control | Test(s) | Actual evidence | Validation status |
|---|---|---|---|---|
| REQ-M6-01 prevent in-scope blocked F2 | Source-level 04 eligibility; JV2 config and copy rules still unknown | TC-SD-002, 003, 004, 005 | EV-027, EV-031–EV-035, EV-038–EV-039, EV-051–EV-052, EV-083–EV-089 | **Failed against proposed control** in observed scenarios; root cause open |
| REQ-M6-02 authorized release and single billing | Approved maker/checker release, one invoice/one correct FI chain | TC-SD-008 | None | **Not executed**; no change or approved release |
| REQ-M6-03 preserve normal fulfillment | No regression for unblocked OR/TAN/TG11; PGI guard should remain | TC-SD-001, 006 | EV-017–EV-026, EV-045–EV-050 | **Historical baselines executed**, not post-change proof |
| REQ-M6-04 control unintended cross-effects | Output/interface and source/billing variants assessed | TC-SD-007, 008, 009 | EV-077–EV-078; M4 config observations | Output **historical baseline only**; interface and post-change regression **not executed** |
| REQ-M6-05 secure release and approvals | Least privilege, SoD and audit approval | TC-SD-008, 009 | EV-079–EV-080 access limitation only | **Design proposed**, real role verification and approval outstanding |
| REQ-M6-06 test traceability | Register, evidence ledger, defect record | TC-SD-001–009 | EV-017–EV-089 as individually cited | **Documentation completed**, with precise limitations |

**Evidence constraints:** EV-083 is an item-block *pre-save* image. Header clearance and order save were user-confirmed but not separately screenshot-proven. EV-088 shows a delivery item block and the user confirmed delivery save. EV-089 shows accounting links in the invoice 90000307 context; invoice creation was user-confirmed rather than preserved in an invoice-overview screenshot. T41/400 EV-082 cannot establish JV2 settings.
