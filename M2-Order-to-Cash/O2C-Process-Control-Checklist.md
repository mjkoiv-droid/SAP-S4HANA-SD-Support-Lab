# M2 — O2C Execution and Reconciliation Checklist

**System/client:** JV2 / 100 — SAP S/4HANA Cloud Public Edition training sandbox.  
**Executed:** 16–17 November 2026.  
**Status:** Two end-to-end O2C document chains **PASS**; separate billing-block negative test **FAIL / OPEN**.  
**Verification standard:** Captured SAP screenshot or exact contemporaneous user-reported SAP message. Distinguish fields that were not measured.

## Cross-scenario controls

| Check | Scenario 1: 1055 | Scenario 2: 1056 | Assessment |
|---|---|---|---|
| Order type/material/qty | OR, TG11, 1 PC | OR, TG11, 1 PC | Both verified |
| Customer/organization | 1000193 / 1010/10/00 | 1000193 / 1010/10/00 | Both verified |
| Standard pricing / VAT | 17.55 / 3.33 EUR | 17.55 / 3.33 EUR | Both verified |
| ATP/schedule line | Delivery 1 PC; schedule-line confirmation screenshot not retained for 1055 | 1 PC confirmed, schedule line CP | Partial for 1055 |
| Delivery | 80000784 | 80000785 | Both saved |
| Picking | 1 PC fully picked, status C | Fully Picked (user confirmation) | Both executed |
| PGI material document | 4900001488 | 4900001489 | Both created, confirmed in flow |
| Movement type 601 | Not displayed | Not displayed | **NOT VERIFIED** |
| Actual inventory balances before/after PGI | Not measured | Not measured | **NOT VERIFIED** |
| Billing F2 | 90000303 | 90000304 | Both saved |
| Ordered / delivered / invoiced | 1 / 1 / 1 PC | 1 / 1 / 1 PC | Both verified from combined screenshots |
| Billing status and FI transfer | Initial error; corrected | Completed without FI posting error | Both ultimately posted |
| FI journal | 9400000057 | 9400000058 | Both verified |
| AR debit | 12100000: 20.88 EUR | 12100000: 20.88 EUR | Both verified |
| Sales revenue credit | 41000000: 17.55 EUR | 41000000: 17.55 EUR | Both verified |
| Output tax credit | 22000000: 3.33 EUR | 22000000: 3.33 EUR | Both verified |
| FI debit = credit | 20.88 = 20.88 EUR | 20.88 = 20.88 EUR | **PASS** |
| Payment / clearing | Not executed | Not executed | Not part of demonstrated cycle |

## Exception control findings

### Scenario 1 — SD–FI account master data

**Expected:** Billing document creates a journal entry.  
**Observed initial:** Account interface error. SAP message: `Customer 1000193 is not defined in company code 1010.`  
**Verified correction:** Add customer company-code data 1010 / reconciliation 12100000 / terms NT30.  
**Retest:** FI document 9400000057 posted and balances. **PASS / RESOLVED.**

### Scenario 2 — Billing-block enforcement

**Expected:** Header block 04 prevents invoice creation during VF01 with delivery 80000785.  
**Observed:** Invoice 90000304 and FI journal 9400000058 created despite active header block, which persisted in final VA03 Status Overview.  
**Result:** **FAIL / UNRESOLVED**. Follow up in M3. No proof yet of the configuration-level reason; no corrective configuration change executed.

## Completeness notes

- Both cases are real SAP training execution, not production transactions and not fictional simulations.
- Dates shown as January 2027 on schedule lines are planned fulfilment dates, whereas actual PGI and billing were posted in November 2026; do not confuse planned versus actual.
- Material documents confirmed, but independent before/after inventory quantities were not captured.
- Additional journal entries appeared in Scenario 2 document flow; do not infer their nature without inspection.
- The two billing-block test outcomes are not conflated: an **O2C chain PASS** is compatible with a separate **control FAIL**.

See the [swimlane](O2C-Executed-Swimlane-and-Controls.md) and [scenario traces](README.md).
