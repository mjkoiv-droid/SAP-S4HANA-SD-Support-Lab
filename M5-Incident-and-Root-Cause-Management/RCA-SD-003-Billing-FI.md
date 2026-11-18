# RCA-SD-003 — Customer company-code master-data omission prevents billing FI posting

| Field | Result |
|---|---|
| Related incident | [INC-SD-003](Incident-INC-SD-003-Billing-FI.md) |
| Context | JV2 / 100, invoice `90000303`, customer `1000193`, company code `1010` |
| Outcome | **Explicit SAP error, missing data, corrective extension and successful FI retest confirmed** |
| Evidence | EV-020–EV-026, EV-074–EV-076 |

## Executive conclusion

An F2 billing document was created, but accounting transfer initially failed with **`Customer 1000193 is not defined in company code 1010`**. The customer did not have the required company-code master record. The company-code extension was maintained with reconciliation account `12100000` and payment terms `NT30`. A retest produced FI journal **9400000057**, balancing EUR 20.88 debit and EUR 20.88 credit.

**This is an SD–FI posting error, not an invoice-creation error.** The distinction is essential in troubleshooting and case routing.

## Cause analysis

| Hypothesis | Diagnostic evidence | Conclusion |
|---|---|---|
| F2 invoice did not exist | Invoice 90000303 saved and displayed | Rejected |
| FI interface prevented accounting | Error in Accounting Interface, EV-021 | Confirmed symptom |
| Customer not extended to company code 1010 | Explicit message EV-022 and absent company code EV-023 | Confirmed root cause in this scenario |
| Tax / revenue mapping error | Balanced journal after master extension; no independent mapping test | No evidence for primary cause |
| CBC billing-block setting responsible | Unrelated block behavior occurred in different scenario | Not supported as cause of this FI posting failure |

### Evidence-limited 5 Whys

1. **Why was no FI journal generated initially?** The billing-to-FI transfer failed.
2. **Why did transfer fail?** SAP reported customer 1000193 undefined in company code 1010.
3. **Why did the customer fail validation?** Its relevant company-code master record was absent (EV-023).
4. **Why had the company-code extension not been created?** **Not established.** This training case did not audit the master-data onboarding or master-change approval process.
5. **Why did no earlier control catch the omission?** **Not established.** We can propose onboarding/pre-billing controls, not claim a proven design deficiency.

**Confirmed root cause:** Missing customer company-code FI data at billing transfer time.

## Corrective action and verification

| Action | Type | Status | Evidence |
|---|---|---|---|
| Review master company-code view | Diagnostic | Completed | EV-023 |
| Maintain customer/1010 FI data | Corrective, actual SAP | Completed for case; draft screen itself is not save proof | EV-024 and later posting |
| Reattempt accounting transfer | Positive retest, actual SAP | **Passed** | EV-025–EV-026 |
| Independently recheck accounting link | Read-only SAP follow-up | **Passed** | EV-074–EV-076 |
| Customer payment/AR clearing | Outside this case | **Not done** | EV-074 shows Not Cleared |
| Implement onboarding control / validation checklist | Preventive proposal | **Not implemented** | No approval/testing evidence |

## FI cross-module impact

Posted FI document `9400000057`: AR `12100000` debit EUR **20.88**, revenue `41000000` credit EUR **17.55**, output tax `22000000` credit EUR **3.33**. Document is **Not Cleared**: an outstanding receivable, not a new posting error. Customer receipt and balance clearing were not executed.

**RCA closure:** Corrected and retested successfully for invoice 90000303. No assertion of customer onboarding process change, broader master-data cleansing, or real-business approval.
