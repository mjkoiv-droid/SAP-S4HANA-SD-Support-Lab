# INC-SD-001 — Manual PPR0 sales-price override

| Field | Recorded result |
|---|---|
| Case classification | **Executed; resolved in training sandbox; regression scope limited** |
| System/client | JV2 / 100 |
| SAP transactions | VA01, VA02, VA03, pricing analysis / condition record inspection |
| Sales document | OR **1056**, item 10, customer `1000193`, material `TG11`, 1 PC |
| Business process | Standard price determination and order entry |
| Actual severity / requester / SLA | Not established; illustrative priority: medium if discovered before invoicing |
| Evidence | **EV-014–EV-016, EV-042, EV-071–EV-072** |

## Symptom and business impact

A controlled test manually replaced the legitimate **PPR0 EUR 17.55 / PC** with **EUR 15.55 / PC** in the sales order. A EUR 2.00 unit undercharge would result if the price passed downstream unchanged. This was deliberately produced in the training environment, not a production incident or measured revenue loss.

## Reproduction and diagnosis

1. Baseline PPR0 EUR 17.55 was shown in the pricing conditions (**EV-014**).
2. The operator manually entered EUR 15.55 and saved the order. The saved incorrect amount was reported in the workshop but not independently captured in its own image.
3. Pricing Analysis showed **PPR0 reason/message 203: condition record found and manually changed** (**EV-015**). It proves a manual intervention; it does not on its own reproduce the saved EUR 15.55 value.
4. An independent condition-record check confirmed valid PPR0 EUR 17.55 for the tested pricing keys (**EV-042**).

**Hypotheses assessed:** Invalid master condition record — contradicted by EV-042. Deliberate manual override — supported by input actions and pricing message 203. Broader pricing-procedure defect — not established.

## Root cause and corrective action

- **Immediate trigger:** Manual replacement of PPR0 on the order line.
- **Confirmed cause in this controlled test:** Document-level manual price override despite a valid condition record.
- **Executed correction:** Restore PPR0 EUR 17.55 in order 1056 and save.
- **Verified result:** VA03 PPR0 and net value **EUR 17.55** (**EV-016**, independently observed again **EV-072**). Order flow shows completed invoice **90000304** and FI journal **9400000058** (**EV-071**).
- **Preventive proposal, not implemented:** Approval/variance review for manual reductions, plus properly scoped role/control assessment.

## Test and closure

| Test | Expected | Actual | Classification |
|---|---|---|---|
| Baseline | Determined price 17.55 | PPR0 17.55 | Pass — actual SAP |
| Negative | Manual change causes discrepancy | Manual 15.55; reason 203 observed | Executed; amount partly workshop-reported |
| Correction | Order price restored | PPR0/net 17.55 | Pass — actual SAP |
| Independent follow-up | Correct price persists | Order 1056 net 17.55; billing flow completed | Pass — actual SAP |
| Cross-customer regression | Price determination works for other customers | Not tested | **Open / not verified** |

**Closure:** Resolved for order 1056 only. No assertion of a permanent SAP system-level control or cross-customer regression. Detailed analysis: [RCA-SD-001](RCA-SD-001-Pricing.md).

## Investigation standard

- **Training context:** These are training-sandbox observations, not customer production incidents. Impact, severity, roles, and communications are scenarios unless a system effect was actually observed.
- **Evidence standard:** A screenshot of successful status alone does not prove how a prior failure was corrected. Where a previous module documented the negative test and correction, both are linked. No unexecuted action is described as complete.
