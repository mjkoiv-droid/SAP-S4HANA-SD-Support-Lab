
# SAP SD - Change Impact Assessment

## 1. Change Information

| Field | Value |
|---|---|
| Change Request ID | CHG-SD-001 |
| Change Title | |
| Related Functional Specification | |
| SAP Module | SD |
| Change Type | Configuration / Master Data / Enhancement |
| Assessor | Mikko Koivistoinen |
| Status | Draft |
| Execution Type | Executed / Proposed / Simulated |

## 2. Business Change Overview

**Current business problem:**

**Requested change:**

**Business justification:**

**Expected business benefits:**

**Consequences of not implementing the change:**

## 3. Organizational Scope

| Organizational Element | Affected Values | Impact |
|---|---|---|
| Company Code | | |
| Sales Organization | | |
| Distribution Channel | | |
| Division | | |
| Plant | | |
| Shipping Point | | |

## 4. SAP Configuration Impact

| Configuration Object | Current Setting | Proposed Setting | Impact | SPRO Path / Transaction |
|---|---|---|---|---|
| Sales Document Type | | | | |
| Item Category | | | | |
| Schedule Line Category | | | | |
| Pricing Procedure | | | | |
| Condition Type | | | | |
| Shipping Point Determination | | | | |
| Copy Control | | | | |
| Billing Configuration | | | | |
| Account Determination | | | | |

## 5. Business Process Impact

| Process Area | Potential Impact | Severity | Required Action |
|---|---|---|---|
| Sales Order Entry | | | |
| Pricing and Discounts | | | |
| Availability / Scheduling | | | |
| Outbound Delivery | | | |
| Picking / PGI | | | |
| Billing | | | |
| FI Accounting | | | |
| Returns / Credit Memos | | | |

## 6. Cross-Module Integration Impact

### SD — MM Integration

**Inventory and logistics impact:**

**Stock movement or availability implications:**

### SD — FI Integration

**Revenue accounting impact:**

**Tax and account determination impact:**

### Interfaces and Output

**IDoc/interface dependencies:**

**Output determination and document generation:**

### Reporting and Analytics

**Affected reports, KPIs, or downstream data:**

## 7. Master Data Impact

| Master Data Object | Required Change | Risk | Owner |
|---|---|---|---|
| Business Partner / Customer | | | |
| Material Master | | | |
| Condition Records | | | |
| Partner Functions | | | |
| Other | | | |

## 8. Authorization and Control Impact

**Required authorizations:**

**Affected user roles:**

**Segregation-of-duties risks:**

**Audit and compliance implications:**

## 9. Risk Assessment

| Risk ID | Description | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| RISK-001 | | | | |
| RISK-002 | | | | |
| RISK-003 | | | | |

## 10. Testing and Regression Requirements

| Test ID | Test Type | Scenario | Expected Result | Priority |
|---|---|---|---|---|
| TC-SD-001 | Unit | | | |
| TC-SD-002 | Integration | | | |
| TC-SD-003 | Negative | | | |
| TC-SD-004 | Regression | | | |
| TC-SD-005 | UAT | | | |

## 11. Implementation Dependencies

**Prerequisite configuration:**

**Required master data:**

**Transport dependencies:**

**External system dependencies:**

**Implementation sequence:**

## 12. Rollback and Recovery

**Rollback feasibility:**

**Rollback procedure:**

**Data or transaction recovery requirements:**

**Forward-fix alternatives:**

**Post-rollback validation:**

## 13. Effort and Priority Assessment

| Activity | Estimated Effort | Responsible Role |
|---|---|---|
| Requirements clarification | | |
| Configuration / Development | | |
| Unit testing | | |
| Integration testing | | |
| UAT | | |
| Release preparation | | |
| Post-release validation | | |

**Overall change priority:**

**Overall risk level:**

**Implementation recommendation:**

## 14. Stakeholder Review

| Role | Name | Review Status | Comments |
|---|---|---|---|
| Sales | | Pending | |
| Logistics | | Pending | |
| Finance | | Pending | |
| SAP SD Consultant | | Pending | |
| Change Manager | | Pending | |

## 15. Supporting Evidence

| Evidence ID | Description | File / Link |
|---|---|---|
| EV-XXX | Existing configuration | |
| EV-XXX | Business process evidence | |
| EV-XXX | Proposed configuration | |
| EV-XXX | Test and validation evidence | |

---

**Evidence integrity:** Distinguish verified SAP system behavior from proposed changes, assumed impacts and simulated approvals. Record actual configuration changes only when executed in an authorized training environment.
