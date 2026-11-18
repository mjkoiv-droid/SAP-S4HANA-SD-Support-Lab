# RCA-SD-001 — Manually overridden PPR0 price

| Field | Result |
|---|---|
| Related incident | [INC-SD-001](Incident-INC-SD-001-Pricing.md) |
| Context | JV2 / 100, order `1056` item 10, 1 PC TG11 |
| Outcome | **Confirmed document-level cause; order correction verified; prevention unimplemented** |
| Evidence | EV-014–EV-016, EV-042, EV-071–EV-072 |

## Executive conclusion

An operator deliberately replaced the condition-record-derived PPR0 value **EUR 17.55** with **EUR 15.55** in the sales order. Pricing Analysis reported **message 203**, indicating a condition record had been found and its value manually changed. An independent condition record check showed the reference price was valid. The order was corrected back to EUR 17.55 and independently verified via VA03.

This is a **training-only, deliberately induced data/control exception**, not a software defect and not a customer financial loss.

## Causal chain and hypotheses

| Candidate cause | Observed test | Conclusion |
|---|---|---|
| Wrong condition record | Checked PPR0 EUR 17.55 / PC | Not supported for tested key |
| Manual override on order | Operator action and pricing-analysis reason 203 | Supported — direct cause |
| Pricing-procedure configuration error | No comparative procedure/re-determination test | Unverified |
| System-wide lack of price override governance | No roles/approval workflow inspected | Unverified — proposed control issue only |

### Evidence-limited 5 Whys

1. **Why did order value become incorrect?** The order-level selling price was changed to EUR 15.55.
2. **Why did it differ from the maintained condition record?** A manual PPR0 override replaced the EUR 17.55 value; message 203 supports this.
3. **Why was manual override attempted?** Deliberately as an approved training negative test; there is no real-user process explanation to discover.
4. **Why did the transaction permit the change?** The test workflow accepted and saved a manually entered condition, but the specific authorizations/configuration enabling this were not audited.
5. **Why was there no preventive rejection?** **Not established.** No price-approval configuration or systematic guardrail test was executed. It would be improper to claim a confirmed five-level organizational root cause.

**Confirmed immediate cause:** Manual condition override. **Potential preventive-control gap:** Unreviewed price exceptions; proposed, not proven as a failed company policy.

## SD and downstream implications

The order was at risk of an undercharge of EUR 2.00 per unit if billed at the lower price. Subsequent document flow for order 1056 shows invoice **90000304** at **EUR 17.55** and FI journal **9400000058**, indicating correct final pricing in this executed test. No financial adjustment, refund or production exposure is claimed.

## Action tracking

| Action | Classification | Actual result | Status |
|---|---|---|---|
| Restore PPR0 17.55 in order 1056 | Corrective — executed | Confirmed in VA03 (EV-016 and EV-072) | Complete |
| Verify pricing record EUR 17.55 | Diagnostic — executed | EV-042 | Complete |
| Verify downstream billing value | Read-only follow-up — executed | Order document flow (EV-071) | Complete for 1056 |
| Prevent unmanaged manual reductions | Preventive proposal | Role/approval/variance controls not evaluated | Proposed only |
| Cross-customer / other-material regression | Test proposal | No actual run | Open |

## Closure and limitation

**RCA closure for the single training case:** Cause and order-level fix verified. **Not verified:** System-wide durable prevention, why the user was permitted to override PPR0, and any cross-customer regression. No customer sign-off or SLA was obtained.
