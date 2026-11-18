# M4 — IDoc / Interface Recovery Runbook

**Classification:** Documented recovery simulation and support procedure, not an executed configuration repair or retest.

## Initial triage and ownership

| Classification | Observable symptom | Primary check | Escalation owner |
|---|---|---|---|
| Partner-profile mismatch | Status `56`, e.g. inbound `DELFOR` `180016` | `WE02` control/status, `WE20` inbound entry | Integration/EDI + SAP SD |
| Application/business data | Status `51` and application message | `WE02`, master data, related document and `SLG1` | SD/MM/FI functional owner |
| Port/RFC handoff | Outbound status `03` only proves handoff, not target posting | `WE21`, RFC destinations, receiving IDoc/status | Integration/Basis |
| Billing invoice integration | Missing or rejected `INVOIC` invoice | `OPD`, `WE20`, `WEL1`, `OBCB`, `OBCE`, `FB03`, `WLF_IDOC` | SD + FI + integration |
| Output delivery | Failed order-confirmation print output | Order output status, recipient, form and queue | SD + output operations |

## Controlled recovery steps (not executed in this lab)

1. Capture the original IDoc and status message, direction, message type, basic type, sender/receiver partner and relevant business reference.
2. Locate downstream documents and compare source references to determine whether processing already succeeded elsewhere.
3. Check the specific configuration dimension implicated by the error (`WE20` partner, `WE21` port/RFC, business-partner master, mapping, tax/G/L keys or output rule). Do not replace investigation with broad configuration changes.
4. Obtain business/technical owner approval; in shared sandbox or production do not change a profile or reprocess a historical IDoc without authorization.
5. In an isolated test case, change **only** the confirmed defect, process the authorized IDoc through the correct supported workflow (`BD87` only where appropriate), then verify the new status and application document.
6. Confirm the interface partner/document correlation, posting values, absence of duplicates, and correct final output. Capture evidence of both negative and positive results.
7. If no authorized correction or valid replay is possible, retain the original error and stop at **diagnosis only**. Do not label the interface recovered.

## Example for the observed status 56

- **Observed:** `DELFOR` `180016`, status `56`, message **EDI: Inbound partner profile does not exist**.
- **Proposed:** Cross-check the control-record logical-system partner with the inbound `DELFOR` entry in `WE20`, including relevant code/function dimensions. An owner would decide whether the missing/mismatched profile should be corrected.
- **Not performed:** No partner-profile write, no replay, no new IDoc, no receiving sales/forecast document and no positive retest.

## Validation matrix

| Validation check | Status |
|---|---|
| Historical inbound error and status captured | Verified |
| Intercompany billing/INVOIC partner and FI configuration inspected | Verified |
| Sales-order output completed for order `374` | Verified |
| New inbound failure introduced under controlled conditions | Not executed |
| Root cause configuration changed with approval | Not executed |
| Reprocessing/status success after correction | Not executed |
| Invoice/posting and duplicate reconciliation after recovery | Not executed |

**Closure classification:** M4 support investigation and documentation completed; live IDoc recovery **unverified**. This distinction prevents a paper procedure from being mistaken for a tested fix.
