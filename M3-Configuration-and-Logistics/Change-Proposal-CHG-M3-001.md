# CHG-M3-001 — Proposed enforcement of billing block 04 for F2 invoicing

| Control | Value |
|---|---|
| Related module | M3.03 / M3.04 / M3.06 |
| Document status | **Draft proposal, not approved or implemented** |
| Environment | JV2 / 100 — S/4HANA Cloud Public Edition training system |
| Change owner | Proposed: SAP SD configuration specialist / CBC-authorized administrator |
| Production change? | **No** |

## 1. Business requirement and observed gap

A sales/logistics or finance user selects billing block **04 — Check Payment Terms** to prevent invoicing pending review. In tested delivery-related F2 billing, the block was not enforced:

- **Order-header test:** Order 1056 retained block 04, but delivery 80000785 was invoiced as **90000304**, and FI journal **9400000058** posted.
- **Delivery-header test:** Delivery 80000787 had block 04 applied and saved; goods issue 4900001490 completed; invoice **90000305** was created and FI posting status showed **Journal entry has been created** (invoice type is not independently visible in the retained M3 screenshot).

The tests show a control failure in this scenario, but **not** its root configuration cause. See [investigation](Billing-Block-Behavior-Investigation.md).

## 2. Proposed target behavior

If the business intends billing block 04 to stop F2 invoice creation for relevant source documents, an **authorized configuration specialist** should inspect and, if needed, adjust billing-type/block-reason assignment so that:

1. Billing from a source document carrying active block 04 is rejected with a meaningful error or excluded with an explicit block reason as applicable.
2. A permitted user can remove the block after legitimate business approval.
3. Billing then succeeds exactly once, and downstream FI posting completes without duplicates.
4. Unblocked invoices and unrelated block reasons retain existing behavior.

**Important:** An authorized functional owner must first confirm scope: delivery-related F2, order-related F2 if applicable, header versus item source block, and the intended business control. The current behavior alone does not authorize changing settings.

## 3. Config objects to inspect (not confirmed existing state)

| Candidate | Purpose | Baseline | Proposed action |
|---|---|---|---|
| Cloud config 102358 — Define Billing Blocking Reasons | Inspect meaning/existence of block 04 | **Not inspected** | Retain definition unless business gap confirmed |
| Cloud config **102401 — Assign Blocking Reasons to Billing Types** | Confirm applicability of block 04 to **F2** | **Unknown — CBC denied** | If absent and required, propose authorized assignment of **04 ↔ F2** |
| F2 billing type and delivery-to-F2 copy controls | Check any requirements affecting block propagation/enforcement | **Unknown** | Investigate before implementing; no blind copy-control change |
| Sales order/delivery item/header master and document data | Distinguish where block is persisted | Order header vs delivery header tested | Specify correct source-level semantics in functional design |
| Workflow / roles | Determine who sets/clears billing blocks | Not inspected | Restrict access and require business approval as appropriate |

SAP reference: [KBA 3147488](https://userapps.support.sap.com/sap/support/knowledge/en/3147488) and [KBA 2991828](https://userapps.support.sap.com/sap/support/knowledge/en/2991828). These establish diagnostic relevance, **not actual tenant configuration**.

## 4. Preconditions and authorization

- Access to authorized CBC environment or approved equivalent configuration sandbox.
- Written training-system scope and change approval; no production configuration changes.
- Baseline screenshots/export of relevant existing assignments and any affected copy controls.
- Isolated test customer/material, no shared live orders or postings.
- Ownership of change, rollback and test approvals assigned by the training environment administrator.

**Current status:** CBC access returned **Unauthorized**, so the change is **blocked**. No configuration was edited, transported, or approved.

## 5. Expected impact

| Domain | Expected effect if target enforced | Risk |
|---|---|---|
| Sales | Users can place/release intentional billing hold | Orders blocked longer than intended |
| Logistics | Deliveries can be picked/PGI under a billing hold unless business policy specifies otherwise | Confusion between logistics and invoicing controls |
| Billing | F2 invoice should not be created with active relevant block | Unauthorized reduction in billing throughput |
| Finance | No premature AR/revenue/tax posting for blocked invoices | Period-end cutoff and reconciliation impact |
| Output / interfaces | May delay output and downstream invoice messages | Resend, deduplication, missing output monitoring |
| Reporting | Due-list and blocked-document KPIs change | False aging and SLA reports |
| Authorizations | Block maintenance/release should be controlled | Inappropriate ability to bypass hold |

Detailed matrix: [Change Impact and Regression](Change-Impact-and-Regression-Matrix.md).

## 6. Proposed test and acceptance criteria (NOT EXECUTED)

| Test | Condition | Expected result | State |
|---|---|---|---|
| REG-M3-01 | F2 delivery billing with active **delivery-header** block 04 | Invoice creation prevented with actionable reason | Proposed |
| REG-M3-02 | F2 delivery billing with active **order-header** block 04 | Decision documented and enforced per approved design | Proposed |
| REG-M3-03 | F2 with **item-only** block 04 | Appropriate item restriction per approved design | Proposed |
| REG-M3-04 | Clear block with approval; retry same reference | One invoice, no duplicates; correct SD/FI flow | Proposed |
| REG-M3-05 | Unblocked order/delivery | Baseline F2 completes to balanced FI | Proposed |
| REG-M3-06 | Other billing types/reasons, output and batch due list | Unintended blocking absent; reconciled counts | Proposed |

No tests in this table have passed; they are the **future acceptance suite** for an authorized change.

## 7. Rollback / forward fix

1. Save verified before-state of configuration assignments, expected transport or CBC change identity, and approved release scope.
2. If the change causes adverse results in isolated training or approved environment, restore the **documented prior configuration** using authorized change control (exact mechanics depend on tenant permissions).
3. Inspect whether any blocked/in-flight invoices, billing-due items and output messages require manual reconciliation.
4. Re-run the approved smoke tests and review invoices/journal entries for duplicates.
5. If rollback is not suitable, agree a controlled forward-fix and document owners, approvals and post-fix results.

**No rollback was performed:** no configuration change was made.

## 8. Approval and implementation record

| Gate | Status |
|---|---|
| Business scope confirmed | Pending |
| SD configuration review | Blocked by CBC access |
| Finance / Logistics review | Proposed, not completed |
| Authorization/approval | Not obtained |
| Implementation | Not started |
| Regression and UAT | Not executed |
| Final change sign-off | Pending |

**Final classification:** Proposed configuration improvement based on executed tests; exact tenant cause **unconfirmed**. Do not describe as implemented or validated.
