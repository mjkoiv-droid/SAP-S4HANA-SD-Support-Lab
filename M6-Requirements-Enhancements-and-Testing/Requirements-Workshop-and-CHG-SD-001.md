# M6 — Requirements workshop and change request CHG-SD-001

| Attribute | Classification |
|---|---|
| Scope | JV2 / client 100; order-to-cash for material TG11 |
| Input | Actual JV2 observations in M2–M5 and M6 |
| Stakeholder workshop | **Documented role-play only**; no Sales, Logistics or Finance representatives were interviewed |
| Change status | **Proposed, not approved, not implemented** |
| Related problem | [PRB-SD-001](../M5-Incident-and-Root-Cause-Management/Problem-Record-PRB-SD-001.md) |
| Existing proposal | [CHG-M3-001](../M3-Configuration-and-Logistics/Change-Proposal-CHG-M3-001.md) |

## 1. Problem and business objective

In actual training transactions, **04 — Check Payment Terms** was selected at sales-order header, delivery header, sales-order item and delivery item level in separate tests. Delivery-related F2 invoices were nevertheless created. In M6 the newly created invoices also produced FI accounting documents. This is an **unmet proposed business control**, not a demonstrated SAP standard defect, financial loss or confirmed incorrect configuration.

**Business objective (proposed):** If the business authorizes reason 04 as a preventive payment-terms hold on delivery-related F2 invoices, an active in-scope block should prevent invoice creation until an authorized release. Unblocked transactions must continue normally.

## 2. Simulated stakeholder requirements conversation

*The statements below are a training-role-play design; they are not quotations, approvals or actual meetings.*

| Role (fictional) | Illustrative concern | Open business decision |
|---|---|---|
| Sales key user | Avoid invoicing before payment-term exception review | Who may set/remove reason 04 and at which source-document level? |
| Logistics key user | Shipping and goods-issue processing should not be unexpectedly stopped by an invoice hold | Can delivery and PGI proceed while billing is held? |
| Finance key user | Prevent premature AR, revenue and tax posting; preserve reconciliation | Should the hold apply to F2 only, and to which order-/delivery-related billing paths? |
| SD functional analyst | Establish precise source-level logic and regression criteria | What do actual JV2 CBC billing-type assignments and copy rules permit? |

## 3. Requirements and acceptance criteria

| ID | Proposed requirement | Priority | Acceptance criterion after approved change |
|---|---|---|---|
| REQ-M6-01 | Authorized delivery-related F2 billing hold | High | Eligible delivery with active configured 04 at the approved source/level cannot create F2; meaningful system response |
| REQ-M6-02 | Authorized release and clean restart | High | After approved clearance, exactly one F2 invoice and appropriate FI accounting entries are created |
| REQ-M6-03 | Preserve ordinary fulfillment | High | Unblocked OR/TAN/TG11 order, picking, PGI and F2 flow continue as baseline |
| REQ-M6-04 | Prevent unnecessary cross-impact | Medium | Order-related billing, other block reasons, output and interfaces are assessed and regression-tested where applicable |
| REQ-M6-05 | Govern setting/releasing the hold | High | Role ownership, approval, audit trail and SoD defined before release |
| REQ-M6-06 | Trace requirements to test results | Medium | Matrix distinguishes historical executions from post-change validation and unresolved tests |

## 4. Scope and boundaries

**In scope for analysis:** JV2 client 100, OR/TAN physical-goods scenario, customer 1000193, material TG11, sales area 1010/10/00, plant 1010; F2 eligibility and SD–logistics–FI dependencies; output/interface review; unit, negative, integration, boundary and UAT designs.

**Not in scope as performed:** No JV2 CBC configuration update, production deployment, transport, actual end-user workshop, approval, genuine business UAT or post-change retest. T41/400 IMG observations are **separate-system** evidence only.

**Open assumptions:** The business purpose and affected blocking levels have not been formally approved; JV2 billing-block assignment and copy control are not verified. The proposed control must be confirmed as technically suitable before any change.

## 5. Proposed change / decision record

- **CHG-SD-001** extends the investigation initiated in CHG-M3-001; it is not a second independent implemented change.
- **Business decision:** Pending actual Sales and Finance owners; logistics to confirm shipment behavior.
- **Technical decision:** Pending authorized JV2 CBC read access and design analysis.
- **Approval:** Not obtained. The role-play does not confer authorization.
- **Implementation:** Not started. **Rollback:** Design only; no system change to reverse.
- **Closure:** Change stays open. Evidence of failed pre-change expected controls does **not** count as successful remediation.

See [Functional Specification](Functional-Specification-CHG-SD-001.md), [Impact Assessment](Change-Impact-Assessment-CHG-SD-001.md), [Traceability](Requirements-Traceability-Matrix.md) and [Test Register](Test-Execution-and-Defect-Register.md).
