# INC-SD-004 — Inbound DELFOR partner-profile error

| Field | Recorded result |
|---|---|
| Classification | **Verified read-only diagnosis of pre-existing IDoc; correction/reprocessing not executed** |
| System/client | T41 / 400 (SAP GUI training system) |
| Transactions | WE02/WE05 and WE20 configuration inspection; BD87 and WE19 not executed for this case |
| Document | Inbound IDoc `180016`, message `DELFOR`, basic type `DELFOR02` |
| Status | `56` |
| Error | **EDI: Inbound partner profile does not exist** |
| Evidence | **EV-053**, [M4 IDoc diagnostic](../M4-IDocs-Interfaces-and-Output/IDoc-Diagnostic-Record.md) |

## Business and technical problem

IDoc processing stopped at partner-profile validation. Message processing cannot safely be called complete; no downstream sales scheduling transaction was verified. This IDoc was already present in shared training data and was **not** generated, altered or failed deliberately in M5.

## Diagnostic record

| Observation | Result |
|---|---|
| Direction | `2` inbound |
| Partner / sender shown | `HE4CLNT400`, type `LS` |
| Port | `SAPT41` |
| Message/status | `DELFOR` / `56` |
| Error detail | Inbound partner profile not found |
| Status of separate outbound IDoc `180015` | `03`, handed to port; **not proof** of paired downstream receipt |

**Working diagnosis:** The runtime control-record/sender/message combination did not resolve an applicable inbound partner profile. The exact missing selection or profile/configuration dimension was **not confirmed**; a separate outbound IDoc should not be treated as proof of successful end-to-end processing.

## Recovery proposal — not executed

1. Confirm allowed test IDoc and protect against duplicate application posting.
2. Compare exact sender/partner type/message/control record against WE20 inbound definition.
3. Seek owner and configuration/change approval for any required fix.
4. In a disposable authorized test scenario, retry **one** message; verify new IDoc status and target business posting; reconcile duplicates.

No WE20 change, BD87 reprocessing, WE19 replay, target posting or success claim occurred. This case is **Open — diagnosed only**, with no business SLA/priority measured. [M4 recovery runbook](../M4-IDocs-Interfaces-and-Output/Interface-Recovery-Runbook.md) is a procedure, not an executed recovery.

## Investigation standard

- **Training context:** These are training-sandbox observations, not customer production incidents. Impact, severity, roles, and communications are scenarios unless a system effect was actually observed.
- **Evidence standard:** A screenshot of successful status alone does not prove how a prior failure was corrected. Where a previous module documented the negative test and correction, both are linked. No unexecuted action is described as complete.
