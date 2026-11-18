# INC-SD-003 — Billing-to-FI posting failure from customer company-code master data

| Field | Recorded result |
|---|---|
| Classification | **Executed; resolved in training system** |
| System/client | JV2 / 100 |
| Transactions | Billing / VF03, BP master data, FI journal display |
| Process | Delivery-related F2 invoice transfer to FI; **not a billing-creation failure** |
| Documents | Order `1055` → delivery `80000784` → billing `90000303` → FI journal `9400000057` |
| Customer / company code | `1000193` / `1010` |
| Priority / SLA | No real support priority, requester or SLA established |
| Evidence | **EV-020–EV-026, EV-074–EV-076** |

## Symptom, impact and reproduction

The F2 billing document `90000303` was created but did not post to Financial Accounting. SAP displayed **Error in Accounting Interface** and **`Customer 1000193 is not defined in company code 1010`** (**EV-021–EV-022**). The customer lacked the necessary company-code data (**EV-023**). The financial result was initially no journal for this invoice; billing document creation itself had succeeded.

**Potential business impact:** Unposted billing and missing receivable/revenue/tax transfer until correction. This is a training observation, not a measured company exposure.

## Diagnosis and correction

| Step | Evidence | Finding |
|---|---|---|
| Inspect billing posting status | EV-021–EV-022 | Billing existed; accounting transfer failed with explicit missing customer company-code error |
| Inspect customer master | EV-023 | Company code 1010 view missing |
| Maintain required master data | EV-024 | Customer/company-code entry created with reconciliation account `12100000` and terms `NT30`; screenshot shows draft, not final save confirmation |
| Retest posting / inspect FI | EV-025–EV-026 | Invoice completed; journal `9400000057` posted with balanced receivable, revenue and tax lines |
| Independent follow-up | EV-074–EV-076 | Invoice and FI journal still present; FI journal displayed **Not Cleared** (not an error) |

## Root cause and validation

**Root cause:** Customer master was not extended to company code 1010 when the billing-to-FI process required it. **Executed correction:** Create relevant company-code master record. **Confirmed downstream result:** FI journal 9400000057 with AR debit **EUR 20.88**, revenue credit **EUR 17.55**, tax credit **EUR 3.33**; debit equals credit (**EV-026**).

| Test | Outcome | Classification |
|---|---|---|
| Invoice created | F2 90000303 exists | Executed |
| FI transfer with missing master | Explicit failure / no FI journal | Executed, negative result |
| Maintain customer company-code data | Entry maintained; subsequent success verifies viable setup | Executed |
| Retest FI posting | Balanced document 9400000057 | Executed, resolved |
| Payment/clearing | Journal open, Not Cleared | Not performed |
| Billing-block negative test | Separate JV2 billing-control anomaly documented in M3 | **Not a successful blocking control** |

**Closure:** Resolved **SD-to-FI posting error**, not a billing-creation failure. The unrelated unresolved F2 billing-block behavior is tracked separately in [PRB-SD-001](Problem-Record-PRB-SD-001.md) and [M3 billing-block investigation](../M3-Configuration-and-Logistics/Billing-Block-Behavior-Investigation.md). Detailed analysis: [RCA-SD-003](RCA-SD-003-Billing-FI.md).

## Investigation standard

- **Training context:** These are training-sandbox observations, not customer production incidents. Impact, severity, roles, and communications are scenarios unless a system effect was actually observed.
- **Evidence standard:** A screenshot of successful status alone does not prove how a prior failure was corrected. Where a previous module documented the negative test and correction, both are linked. No unexecuted action is described as complete.
