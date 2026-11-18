
# SAP SD Lab - Evidence Register

**Project:** SAP S/4HANA SD Application Support Lab  
**Status:** In progress

## Purpose

Maintain a central record of all evidence produced during the SAP SD practical lab.

Each evidence item must be traceable to a module, requirement, and completed or simulated activity.

## Evidence Register

| Evidence ID | Module | Requirement | Description | Execution Status | Evidence File |
|---|---|---|---|---|---|
| EV-001 | M1 | Access / A01 | 14 assigned business roles list, cropped to exclude user-identifying columns | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/iam-14-roles-crop.png) |
| EV-002 | M1 | A02 / M1.02 | VA01 sales organization 1010/10/00 | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/sales-org-va01.png) |
| EV-003 | M1 | M1.03 | Sales fulfillment issues: 44 issue flags, 40 affected documents | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/sales-fulfillment-monitoring.png) |
| EV-004 | M1 | M1.03 | Manage Outbound Deliveries: 8 ready-for-GI results | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/outbound-delivery-monitoring.png) |
| EV-005 | M1 | A05 / M1.03 | SIT log view: 36 entries | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/situation-log-sit.png) |
| EV-006 | M1 | M1.03 | Billing posting status filter menu; counts supplied in chat | Executed - count not screenshot-proven | [View image](../M1-Landscape-and-Monitoring/evidence/billing-posting-status-filter.png) |
| EV-007 | M1 | M1.03 | Delivery output filters; counts supplied in chat | Executed - count not screenshot-proven | [View image](../M1-Landscape-and-Monitoring/evidence/delivery-output-status-filter.png) |
| EV-008 | M1 | Triage / INC-SD-002 | Third-party item category CB1/purchase requisition diagnostic | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/third-party-item-cb1-pr.png) |
| EV-009 | M1 | Triage / INC-SD-002 | Order 1055 TG11 item TAN and plant 1010 | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/stock-material-tg11-tan.png) |
| EV-010 | M1 | Triage / INC-SD-002 | Negative test: Political Reasons delivery-block error | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/delivery-block-error.png) |
| EV-011 | M1 | Triage / INC-SD-002 | Positive test: sales order 1055 to outbound delivery 80000784 in document flow | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/delivery-positive-document-flow.png) |
| EV-012 | M1 | M1.02 / INC-SD-002 | Outbound delivery 80000784 shipping point 1010 | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/delivery-shipping-point.png) |
| EV-013 | M1 | Triage / INC-SD-002 | Outbound delivery 80000784 checked, not picked, GI not started, not invoiced | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/delivery-processing-status.png) |
| EV-014 | M1 | Triage / INC-SD-001 | Pricing baseline PPR0 EUR 17.55, tax and internal price | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/pricing-baseline.png) |
| EV-015 | M1 | Triage / INC-SD-001 | Pricing Analysis Y10101 PPR0 message 203 manual override | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/pricing-analysis-manual-override.png) |
| EV-016 | M1 | Triage / INC-SD-001 | VA03 order 1056 corrected PPR0 EUR 17.55 | Executed | [View image](../M1-Landscape-and-Monitoring/evidence/pricing-corrected-va03.png) |

| EV-017 | M2 | R02 / O2C-SD-001 | Scenario 1: picked 1 PC, status C — Fully Picked | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-picking-fully-picked.png) |
| EV-018 | M2 | R02 / O2C-SD-001 | Scenario 1: PGI material document 4900001488 in document flow | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-pgi-document-flow.png) |
| EV-019 | M2 | R02 / O2C-SD-001 | Scenario 1: material document 4900001488, 1 PC TG11, reference EUR 13.50 | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-material-document.png) |
| EV-020 | M2 | R02 / O2C-SD-001 | Scenario 1: F2 invoice preview, 1 PC, net EUR 17.55, tax EUR 3.33 | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-billing-f2-preview.png) |
| EV-021 | M2 | R02 / O2C-SD-001 | Scenario 1: accounting-interface error before correction | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-fi-interface-error.png) |
| EV-022 | M2 | R02 / O2C-SD-001 | Scenario 1: customer 1000193 not defined for company code 1010 | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-fi-master-error.png) |
| EV-023 | M2 | R02 / O2C-SD-001 | Scenario 1: customer company codes empty before correction | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-customer-company-code-missing.png) |
| EV-024 | M2 | R02 / O2C-SD-001 | Scenario 1: 1010 / 12100000 / NT30 entered; draft screen (not proof of commit) | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-customer-company-code-draft.png) |
| EV-025 | M2 | R02 / O2C-SD-001 | Scenario 1: invoice 90000303 and FI journal entry 9400000057 | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-billing-fi-success.png) |
| EV-026 | M2 | R02 / O2C-SD-001 | Scenario 1: three balanced FI ledger lines, creator user ID redacted | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc1-fi-ledger-redacted.png) |
| EV-027 | M2 | R02 / O2C-SD-002 | Scenario 2: billing block Check Payment Terms selected in VA02 | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-order-billing-block.png) |
| EV-028 | M2 | R02 / O2C-SD-002 | Scenario 2: confirmed quantity 1 PC, schedule line CP, no schedule-line block | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-atp-confirmed.png) |
| EV-029 | M2 | R02 / O2C-SD-002 | Scenario 2: VL01N reached delivery creation for order 1056 | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-delivery-draft.png) |
| EV-030 | M2 | R02 / O2C-SD-002 | Scenario 2: delivery 80000785, picking, PGI 4900001489 | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-pgi-document-flow.png) |
| EV-031 | M2 | R02 / O2C-SD-002 | Scenario 2: F2 invoice preview despite billing block | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-billing-f2-preview.png) |
| EV-032 | M2 | R02 / O2C-SD-002 | Scenario 2: invoice 90000304, journal entry 9400000058, other journal entries | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-invoice-fi-document-flow.png) |
| EV-033 | M2 | R02 / O2C-SD-002 | Scenario 2: FI ledger balanced, creator user ID redacted | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-fi-ledger-redacted.png) |
| EV-034 | M2 | R02 / O2C-SD-002 | Scenario 2: VA03 shows header billing block still present after invoicing | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-header-block-retained.png) |
| EV-035 | M2 | R02 / O2C-SD-002 | Scenario 2: block 04 persists; fully delivered, GI complete, fully invoiced | Executed — SAP screenshot | [View image](../M2-Order-to-Cash/evidence/m2-sc2-final-status-with-block.png) |

**Evidence limitations:** For EV-017–EV-035, evidence images are captured SAP sandbox screens; original user-facing save confirmations remain in the workshop conversation, not all in screenshots. FI creator user IDs are masked in the two ledger images. The material-document movement type and stock before/after balances are not shown. The negative billing-block test failed and is not a passed control.  Some aggregate monitor counts were supplied as contemporaneous SAP UI readouts rather than preserved screenshot counts. Do not characterize them as screenshot-verified. The cropped IAM screenshot omits user identity. Review all images for publication rights and other sensitive data before making the repo public.

| EV-036 | M3 | R07 | Delivery 80000785 financial processing shows billing block blank and fully invoiced | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-order1056-delivery-no-billing-block.png) |
| EV-037 | M3 | R07 | Sales order 1056 item 10 billing document tab shows billing block blank | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-order1056-item-no-billing-block.png) |
| EV-038 | M3 | R07 | Delivery 80000787 financial processing shows billing block Check Payment Terms before save | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-delivery80000787-billing-block.png) |
| EV-039 | M3 | R02 / R07 | Sales order 1058 document flow confirms PGI material document 4900001490 | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-delivery80000787-post-goods-issue.png) |
| EV-040 | M3 | R07 | Manage Your Solution indicates SAP Central Business Configuration management | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-cbc-tenant-managed.png) |
| EV-041 | M3 | R07 | Order 1058 item 10 PPR0 price 17.55, tax 3.33, cost 13.50 | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-order1058-pricing-values.png) |
| EV-042 | M3 | R07 | PPR0 condition record for material TG11 with validity and scale | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-ppr0-condition-record.png) |
| EV-043 | M3 | R07 | Order 1058 shipping tab: plant 1010, shipping point 1010, weight and delivery tolerances | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-order1058-shipping.png) |
| EV-044 | M3 | R07 | Product plant 1010 loading group Crane and availability check SR | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-material-tg11-loading-group.png) |
| EV-045 | M3 | R07 / R02 | Sales order 1059 quantity 2 PC, value EUR 35.10; learner IDs hidden | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-order1059-2pc-redacted.png) |
| EV-046 | M3 | R07 | Delivery 2 PC with picked quantity 1 PC and status B Partially Picked, before save | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-picking-half-delivery.png) |
| EV-047 | M3 | R07 | Goods issue failure: VLMOVE 030 delivery not yet completely picked | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-pgi-error-vlmove030.png) |
| EV-048 | M3 | R07 | Sales order 1059 to delivery 80000788 and goods issue document 4900001491, status complete | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-pgi-post-correction-document-flow.png) |
| EV-049 | M3 | R07 / R10 | Delivery 80000788 incompletion list empty | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-delivery-incompletion-blank.png) |
| EV-050 | M3 | R07 / R10 | VA03 sales order 1059 confirms Document is complete | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-sales-order-complete-message.png) |
| EV-051 | M3 | R07 | Order 1056 block 04 persists while fully delivered and invoiced | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-order1056-billing-block-final-status.png) |
| EV-052 | M3 | R07 / R02 | Invoice 90000305 item details 1 PC price and tax; no incompletion indicator displayed | Executed — SAP screenshot | [View image](../M3-Configuration-and-Logistics/evidence/m3-billing90000305-item-values.png) |

**M3 evidence limitations:** EV-036–EV-052 are contemporaneous SAP screen images, but some later save confirmations and the separate CBC Unauthorized screen were reported in the workshop conversation, not preserved as screenshot artifacts. EV-038 shows selection before saving; the after-save confirmation was reported by the user. There was **no** FI journal number captured for invoice 90000305. No screenshot establishes exact GI movement type or configuration settings.


## M4 — IDoc, Interface and Output Evidence

| Evidence ID | Module | Requirement | Description | Execution Status | Evidence File |
|---|---|---|---|---|---|
| EV-053 | M4 | R03 | Historical inbound DELFOR 180016, status 56, missing inbound partner-profile error | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/idoc-inbound-delfor-partner-profile-error.png) |
| EV-054 | M4 | R03 | Standard order 374 two completed order confirmation outputs | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/sales-order-374-output-completed.png) |
| EV-055 | M4 | R03 | Standard order 374 ORDER_CONFIRMATION detail; print queue LP01, status completed; metadata redacted | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/sales-order-374-output-details.png) |
| EV-056 | M4 | R03 | Vendor S680-1010 FI role company code 90FR and reconciliation account 21200000 | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/bp-company-code.png) |
| EV-057 | M4 | R03 | VV33 RD04 condition 1010 / C680-90FR, medium 6 and dispatch 4 | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/invoice-output-condition.png) |
| EV-058 | M4 | R03 | OPD IV billing type to S4680_BILLING_DOCUMENT immediately | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/opd-output-type.png) |
| EV-059 | M4 | R03 | OPD S4680_BILLING_DOCUMENT output channel IDOC | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/opd-channel.png) |
| EV-060 | M4 | R03 | WE41 process SD08 assigned function module IDOC_OUTPUT_INVOIC_IV_MM | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/outbound-process-code.png) |
| EV-061 | M4 | R03 | WE20 outbound INVOIC partner C680-90FR basic type INVOIC01 and port A000000003 | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/outbound-partner-parameters.png) |
| EV-062 | M4 | R03 | WE20 V3 RD00 message control linked to SD08 | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/outbound-message-control.png) |
| EV-063 | M4 | R03 | WE20 inbound S680-1010 LI INVOIC process code INVF | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/inbound-partner-parameters.png) |
| EV-064 | M4 | R03 | WEL1 logical address 1010C680-90FR maps 90FR to S680-1010 | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/supplier-assignment.png) |
| EV-065 | M4 | R03 | MM EDI tax conversion for supplier S680-1010 | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/tax-code-mapping.png) |
| EV-066 | M4 | R03 | MM EDI program parameters company code 90FR, KR / KG | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/invoice-program-parameters.png) |
| EV-067 | M4 | R03 | OBCB goods/services wildcard mapped to G/L 51600000 | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/fi-edi-gl-accounts.png) |
| EV-068 | M4 | R03 | OBCE invoice posting keys, document types and tax code | Verified SAP observation; not recovery | [View image](../M4-IDocs-Interfaces-and-Output/evidence/fi-edi-program-parameters.png) |
| EV-069 | M4 | R03 | FB03 KR filter, own-document search in company code 90FR returned no items | Verified SAP observation; no invoice | [View image](../M4-IDocs-Interfaces-and-Output/evidence/fb03-company-90fr-no-kr-result.png) |
| EV-070 | M4 | R03 | Wider FB03 KR document list contained only other company codes (date columns cropped) | Verified SAP observation; no 90FR document | [View image](../M4-IDocs-Interfaces-and-Output/evidence/fb03-other-company-kr-documents-crop.png) |

**Evidence boundary:** EV-053 is a pre-existing IDoc diagnosed read-only, not an induced failure. EV-054–EV-055 are completed PRINT output for a sales order, not an IDoc. EV-056–EV-068 document configuration inspected in SAP; EV-069–EV-070 document the unavailable 90FR invoice prerequisite; no new `INVOIC` message, FI invoice or successful IDoc recovery is claimed.

## Evidence Categories

- SAP screenshots and transaction records
- Order-to-Cash document flows
- Configuration analysis and change records
- Incident investigation and RCA reports
- IDoc, interface, and application log evidence
- Unit, integration, and UAT test results
- Release and validation documentation
- Authorization and audit records
- Business communication and training materials

## Evidence Standards

Each evidence item should record:

1. Unique evidence ID
2. Related module and requirement
3. SAP transaction or Fiori application
4. System/client and evidence context
5. Business scenario or technical problem
6. Expected and actual results
7. Investigation or execution details
8. Supporting screenshot or document
9. Final status and validation

## Execution Status

- **Executed:** Activity performed in SAP
- **Simulated:** Documented without SAP execution
- **Blocked:** Activity could not be performed
- **Not Started:** No evidence collected

## Evidence Storage

Supporting files will be stored within their respective module folders.

Every evidence file should be referenced from this register and the relevant module documentation.

## Confidentiality

Only anonymized and publication-permitted SAP training evidence should be stored in this repository.

Passwords, credentials, personal data, and confidential system information must not be included.
