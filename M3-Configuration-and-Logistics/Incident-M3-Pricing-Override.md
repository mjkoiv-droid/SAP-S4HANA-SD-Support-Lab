# M3-INC-001 — Incorrect manually overridden PPR0 selling price

| Field | Result |
|---|---|
| Scenario | Real controlled training-sandbox pricing discrepancy, originally executed in M1 |
| SAP system | JV2 / client 100 |
| Customer | 1000193 |
| Sales order | **1056**, item 10, TG11, 1 PC |
| Expected / reference price | **EUR 17.55** (PPR0 condition record) |
| Incorrect price | **EUR 15.55** manual override; EUR 2.00 undercharge (~11.4%) |
| Reproduction | **Executed** and order saved at incorrect price |
| Diagnosis | Pricing Analysis Y10101, PPR0 **message 203**: condition record found and changed manually |
| Correction | Restored PPR0 EUR 17.55 and saved order 1056 |
| Retest | VA03 Conditions independently showed PPR0 / net **EUR 17.55** |
| Status | **Resolved / PASS**, with evidence |

## Steps and evidence

1. Baseline selling price PPR0 EUR 17.55 was captured in M1 [EV-014](../M1-Landscape-and-Monitoring/evidence/pricing-baseline.png).
2. In VA01, condition amount changed manually to EUR 15.55 and standard order **1056** saved. This is a **business rule / data quality** problem, not a SAP technical message.
3. Pricing Analysis showed reason **203** on PPR0: condition record found but value manually changed — [EV-015](../M1-Landscape-and-Monitoring/evidence/pricing-analysis-manual-override.png).
4. Change order 1056 corrected PPR0 to EUR 17.55; VA03 verified correct condition and net amount — [EV-016](../M1-Landscape-and-Monitoring/evidence/pricing-corrected-va03.png).
5. An independent PPR0 record check performed in M3 found sales org **1010**, DC **10**, material **TG11**, price **EUR 17.55 / 1 PC**, valid **a maintained validity interval** — [EV-042](evidence/m3-ppr0-condition-record.png).

## Root cause and control recommendation

**Cause:** Document-level manual replacement of a valid condition record's PPR0 value. **Trigger:** Deliberate manual entry for lab. **Impact:** Potential underbilling and margin distortion. **Correction:** Restore price in document, validate pricing analysis. **Preventive proposal (not implemented):** Restrict manual override by role or document approval threshold as appropriate; introduce review for negative variances and regression tests for normal pricing.

**Regression boundary:** One material/customer/order combination was verified. Cross-customer or multi-material regression was **not** executed. No shared condition master record was modified.
