# M5 — Service request register (proposed, not submitted)

These are **documentation-only service-request exercises**. They are not actual tickets raised to an SAP operations team and have no real approvals, SLAs or change implementations. The purpose is to distinguish a routine request from an incident.

## SR-SD-001 — Request a new billing variant

| Field | Proposed request |
|---|---|
| Type | Service request / change enablement, **not** a current system failure |
| Requested outcome | Approved and tested billing-list variant for the intended F2 billing work queue |
| Business owner | Billing process owner — fictional role placeholder |
| Scope | Confirm fields/filters, company code/sales org, relevant billing types/statuses, display permissions and naming convention |
| Existing evidence | M1 billing-monitoring view EV-006, M2 F2 invoice 90000303 and related status |
| Constraints | Do not alter shared master data, customizing or another user's personal variants |
| Implementation status | **Proposed only; not executed** |

**Suggested acceptance:** The requester confirms the criteria and receives a read-only or own-user variant that (a) filters expected relevant billing documents, (b) preserves access boundaries, and (c) works for an independent verification sample. No variant creation, approval or real user acceptance was performed.

**Action workflow (simulation):** Clarify requirement → access/owner approval → owner implements permitted personal/shared variant → requester verifies → close. Every arrow represents a proposed step, not a recorded transaction.

## SR-SD-002 — Request authorized read-only CBC diagnostic access

| Field | Proposed request |
|---|---|
| Type | Access service request arising from actual denial [INC-SD-006](Incident-INC-SD-006-CBC-Access.md) |
| Requested outcome | Least-privilege, approved ability to inspect JV2 CBC configuration activity 102401 for billing-block analysis |
| Current observation | CBC is managing tenant configuration; launch returns **Unauthorized** (EV-079–EV-080) |
| Impact | Unable to verify JV2 billing-block to F2 assignment as part of [PRB-SD-001](Problem-Record-PRB-SD-001.md) |
| Owner / approver | Authorized CBC administrator / IAM owner — role placeholders, **not contacted** |
| Security control | Verify identity, tenant assignment, exact permissions and SoD before granting any access |
| Modification request | **Read-only diagnostic scope**, if supported; do not request blanket CBC editing rights |
| Implementation status | **Not submitted; no role change** |

**Acceptance test (not executed):** Admin confirms approved scope → user launches *JV2* CBC successfully → accesses permitted configuration screen read-only → capture evidence of the actual assignment → access review/expiry per owner policy. T41/400 IMG access cannot substitute for JV2 CBC authorization.

## Service request versus incident distinction

`SR-SD-001` asks for optional capability; it is **not an incident**. `SR-SD-002` requests support access to investigate an **actual denied operation** and should remain linked to open incident `INC-SD-006`, without presenting the request as granted.
