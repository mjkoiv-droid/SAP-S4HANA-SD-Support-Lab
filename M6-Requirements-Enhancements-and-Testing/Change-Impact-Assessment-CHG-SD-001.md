# CHG-SD-001 — Change impact assessment

**Status:** Proposed analytical assessment only; **no authorized change, transport, real approval or rollback**. Based on [functional specification](Functional-Specification-CHG-SD-001.md) and open [problem PRB-SD-001](../M5-Incident-and-Root-Cause-Management/Problem-Record-PRB-SD-001.md).

## Business case

A payment-terms billing hold is expected by the proposed business scenario but did not prevent delivery-related F2 invoices for the four source/level variants actually tested in JV2. The business definition, correct SAP control design and JV2 root cause are **unverified**. Potential risk is unintended billing/AR posting during review, **not any demonstrated real-world loss**. Conversely, a poorly scoped global fix may stop legitimate invoices.

## Change scope / design alternatives

| Area | Verified starting point | Candidate impact / action (not implemented) |
|---|---|---|
| Scope | OR/TAN/TG11, sales area 1010/10/00, plant 1010, customer 1000193 | Restrict proposed change to approved entities/business process; broader scope to be evaluated |
| Billing block 04 | Selectable at order/delivery levels in JV2 | Define level and meaning with business owners |
| F2 billing configuration | JV2 CBC read permission denied | Authorized JV2 display of relevant billing-type/block mapping and copy requirements; only then select remedy |
| T41 IMG | 04→F2 mapping observed in T41/400, EV-082 | **Not proof** of JV2 settings; no transport/copy between systems assumed |
| Pricing | PPR0 / EUR 17.55 baseline in controlled sample | No change proposed; unblocked regression check after fix |
| Master data | Existing sample customer/material usable | No master-data change indicated |
| Security | No release-role analysis performed | Review set/clear privileges, audit trail, maker/checker and approvals |

## Cross-functional change impact

| Function | Potential impact | Severity if misconfigured | Required owner action |
|---|---|---|---|
| Sales | Hold entry/release and customer communication | High | Confirm eligibility and exception owner |
| Logistics | Delivery creation, picking and PGI should follow agreed shipment policy | Medium | Clarify whether shipping proceeds while invoice held |
| Billing | Due-list selection, F2 creation, cancellation/duplicates | High | Validate block and release acceptance criteria |
| FI | AR, tax, revenue postings and reconciliation | High | Confirm no postings from blocked invoices; verify post-release correctness |
| MM / stock | PGI may post independently of invoice | Medium | Validate no unintended effect on inventory/COGS |
| Outputs and interfaces | Delayed/repeated invoice messages | Medium | Define monitoring and duplicate prevention; no new executed M6 interface work |
| Reporting | Billing holds and aging KPIs may change | Medium | Define due-list/status validation |
| SoD/security | Release bypasses hold if assigned too broadly | High | Approve role separation and audit controls |

## Risks and mitigations

| ID | Risk | Probability | Impact | Proposed mitigation |
|---|---|---|---|---|
| RSK-M6-01 | Assuming JV2 configuration from T41 | Unknown | High | Obtain JV2 authorized read-only evidence before change |
| RSK-M6-02 | Overblocking valid F2 documents | Unknown | High | Targeted technical design, isolated unit/regression tests |
| RSK-M6-03 | Block bypass/weak approval chain | Unknown | High | Role/SoD review and audit-friendly release workflow |
| RSK-M6-04 | Duplicate invoice/FI/output after release | Unknown | High | Single-invoice reconciliation and repeat-attempt test |
| RSK-M6-05 | Incorrectly claiming defect fixed from negative tests alone | Known documentation risk | Medium | Preserve failed-control status and pending post-change tests |

## Dependencies, relative effort and priority

| Work package | Relative complexity (not an estimate of duration) | Owner type | Status |
|---|---|---|---|
| Decide business rule and approved source/level | Medium | Sales/Finance/Logistics | Pending; stakeholder role-play only |
| JV2 CBC display/diagnostic review | Medium | Authorized configuration owner | **Blocked by current CBC access** |
| Confirm valid technical intervention | Uncertain | SD specialist | Not started |
| Implement approved isolated sandbox change | Uncertain | Authorized change owner | Not started |
| Post-change unit, integration, negative and regression | Medium | SD/FI/logistics testers | Not started |
| Business UAT / release approval | Medium | Actual business owners | Not started |

**Priority (proposed):** High for business-control clarification; final severity and urgency require real business assessment. Do not confuse with an actual incident SLA classification.

## Rollback / forward fix

Retain a validated JV2 configuration snapshot before any approved change. Restore only via the authorized mechanism and approved instructions if the change causes unintended holds; reconcile unbilled documents, invoices, FI entries, output queues and duplicates, and rerun targeted checks. If rollback is unsuitable, document forward fix and owner. **No rollback performed** because **no change was made**.

## Approval-style record

| Role | Review outcome |
|---|---|
| Sales, Logistics, Finance | Fictional consultation points documented; **no real review or sign-off** |
| Configuration owner | Inspection blocked; no approved design |
| Change manager | No approval |
| Test/UAT approver | No post-change/UAT acceptance |

**Recommendation:** Complete diagnosis/approval in an authorized sandbox before any alteration. Until then this remains a **documented proposal supported by executed pre-change negative tests**, not a validated remedy.
