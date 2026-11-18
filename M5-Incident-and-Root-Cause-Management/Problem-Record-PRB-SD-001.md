# PRB-SD-001 — Billing block 04 not preventing F2 billing in JV2

| Field | Result |
|---|---|
| Classification | **Actual negative control results; root cause unresolved; T41 inspection is not JV2 proof** |
| System/client experiencing symptom | JV2 / 100 |
| Independent reference system | T41 / 400 — read-only IMG, not same customizing |
| Related investigation | [M3 Billing-Block Behavior](../M3-Configuration-and-Logistics/Billing-Block-Behavior-Investigation.md) |
| Related change proposal | [CHG-M3-001](../M3-Configuration-and-Logistics/Change-Proposal-CHG-M3-001.md) |
| Access constraint | [INC-SD-006](Incident-INC-SD-006-CBC-Access.md), CBC Unauthorized |
| New evidence | **EV-079–EV-082** |
| Status | **Open** — no authorized JV2 configuration review or fix |

## Problem statement

A billing control intended to block invoicing with reason **04 — Check Payment Terms** did **not** stop the tested delivery-related F2 invoices in JV2. This is a **control test failure** (business expectation versus observed behavior), not an FI posting failure. Two actual negative scenarios were recorded in M3:

- **Order-header block:** Order `1056` retained reason 04 after invoice `90000304` and FI journal `9400000058` were created. Item and delivery-level blocks were blank (EV-036, EV-037, EV-051).
- **Delivery-header block:** Reason 04 was selected/saved on delivery `80000787`; invoice `90000305` was created after PGI. Saved block persistence is supported by user report and selection evidence (EV-038), without an independent after-save image. See EV-039 and EV-052. FI journal ID/ledger for 90000305 were not captured.

**Important:** Neither result establishes what IMG/CBC assignment should or does exist **in JV2**. Header, item, delivery, requirements and copy-control semantics are not fully established.

## Separate-system IMG inspection

Read-only `SPRO → SAP Reference IMG → Sales and Distribution → Billing → Billing Documents → [Blocking Reasons assignment]` in **T41 / client 400** showed:

- `01 — Calculation Missing` assigned to `F2` (**EV-081**).
- `04 — Check Payment Terms` assigned to `F2` (**EV-082**).

This confirms **T41's** assignment, **not JV2's**. It does not prove the observed JV2 control failure is a missing assignment or a SAP software defect.

## Causal hypotheses (not confirmed)

| Candidate | What would verify | Current status |
|---|---|---|
| JV2 102401 assignment absent/different | Authorized read-only JV2 CBC activity display | Blocked by CBC Unauthorized |
| Block level/requirements in delivery-related billing | Compare header/item/delivery and relevant requirements in JV2 | Not established |
| Billing copy control or BAdI behavior | Authorized configuration analysis with owner | Not established |
| User action/data persistence issue | Reproduce with saved-state screenshots, controlled new documents | Earlier cases partially captured; no further test |

## Risk, ownership and action plan

**Potential risk:** Billing may proceed despite an intended payment-terms check. No actual loss, financial impact, production exposure or real business severity is measured.

**Workaround recommendation — not implemented:** Do not rely on this unverified block alone as a preventive payment-terms control; use approved manual billing checks until the configuration owner evaluates it. This is advice for a hypothetical support operation, not an implemented control.

**Next authorized path:** Route [SR-SD-002](Service-Requests.md) for narrow JV2 CBC access; review exact JV2 assignment and billing requirements; propose any needed change through change approval; retest the negative blocking case and a positive unblocked invoice; document whether the observed behavior is intended design or a defect. No role/configuration change has been made.

## Problem closure criterion

Do **not** close until root cause is actually demonstrated in JV2, approved corrective action or accepted design behavior documented, and relevant negative/positive regression tests have system evidence. Currently **Open**.
