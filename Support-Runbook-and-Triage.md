# M1 — Support Operations Runbook and Two Controlled Triage Cases

**Status:** Runbook drafted for a **fictional** global company, and two actual **SAP sandbox** practice cases executed and validated on 16 November 2026. These are not enterprise service-desk incidents.  
**Fictional business:** Atlas Components Global — Japan sales, Singapore logistics, UK finance. Operational model is a role-play; actual tested documents belong to the separate SAP sandbox NPS Test Chemical GmbH customer (1000193).  
**Source:** Original Word guide M1 and ticket standard §6.1.

## A. Support operating model (policy design / simulated)

### 1. Scope and communication

The SD support analyst coordinates Sales (JP), Warehouse/Logistics (SG), Finance (UK), Security, and Change Management. The organization, owners and response targets below are design assumptions for the fictional training company. They are **not observed services, staffed shifts or achieved SLAs**.

| Priority | Illustrative impact/urgency test | Target initial response (fictional proposal) | Escalation route |
|---|---|---|---|
| P1 Critical | Multi-country order/shipping/billing stopped, no workaround | 15 min | SD lead + incident bridge + affected business owners |
| P2 High | Key sales process blocked for several users, material financial risk | 30 min | SD lead + functional owner |
| P3 Medium | Localized order/price issue, controlled workaround possible | 4 business hours | SD analyst + sales key user |
| P4 Low | Information/request with limited immediate impact | 1 business day | Service desk / feature owner |

Select priority from both business impact (scope, monetary effect, deadline, compliance) and urgency (time until consequence); do not infer high severity from error-message color alone.

**Ticket types:** Incident = unexpected loss/degradation of an agreed service; Service request = standard authorized demand; Problem = underlying cause common to incidents; Change = controlled modification requiring impact and approval.

**States:** New → Triaged → Investigating → Mitigation/Correction → Pending Validation → Resolved → Closed; Reopened if regression fails; Blocked/Waiting for Approval where applicable.

**Evidence rule:** Track user-visible symptom, reproducible steps, expected/actual, document IDs and client, timestamp/timezone, error text, hypotheses, cause, allowed correction, control/rollback, negative and positive tests, business impact, evidence IDs, final sign-off. Avoid secrets/personal data. Retain failed test and successful retest separately.

**Daily handover format (fictional):** incident ID, JP/SG/UK impact, priority, first detection and last verified status (timezone explicit), owner, workaround, performed checks, next action, pending approval/dependency, next update commitment and linked evidence. Pending cases must never appear as resolved solely because symptoms stopped.

### 2. Daily support checklist

| Step | Monitor / decision | Observed M1 capability |
|---|---|---|
| 1 | Compare open incident count, aging, escalations and previous handover | Fictional workflow only; no live ticket-system access |
| 2 | Review sales fulfillment issues and blocked/aged sales documents | Sales Order Fulfillment Issues accessible; 44 flags in 40 documents (historical sample baseline) |
| 3 | Review order/ATP and due deliveries, picking/PGI backlog | Sales-order and outbound-delivery apps accessible; eight `Ready to Post GI` records at baseline |
| 4 | Review billing posting blocks, accounting errors and unbilled delivery backlogs | Manage Billing Documents accessible; 63 FI posting blocks at baseline |
| 5 | Review delivery outputs and pending/failed output items | F4455 accessible; 802 in preparation, 1,543 completed |
| 6 | Review app/interface logs and failed IDocs | SIT log category accessible; general SD log and IDoc monitor not verified here; use M4 alternate sandbox |
| 7 | Confirm triage ownership, incident severity, change approvals and evidence | Policy-only in fictional runbook |
| 8 | Publish JP/EN handover with risk, owner, next checkpoint | M9 controlled bilingual handover exercise pending |

**Escalation:** stop unsupervised remediation of shared roles/configuration/IDocs/transport; seek authorized sandbox and approval before replay/transport. No bulk processing of historical test artifacts.

## B. M1-TRIAGE-001 — Controlled delivery-block incident (cross-reference INC-SD-002)

| Field | Verified fact or lab classification |
|---|---|
| Nature | **Executed SAP training incident** — deliberate application of a known delivery block, not an accidental real-world outage |
| Priority/region | P3 illustrative; training customer in DE sales organization, not actual JP/SG incident |
| Sales order | **1055**, customer 1000193, material **TG11**, quantity **1 PC**, value **EUR 17.55**, plant 1010, item category **TAN** |
| Initial controlled defect | Delivery Block = **Political Reasons** (header) |
| Expected | With an ordinary sell-from-stock item, delivery creation must be prevented when blocked; become possible once the block is removed |
| Negative test | On attempting delivery creation SAP explicitly returned **`Sales order is blocked for delivery: Political Reasons`**; screenshot EV-010 |
| Diagnosis | Earlier alternatives `POWERRACK_472` (CB1 third-party, PR 10000248) and `TG11_PH_GP200` (TAN but no stock) were unsuitable for isolating the block. Valid test material TG11 was chosen; root cause of **controlled** rejection established by explicit SAP message |
| Correction | Delivery block was cleared in VA02; user subsequently created outbound delivery 80000784 |
| Positive retest | SAP document flow links **sales order 1055/item 10 → outbound delivery 80000784/item 10**, 1 PC, EV-011 |
| Additional outcome | Shipping point 1010, ship-to 1000193; delivery **Checked**, **Not Yet Picked**, **GI Not Yet Started**, **Not Invoiced** (EV-012 and EV-013). No PGI/billing performed |
| Risk/rollback | Avoid blind use of shared blocked order; record reason and restore authorized settings if required. In this test the chosen control is removed only from own order |
| Business consequence | In a genuine business process a header block prevents standard delivery processing; here effect restricted to a training order |
| Status | **Resolved and verified for delivery creation only**, not O2C completion |
| Evidence | EV-008–EV-013; save confirmations reported in conversation; system order and delivery IDs |

## C. M1-TRIAGE-002 — Controlled pricing incident (cross-reference INC-SD-001)

| Field | Verified fact or lab classification |
|---|---|
| Nature | **Executed SAP training incident** — deliberate manual sales-price override; SAP accepts it as valid input, so this is a *business discrepancy*, not a technical SAP exception |
| Priority | P3 illustrative, single training order |
| Sales order | **1056**, customer 1000193, material **TG11**, item 10, qty 1 PC, standard item TAN |
| Baseline/expected | PPR0 **EUR 17.55**, TTX1 tax 19% (EUR 3.33), total EUR 20.88, PCIP internal price EUR 13.50; EV-014 |
| Known defect | Price overridden manually from **EUR 17.55 to EUR 15.55** (EUR 2.00 / ~11.4% undercharge); order 1056 saved |
| Diagnosis | Pricing procedure **Y10101**; Pricing Analysis specifically stated for PPR0: **message 203 — `Condition record was found and changed manually`**, EV-015 |
| Root cause | Incorrect document-level **manual PPR0 override**; not evidence of missing condition record/configuration |
| Correction | PPR0 amount restored to EUR 17.55 in order 1056 and order saved |
| Independent positive retest | **VA03** item 10 Conditions shows PPR0 **EUR 17.55** and net **EUR 17.55**, EV-016 |
| Risk/rollback | Only document-level condition changed; no global pricing/condition record was edited |
| Business consequence | Simulated undercharge before correction, EUR 2.00 excluding tax on one training item |
| Status | **Resolved and independently verified** |
| Evidence | EV-014–EV-016; order 1056 |

**Counting rule:** These M1 controlled cases can serve as evidence for INC-SD-002 and INC-SD-001 when revisited in M5, but they must **not** be counted as four separate incidents. M5 still requires six distinct scenarios, three fuller RCAs, communication logging, regression reopening and two service requests.

## D. M1 closure note

Two real sandbox failures/discrepancies were deliberately reproduced and validated; the global support process, response targets and handover are **documentation simulations**. The baseline reports SAP training-data metrics, not actual customer incident KPIs. The Module 1 access audit contains explicit unresolved capabilities, which must be handled in later modules or other Learning Hub sandboxes.
