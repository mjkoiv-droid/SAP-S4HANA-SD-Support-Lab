
# SAP SD Authorization Incident Investigation Example

## 1. Incident Overview

**Incident ID:** INC-SD-AUTH-001

**Category:** SAP SD / Authorization

**Priority:** Medium (illustrative)

**Status:** Simulated / Training Case

**Affected Process:** Sales Order Management

**SAP Transaction:** VA02 – Change Sales Order

### Incident Description

A sales representative reports that they cannot change an existing sales order using transaction VA02.

The user can display sales orders using VA03 but receives an authorization error when attempting to change an order belonging to another sales organization.

## 2. Business Scenario

A manufacturing company operates with two sales organizations:

- 1000 – Domestic Sales
- 2000 – International Sales

The affected user works in Domestic Sales and normally processes sales orders for sales organization 1000.

The user attempts to modify a sales order assigned to sales organization 2000.

### Business Impact

- Requested sales order modification cannot be completed
- Order processing may be delayed
- Unauthorized access must not be granted simply to resolve the incident

## 3. Investigation Procedure

### Step 1 – Verify the Incident

Collect:

- User ID (anonymized)
- SAP system and client
- Transaction code
- Sales document number (masked)
- Sales organization
- Exact error message
- Time of occurrence

Confirm whether the issue is reproducible.

### Step 2 – Check Authorization Failure

Ask the user to reproduce the error and immediately execute transaction SU53.

Review the failed authorization check, if captured.

Record:

- Authorization object
- Checked field values
- Failed authorization values
- Timestamp and supporting evidence

Note: SU53 may not capture every relevant failure. It generally reports the latest failed authorization check for the user.

### Step 3 – Review Role Assignments

An authorized SAP security administrator reviews:

- SU01 – User assignments
- SUIM – User and role information
- PFCG – Role authorization design

Compare assigned roles against the user's approved business responsibilities.

Do not modify production authorizations during initial investigation.

### Step 4 – Analyze Authorization Scope

Check whether the relevant authorization objects restrict:

- Sales organization
- Distribution channel
- Division
- Sales document type
- Permitted activity (display, change, etc.)

For example, the authorization object V_VBAK_VKO may be relevant to sales-area authorization checks.

The actual failed object and authorization values must be confirmed through system evidence.

### Step 5 – Perform Additional Tracing if Necessary

If SU53 does not provide sufficient information, an authorized administrator may use STAUTHTRACE.

Review the actual failed authorization checks before concluding that the problem is caused by missing access.

Also consider non-authorization causes such as document status, processing restrictions, or locks.

## 4. Simulated Investigation Findings

| Investigation Item | Simulated Finding |
|---|---|
| User's assigned business area | Domestic Sales |
| Authorized sales organization | 1000 |
| Requested sales organization | 2000 |
| Transaction | VA02 |
| Reported issue | Cannot change sales order |
| Likely cause | Organizational authorization restriction |
| Evidence status | Hypothetical; requires SAP validation |

## 5. Root Cause Assessment

### Hypothetical Root Cause

The user's assigned role permits sales order processing only within sales organization 1000.

The attempted modification concerns sales organization 2000, outside the user's approved organizational scope.

This is a plausible explanation, not a verified production finding.

### Security Consideration

The existing restriction may be functioning correctly.

An authorization error does not automatically mean the user's role is incorrectly configured.

## 6. Resolution Options

### Option A – Existing Restriction Is Correct

If the user has no approved responsibility for sales organization 2000:

- Do not expand authorization
- Explain the restriction
- Refer the request to an authorized colleague
- Close the incident after confirming an appropriate business solution

### Option B – Additional Access Is Justified

If the user requires access for legitimate business reasons:

1. Obtain business owner approval
2. Request SAP security review
3. Evaluate segregation-of-duties risks
4. Apply least-privilege principles
5. Implement the approved role adjustment
6. Perform authorization testing
7. Document evidence and approval

Avoid granting unrestricted organizational access as a shortcut.

## 7. Validation Test Plan

| Test ID | Scenario | Expected Result |
|---|---|---|
| AUTH-T01 | Display authorized sales order | Display permitted |
| AUTH-T02 | Change order in approved sales organization | Change permitted |
| AUTH-T03 | Change order outside approved scope | Access denied unless separately authorized |
| AUTH-T04 | Review approved role assignments | Assignments match business need |
| AUTH-T05 | Confirm no unintended elevated permissions | No unauthorized access |

Actual results must be recorded when testing is performed.

## 8. Segregation of Duties Considerations

Before expanding access, consider whether the user could gain conflicting responsibilities involving:

- Customer master maintenance
- Sensitive pricing condition changes
- Credit memo processing
- Billing adjustments
- Approval or release activities

A conflict is established only after examining actual access combinations, business processes, and applicable SoD rules.

## 9. Incident Closure Checklist

- [ ] Incident reproduced or otherwise verified
- [ ] Authorization evidence collected
- [ ] Relevant roles reviewed
- [ ] Root cause confirmed
- [ ] Business need evaluated
- [ ] SoD implications reviewed
- [ ] Resolution approved
- [ ] Validation tests completed
- [ ] Evidence documented
- [ ] Business user informed

## 10. Consultant Lessons Learned

This scenario demonstrates that SAP SD authorization troubleshooting requires both technical and business-process understanding.

Key lessons:

1. Separate authorization problems from other SAP SD processing restrictions.
2. Investigate actual authorization checks instead of guessing.
3. Understand organizational responsibilities before modifying access.
4. Apply least-privilege principles.
5. Treat security restrictions as business controls, not merely technical obstacles.
6. Maintain evidence for incident closure and audit review.

---

## Portfolio Disclaimer

This is a fictional SAP S/4HANA SD support scenario created for independent professional training.

No production incident, authorization trace, role change, or SAP system test is claimed to have been performed.

The investigation procedure illustrates practical SAP SD support methodology.
