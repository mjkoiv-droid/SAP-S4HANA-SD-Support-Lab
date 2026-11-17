# M2 — Order-to-Cash (O2C) Processing

**SAP execution status (17 November 2026):** **Two complete O2C document chains executed and verified through FI posting** in the JV2/100 SAP S/4HANA Cloud Public Edition training sandbox. The billing-block enforcement test in Scenario 2 **failed** and remains an open M3 investigation. Some peripheral technical fields and stock before/after counts remain unverified.

## Objective and scope

Execute and verify order creation, pricing, availability, picking, outbound delivery, PGI, billing, SD–FI integration, document flow and two tenant-supported variations. Document real exceptions without claiming unperformed activities. **No production client work.**

## Executed scenarios

| Scenario | Sales order | Delivery | PGI material doc | Invoice | FI RV journal | O2C result | Exception |
|---|---|---|---|---|---|---|---|
| [01 — Standard sale + FI master correction](O2C-Scenario-01-Standard-and-FI-Correction.md) | 1055 | 80000784 | 4900001488 | 90000303 | 9400000057 | **PASS** | Initial missing company-code 1010; resolved |
| [02 — Billing-block exception](O2C-Scenario-02-Billing-Block-Exception.md) | 1056 | 80000785 | 4900001489 | 90000304 | 9400000058 | **PASS** | Block 04 persisted yet invoice posted; **control FAIL / open** |

Both FI documents show customer receivable debit **EUR 20.88** and credits **EUR 17.55 revenue + EUR 3.33 output tax**. Payment and AR clearing were not performed.

## Working files

- [Scenario 1 process trace — executed](O2C-Scenario-01-Standard-and-FI-Correction.md)
- [Scenario 2 process trace — executed, billing block negative test failed](O2C-Scenario-02-Billing-Block-Exception.md)
- [Executed Sales → Logistics → Finance swimlane](O2C-Executed-Swimlane-and-Controls.md)
- [Process control and reconciliation checklist](O2C-Process-Control-Checklist.md)
- [Reusable O2C process trace template — documentation only](O2C-Process-Trace-Template.md)
- [Central evidence register (EV-017–EV-035)](../00-Project-Tracking/Evidence-Register.md)

## Outcomes and verification boundaries

1. **Executed:** Sales order, picking, PGI material document, billing and balanced RV journal for both scenarios.
2. **Executed / resolved:** Missing FI customer company-code data for BP 1000193; added company code 1010 with receivables reconciliation account and payment terms; invoice 90000303 subsequently posted.
3. **Executed / unresolved:** Sales-order billing block **04 — Check Payment Terms** remained active while delivery-related invoice **90000304** was created and posted. Configuration cause not established. Handoff to **M3** for controlled investigation.
4. **Not verified:** Movement type, delivery type, explicit before-and-after stock balance, complete credit-check scope, and customer receipt/clearing. No claim that these activities were performed.

**Evidence handling:** The retained screenshots are genuine SAP sandbox views. Journal-entry screenshots have the creator's account identifier masked; posted amounts and document numbers remain unaltered. The primary source of several save messages is the contemporaneous user-reported SAP confirmation in the workshop conversation.

**GitHub rule:** Keep repository private while the portfolio remains under execution and final validation. M2 evidence was uploaded and verified against a downloaded repository ZIP; repository privacy and current live GitHub state still require separate confirmation.
