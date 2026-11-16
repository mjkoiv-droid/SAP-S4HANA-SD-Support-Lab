
# SAP SD — Configuration Analysis Report

## 1. General Information

| Field | Value |
|---|---|
| Analysis ID | CFG-SD-XXX |
| Analysis Title | |
| SAP Module | SD |
| SAP System / Client | |
| SAP Version | |
| Analysis Date | |
| Analyst | Mikko Koivistoinen |
| Status | Not Started |
| Execution Type | Executed / Read-Only / Simulated / Blocked |
| Related Incident / Change | |
| Evidence IDs | |

## 2. Analysis Objective

**Business process:**

**Configuration area:**

**Reason for investigation:**

**Expected system behavior:**

**Actual system behavior:**

## 3. Organizational Scope

| Organizational Element | SAP Value |
|---|---|
| Company Code | |
| Sales Organization | |
| Distribution Channel | |
| Division | |
| Plant | |
| Shipping Point | |
| Sales Area | |

## 4. Sales Document Configuration

### 4.1 Sales Document Type

**Transaction:** VOV8

| Setting | Current Value | Explanation |
|---|---|---|
| Sales Document Type | | |
| Document Category | | |
| Number Range | | |
| Delivery Block | | |
| Billing Block | | |
| Pricing Procedure Indicator | | |
| Delivery Type | | |

### 4.2 Item Category Determination

**Transaction:** VOV7 / VOV4

| Parameter | Value |
|---|---|
| Sales Document Type | |
| Item Category Group | |
| Usage | |
| Higher-Level Item Category | |
| Determined Item Category | |
| Billing Relevance | |
| Schedule Line Allowed | |

### 4.3 Schedule Line Category

**Transaction:** VOV6 / VOV5

| Parameter | Value |
|---|---|
| Item Category | |
| MRP Type | |
| Schedule Line Category | |
| Movement Type | |
| Availability Check | |
| Transfer of Requirements | |

**Configuration findings:**

## 5. Pricing Configuration

### 5.1 Pricing Procedure

**Transaction:** V/08

| Parameter | Value |
|---|---|
| Pricing Procedure | |
| Sales Area | |
| Customer Pricing Procedure | |
| Document Pricing Procedure | |

### 5.2 Pricing Conditions

| Condition Type | Description | Access Sequence | Requirement | Result |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

### 5.3 Condition Records

**Transaction:** VK13 or available Fiori equivalent

**Customer / Material:**

**Condition validity:**

**Pricing analysis findings:**

**Potential configuration or master data issue:**

## 6. Shipping and Delivery Configuration

### 6.1 Shipping Point Determination

| Parameter | Value |
|---|---|
| Shipping Condition | |
| Loading Group | |
| Delivering Plant | |
| Determined Shipping Point | |

### 6.2 Delivery Configuration

| Parameter | Value |
|---|---|
| Delivery Type | |
| Delivery Item Category | |
| Picking Relevance | |
| Storage Location | |
| Goods Movement Type | |

### 6.3 Delivery Exceptions

**Observed problem:**

**Relevant configuration:**

**Master data dependencies:**

**Diagnostic findings:**

## 7. Billing and Copy Control

### 7.1 Billing Configuration

| Parameter | Value |
|---|---|
| Billing Type | |
| Billing Relevance | |
| Billing Block | |
| Account Determination | |
| Posting Block | |

### 7.2 Copy Control

**Relevant transactions:** VTAA / VTLA / VTFL / VTFA, as applicable

| Source Document | Target Document | Copying Requirement | Findings |
|---|---|---|---|
| | | | |
| | | | |

### 7.3 SD–FI Integration

**Revenue account determination:**

**Tax determination:**

**Accounting document impact:**

**Relevant configuration findings:**

## 8. Configuration Dependency Analysis

| Configuration Object | Dependent Object / Process | Potential Impact |
|---|---|---|
| Sales Document Type | | |
| Item Category | | |
| Schedule Line Category | | |
| Pricing Procedure | | |
| Shipping Point | | |
| Delivery Type | | |
| Billing Type | | |
| Account Determination | | |

## 9. Identified Issues

| Issue ID | Configuration Area | Observed Problem | Root Cause / Finding |
|---|---|---|---|
| CFG-ISS-001 | | | |
| CFG-ISS-002 | | | |

### Issue 1 — Detailed Investigation

**Symptom:**

**Relevant SAP error / message:**

**Diagnostic transactions:**

**Configuration dependency:**

**Root cause or working hypothesis:**

**Recommended correction:**

### Issue 2 — Detailed Investigation

**Symptom:**

**Relevant SAP error / message:**

**Diagnostic transactions:**

**Configuration dependency:**

**Root cause or working hypothesis:**

**Recommended correction:**

## 10. Proposed or Executed Configuration Changes

| Object | Before | After / Proposed | Execution Status | Evidence ID |
|---|---|---|---|---|
| | | | | |
| | | | | |

**Change authorization:**

**Transport requirement:**

**Implementation dependencies:**

**Rollback approach:**

## 11. Testing and Validation

| Test ID | Scenario | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| TC-SD-XXX | Original scenario | | | |
| TC-SD-XXX | Negative test | | | |
| TC-SD-XXX | Regression test | | | |

**Downstream SD/MM/FI validation:**

**Unintended effects:**

**Final outcome:**

## 12. Business Impact Assessment

### Sales

**Order creation and pricing impact:**

### Logistics

**Delivery, picking, and PGI impact:**

### Finance

**Billing and accounting impact:**

### Interfaces and Reporting

**Potential downstream impact:**

## 13. Conclusions

**Configuration findings:**

**Confirmed root causes:**

**Corrections executed or proposed:**

**Outstanding issues:**

**Recommendations:**

## 14. Supporting Evidence

| Evidence ID | Description | File / Link |
|---|---|---|
| EV-XXX | Original configuration | |
| EV-XXX | Observed problem | |
| EV-XXX | Diagnostic findings | |
| EV-XXX | Configuration correction | |
| EV-XXX | Final validation | |

---

**Evidence integrity:** Record actual configuration values observed in SAP. Distinguish read-only investigations from executed changes and simulations. Never claim a configuration change was implemented unless it was actually saved in an authorized SAP training environment.
