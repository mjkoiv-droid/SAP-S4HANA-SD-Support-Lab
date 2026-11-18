# M5 — Illustrative high-priority incident communications

**Classification: SIMULATION — no messages sent, no real high-priority designation or customer impact measured.** This communication exercise uses the **real observed posting symptom** from [INC-SD-003](Incident-INC-SD-003-Billing-FI.md) but the audience, urgency classification, escalation, ownership and texts below are hypothetical. No execution dates, response durations or SLA compliance are asserted.

| Sequence | Intended recipient | Sample communication | Actual status |
|---|---|---|---|
| Initial notice | Billing lead / Finance | “F2 invoice 90000303 exists, but posting to FI failed with a customer company-code master-data error. The invoice cannot yet be treated as posted revenue/receivable. We are checking the customer setup in company code 1010.” | **Draft only, not sent** |
| Diagnostic progress | Billing, master-data owner | “The error identifies missing company-code data for customer 1000193 in company code 1010. The customer company-code view is empty. No change to pricing or billing customizing is indicated by the evidence.” | **Draft only, not sent** |
| Escalation/approval request | Master-data / Finance approver | “Please approve the required customer company-code extension, including reconciliation account and payment terms, before any repeat posting. Confirm ownership and correct values under your governance policy.” | **Draft only, not sent** |
| Restored-service message | Billing lead / Finance | “The training customer extension was maintained. Invoice 90000303 has now posted to FI journal 9400000057; debit and credit each total EUR 20.88. The receivable is open, not cleared. Verify equivalent business acceptance before treating a production incident as closed.” | **Draft only, not sent** |
| Closure / prevention | Support problem owner | “Training validation is complete for the specific invoice. Propose checking customer company-code readiness during onboarding; preventive controls and broader regression have not been implemented.” | **Draft only, not sent** |

## Proposed communication controls

- Separate **invoice creation**, **FI posting** and **customer collection** states; never call an uncleared item a posting failure.
- Record measured impact and priority before any actual escalation; the lab does not provide real business impact or service-level metrics.
- Identify the real approver in an actual assignment; the table has no actual business sign-off.
- Obtain owner approval before editing another user's or shared master data.
