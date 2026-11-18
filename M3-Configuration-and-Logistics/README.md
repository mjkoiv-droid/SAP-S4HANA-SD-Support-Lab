# M3 — SD Configuration and Logistics Exceptions

**SAP execution status:** Read-only configuration-dependent inspection and real sandbox transaction tests **performed**; one picking defect corrected and verified. The billing-block enforcement defect is **reproduced but configuration root cause unverified**. SAP Central Business Configuration (CBC) access is **denied**, so no configuration was changed or transported. Proposed settings, approval and regression tests are explicitly **proposed / not executed**. This is a training-sandbox portfolio, not production consulting work.

## Module outcomes and boundaries

| Workstream | Evidence / deliverable | Classification |
|---|---|---|
| M3.01 Document, item, schedule line, copy control, shipping / billing | OR, TAN and CP observed; plant/shipping point and blocks observed; **copy-control customizing and VOV* settings not inspected** | **Partial — read-only observation** |
| M3.02 Pricing, conditions, account determination | PPR0 record and price checked; FI accounts observed in M2; customizing for revenue determination not inspected | **Partial — read-only observation** |
| M3.03 Proposed safe change and dependencies | [Proposed billing-block control CHG-M3-001](Change-Proposal-CHG-M3-001.md) | **Proposed only** |
| M3.04 Authorized implementation | CBC denied; no custom settings implemented, no transports | **Blocked — access** |
| M3.05 Two negative/positive exceptions | [Pricing override](Incident-M3-Pricing-Override.md) (M1 evidence reused); [Picking mismatch](Incident-M3-Picking-Exception.md) (M3 evidence) | **Executed and verified** |
| M3.06 Cross-functional risk, regression and impact | [Change impact and regression matrix](Change-Impact-and-Regression-Matrix.md) | **Proposed / analyzed; tests not executed** |

## Work products

- [Filled configuration analysis — CFG-SD-001](Configuration-Analysis-CFG-SD-001.md)
- [Change proposal — CHG-M3-001](Change-Proposal-CHG-M3-001.md)
- [Impact and regression matrix](Change-Impact-and-Regression-Matrix.md)
- [Incident 1: Manual selling-price override](Incident-M3-Pricing-Override.md)
- [Incident 2: Partial picking / blocked goods issue](Incident-M3-Picking-Exception.md)
- [Supplemental investigation: Billing block 04 ineffective in two observed scenarios](Billing-Block-Behavior-Investigation.md)
- [Original reusable configuration analysis template](Configuration-Analysis-Template.md)
- [Central evidence register](../00-Project-Tracking/Evidence-Register.md)

**Evidence:** EV-036–EV-052 are M3-specific screenshots. EV-014–EV-016 provide earlier pricing before/after evidence, and EV-033–EV-035 provide M2 billing-block and FI evidence. Save notices and the CBC **Unauthorized** response were reported directly in the workshop chat, not preserved as screenshot images; they are labeled accordingly.

**Unfinished:** Independent reading of VOV8/VOV7/VOV6, VTFL/copy-control and SSCUI 102401, authorized change execution, regression after proposed change, exact GI movement type and stock balances. These are not claimed as completed.
