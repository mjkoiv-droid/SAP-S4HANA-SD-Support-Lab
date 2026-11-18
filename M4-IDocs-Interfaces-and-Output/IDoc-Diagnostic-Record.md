# IDoc Diagnostic Record — Inbound Partner-Profile Error

**Case:** `IDOC-SD-M4-001`  
**System:** SAP GUI training system T41, client 400  
**Execution type:** Read-only inspection of an existing IDoc  
**Observed outcome:** Diagnosis verified; corrective change and retest **not performed**.

## Actual error and control information

| Field | Observed value |
|---|---|
| IDoc number | `180016` |
| Message type | `DELFOR` |
| Basic type | `DELFOR02` |
| Direction | `2` — inbound |
| Status | `56` |
| Error detail | **EDI: Inbound partner profile does not exist** |
| Sender/partner number shown | `HE4CLNT400` |
| Partner type | `LS` (logical system) |
| Port shown | `SAPT41` |
| Structure | 9 data records, including header `E1EDK09`, partner `E1EDKA1` and item `E1EDP10`/`E1EDP16` segments |
| Evidence | [SAP IDoc display](evidence/idoc-inbound-delfor-partner-profile-error.png) |

## Diagnostic interpretation

The status record reports that the receiving IDoc processing could not resolve the required inbound partner profile. This points to a partner-profile/configuration mismatch for the sender and message combination; no additional application posting should be inferred.

The observed error is a **real pre-existing message in the shared training data**, not a defect deliberately injected into a new case. Partner-profile review using `WE20` and associated IDoc-interface tools was part of the diagnostic work. No profile was changed as part of this exercise.

A separate existing outbound `DELFOR` IDoc `180015` had status `03` (data passed to port). This indicates successful handoff to the port, **not** proof that a receiving SAP application created its corresponding business document. The outbound and inbound IDoc numbers are not asserted to be a confirmed paired end-to-end correlation.

## Root cause and recovery status

- **Confirmed symptom:** Inbound IDoc status `56` and missing inbound partner-profile message.
- **Supported hypothesis:** Required inbound `WE20` partner/message matching was absent or inconsistent at processing.
- **Unverified factors:** Whether the partner was genuinely absent in the active client or another selection dimension prevented matching; no authorized configuration change and repeated processing took place.
- **Required corrective path:** Validate exact control-record fields against `WE20`, secure change authorization, correct the specific mismatch in a disposable test environment, then process one authorized test message and reconcile downstream posting.
- **Actual closure:** **Diagnosis only.** No executed fix, BD87 reprocessing or successful post-recovery status.

See [Interface Recovery Runbook](Interface-Recovery-Runbook.md) for the documented process, evidence checks and duplicate-prevention controls.
