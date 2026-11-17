# M3 — Change impact, risk and regression coverage (proposed)

**Related proposal:** [CHG-M3-001](Change-Proposal-CHG-M3-001.md). **State:** Analytical design only; *no authorized customizing change or regression tests executed*. Observed historical O2C and control-failure cases are listed separately from future test expectations.

## Before-state observation

| Test context | Result observed in SAP | Evidence |
|---|---|---|
| 1056 order-header billing block 04 | Delivery 80000785 invoiced 90000304, FI journal 9400000058 posted | [EV-051](evidence/m3-order1056-billing-block-final-status.png), M2 EV-032–EV-035 |
| 1056 order-item billing block | Blank | [EV-037](evidence/m3-order1056-item-no-billing-block.png) |
| Delivery 80000785 header billing block | Blank | [EV-036](evidence/m3-order1056-delivery-no-billing-block.png) |
| Delivery 80000787 header billing block 04 | Block selected, saved and user-confirmed; invoicing nevertheless completed | [EV-038](evidence/m3-delivery80000787-billing-block.png), user-reported save/verification, invoice 90000305 |
| Controls available for customizing review | CBC-managed environment; separate CBC access Unauthorized | [EV-040](evidence/m3-cbc-tenant-managed.png), user report |

## Integration impact and decision table

| Scope | Risk / dependency | Required check before sign-off | Owner (proposed) | State |
|---|---|---|---|---|
| Sales order entry | Header/item holds differ; payment-term workflow | Define approved stage, source and conditions for block 04 | Sales / SD | Pending |
| Delivery / PGI | Billing control distinct from shipment control | Ensure authorized shipments aren't unintentionally blocked | Logistics / SD | Pending |
| Invoice F2 | Eligibility depends on billing reason / type and source | Inspect 102401 and billing copying rules; direct and due-list creation | SD Billing | Blocked CBC |
| Accounts receivable / GL | Premature revenue, tax, AR; cutoff | FI line verification; correct company code and reconciliation master | Finance | Pending |
| Material / cost | PGI may precede billing | Check COGS/stock/document flow consistency; movement type | Logistics / FI | Pending |
| Output | Invoice forms/messages could be deferred | Confirm generated output only on permitted invoices | Output support | Pending |
| Interfaces | Duplicate billing IDs / retransmissions | Idempotence, status log and partner reconciliation | Integration | Pending |
| Reporting | Due list / blocked rate change | Compare queues, aging, period-close KPIs | Reporting | Pending |
| Authorization / audit | Block release may be misused | Confirm roles, SoD, log of changes | Security | Pending |
| Release / regression | Inconsistent behavior across variants | Unit/integration/UAT with test IDs REG-M3-01–06 | Change manager | Pending |

## Proposed regression cases — future, not performed

| ID | Purpose | Expected result |
|---|---|---|
| REG-M3-01 | Delivery-header block 04 with F2 | Billing prevented |
| REG-M3-02 | Order-header block 04 → delivery-related F2 | Matches explicitly approved requirement, no silent bypass |
| REG-M3-03 | Item-only block 04 | Item-level restriction consistent with business design |
| REG-M3-04 | Authorized block removal → F2 | Exactly one invoice and balanced FI journal |
| REG-M3-05 | Unblocked baseline SD→LE→FI | Complete flow without unintended regression |
| REG-M3-06 | Different billing types, other block reasons, output and reporting | No unintended impact |

## Risk / effort / controls

**Risk rating:** Medium-to-high *potential* business control exposure for early invoicing; not assessed in production. **Impact priority:** Subject to business/Finance approval. **Rollback:** Restore approved before-state configuration after authorized review, reconcile outstanding documents, and revalidate control behavior. **Security:** Only CBC-authorized sandbox administrator may change settings; no SAP configuration edits have occurred in JV2/100.
