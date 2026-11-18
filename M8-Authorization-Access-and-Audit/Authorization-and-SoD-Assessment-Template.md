
# SAP SD Authorization and Segregation of Duties Assessment Template

## 1. Assessment Overview

- Assessment ID:
- SAP system / client:
- Business process:
- Requested by:
- Assessed by:
- Status: Open / Under Review / Approved / Closed

## 2. Business Context

Describe the affected SAP SD process.

Examples:
- Sales order creation or modification
- Customer master data maintenance
- Delivery processing
- Billing document creation
- Credit memo processing

Business impact:

Affected users or organizational units:

## 3. Authorization Issue

- SAP transaction / Fiori application:
- User ID (anonymized):
- Error message:
- Activity attempted:
- Expected system behavior:
- Actual system behavior:

### Diagnostic Evidence

| Check | Result | Evidence |
|---|---|---|
| SU53 authorization check | | |
| STAUTHTRACE analysis, if permitted | | |
| PFCG role review | | |
| SUIM user/role analysis | | |
| Relevant authorization objects | | |

## 4. Root Cause Assessment

Determine whether the issue is related to:

- Missing authorization
- Incorrect authorization values
- Incorrect role assignment
- Organizational restrictions
- Role design or configuration
- Other system or process issues

Root cause:

Supporting evidence:

## 5. Segregation of Duties (SoD) Assessment

Identify potentially conflicting business activities.

| Conflict ID | Activity A | Activity B | Risk | Mitigation |
|---|---|---|---|---|
| SOD-001 | Create credit memo request | Approve/release credit memo | High | Independent approval |
| SOD-002 | Maintain sensitive customer master data | Process related financial adjustments | High | Restricted access and monitoring |

These are illustrative risks. Actual conflicts and risk ratings must be validated against the organization's SoD rules and SAP authorization design.

### Conflict Analysis

- Users or roles affected:
- Business risk:
- Existing controls:
- Recommended controls:
- Residual risk:
- Risk owner:

## 6. Recommended Resolution

Proposed authorization or process changes:

Business justification:

Least-privilege considerations:

Required approvals:

## 7. Testing and Validation

| Test ID | Test Scenario | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| AUTH-001 | Authorized user performs permitted activity | Access granted | | |
| AUTH-002 | Unauthorized user attempts restricted activity | Access denied | | |
| SOD-001 | Verify conflicting activities are separated | Conflict prevented or controlled | | |

## 8. Audit Evidence

Attach or reference:

- Authorization failure evidence
- Role and authorization analysis
- SoD conflict assessment
- Approved change request
- Test execution evidence
- Business approval or risk acceptance

Evidence IDs:

## 9. Final Assessment

- Authorization issue resolved: Yes / No
- SoD risks reviewed: Yes / No
- Controls verified: Yes / No
- Business approval obtained: Yes / No
- Final status:

## 10. Lessons Learned

Document findings that could improve role design, access governance, support procedures, or audit readiness.

---

**Note:** This is an independent SAP S/4HANA SD training and portfolio template. Assessment results must be supported by actual system evidence or clearly identified as simulated examples.
