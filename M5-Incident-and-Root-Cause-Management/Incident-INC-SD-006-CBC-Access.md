# INC-SD-006 — Unauthorized access to Central Business Configuration

| Field | Recorded result |
|---|---|
| Classification | **Actual access denial reproduced; unresolved; cause not established** |
| System/client | JV2 / 100 (application launch); second system T41 / 400 used for independent read-only IMG inspection |
| Access path | Manage Your Solution → SAP Central Business Configuration (CBC) |
| Symptom | **Unauthorized** in the CBC application |
| Evidence | **EV-040, EV-079–EV-082** |
| Real-world role/approval owner | Not established; no actual authorization change requested or approved |

## Problem and observed business effect

The JV2 tenant's configuration is managed through CBC, as stated in **Manage Your Solution**. Following the CBC link produces **Unauthorized**. Therefore the training user could not inspect configuration activity **102401 — Assign Blocking Reasons to Billing Types** in JV2, limiting root-cause investigation of the billing-block anomaly.

## Diagnosis and boundaries

1. Reopened Manage Your Solution in JV2: CBC-managed configuration confirmed (**EV-079**; M3 **EV-040**).
2. Followed CBC link: explicit **Unauthorized** response (**EV-080**). Reproduced the earlier observation.
3. Used separate SAP GUI training system **T41/400**, entered `/nSPRO`, opened the IMG blocking-reasons assignment table read-only. Verified block `01` to F2 (**EV-081**) and block `04 — Check Payment Terms` to F2 (**EV-082**).
4. **System boundary:** T41/400 configuration does **not** prove what is configured in JV2/100 and does not repair a JV2/BTP identity or role entitlement issue.

**Unverified root cause:** Missing CBC identity, role assignment, business catalog, tenant entitlement, or other access configuration. No authorization trace or CBC administrator review was completed; SAP GUI `SU53` in T41 would not by itself diagnose separate CBC application access.

## Corrective request, acceptance and closure

Route [SR-SD-002](Service-Requests.md) to the authorized CBC/access administrator to check identity, tenant membership and least-privilege permission required for **read-only investigation**, then repeat access with appropriate approval and log evidence.

**Status:** **Open / not remediated.** This is a verified denial, not an established missing-role cause. No configuration changes, user-role changes or unauthorized bypass were attempted.

## Investigation standard

- **Training context:** These are training-sandbox observations, not customer production incidents. Impact, severity, roles, and communications are scenarios unless a system effect was actually observed.
- **Evidence standard:** A screenshot of successful status alone does not prove how a prior failure was corrected. Where a previous module documented the negative test and correction, both are linked. No unexecuted action is described as complete.
