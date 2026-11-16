
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

**Evidence limitations:** Some aggregate monitor counts were supplied as contemporaneous SAP UI readouts rather than preserved screenshot counts. Do not characterize them as screenshot-verified. The cropped IAM screenshot omits user identity. Review all images for publication rights and other sensitive data before making the repo public.

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
4. System/client and execution date
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
