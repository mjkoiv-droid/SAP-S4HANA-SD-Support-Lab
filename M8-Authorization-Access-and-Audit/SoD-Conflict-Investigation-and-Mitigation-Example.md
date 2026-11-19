
# SAP SD SoD Conflict Investigation and Mitigation Example

> **Portfolio classification: COMPLETE reusable simulation/example.** Blank fields, unselected checkboxes, hypothetical approvals and illustrative pending statuses in this document are **inputs for future use**, not unfinished actions or actual sign-offs in the SAP SD Support Lab. See [final portfolio validation](../PORTFOLIO-VALIDATION.md).

## 1. Case Overview

**Case ID:** SOD-SD-001

**Category:** SAP SD / Access Governance / SoD

**Status:** Simulated Training Case

**Business Process:** Customer Master and Credit Memo Management

**Risk Classification:** High (illustrative)

### Scenario

A manufacturing company identifies a potential segregation-of-duties conflict during a periodic SAP access review.

One employee has permissions that may allow them to:

1. Maintain sensitive customer master data.
2. Create credit memo requests.
3. Release or approve credit memo requests, subject to system configuration.

The combination could allow unauthorized financial adjustments without sufficient independent oversight.

## 2. Business Context

The company uses SAP S/4HANA Sales for order-to-cash processing.

Relevant business activities include:

- Business partner and customer master maintenance
- Customer sales-area data management
- Credit memo request creation
- Credit memo request approval or release
- Credit memo billing processing

### Business Risk

A user with excessive permissions could potentially manipulate customer-related information and process unjustified credits.

Potential consequences:

- Financial loss
- Fraud exposure
- Incorrect customer balances
- Weak audit trails
- Failure of internal controls

Having multiple permissions does not automatically establish a control failure. Actual capabilities and safeguards must be assessed.

## 3. Identified Access Combination

| Business Activity | Example SAP Access | Risk |
|---|---|---|
| Maintain customer master | BP and relevant authorization objects | Unauthorized data changes |
| Create credit memo request | VA01 or applicable Fiori application | Unjustified credit initiation |
| Change credit memo request | VA02 or applicable Fiori application | Modification of credit details |
| Approve/release credit request | Configured approval workflow or release authorization | Unauthorized approval |
| Create credit memo billing | VF01 or applicable Fiori application | Financial adjustment |

Transaction access alone does not prove that the user can perform a restricted action.

Relevant authorization objects, organizational values, workflow permissions, and application-specific controls must also be reviewed.

## 4. Investigation Procedure

### Step 1 – Identify the User and Roles

An authorized SAP security reviewer examines:

- Assigned business responsibilities
- Relevant SAP roles
- Access validity dates
- Organizational authorization scope
- Critical business activities

Useful tools may include:

- SU01 – User maintenance
- SUIM – User and role analysis
- PFCG – Role maintenance

### Step 2 – Confirm Effective Authorizations

Determine whether the user can actually perform each activity.

Review:

- Role authorization values
- Permitted activities
- Sales organization restrictions
- Company code restrictions, where relevant
- Business partner authorization restrictions
- Relevant workflow approval permissions

Do not conclude that a conflict exists solely because transaction codes appear in assigned roles.

### Step 3 – Evaluate the Business Process

Identify whether the user's responsibilities require access to all activities.

Questions:

- Does the user legitimately maintain customer data?
- Does the user need to process credit memo requests?
- Can the user independently approve their own requests?
- Are monetary approval limits configured?
- Are changes and approvals logged?
- Are compensating controls already operating?

### Step 4 – Check Existing Controls

Review potential safeguards:

- Independent approval workflows
- Role-based authorization restrictions
- Approval amount limits
- Exception reporting
- Change document monitoring
- Periodic access reviews

Control effectiveness must be supported by evidence.

## 5. Simulated Findings

| Finding | Simulated Result |
|---|---|
| Customer master maintenance | Permitted |
| Credit memo request creation | Permitted |
| Credit memo request approval | Potentially permitted |
| Independent approval requirement | Not yet verified |
| SoD conflict status | Potential conflict requiring review |
| Final risk rating | Pending control assessment |

These are fictional findings for portfolio demonstration.

## 6. Root Cause Analysis

### Hypothetical Root Cause

The employee received multiple SAP roles over time as business responsibilities expanded.

Previous access assignments were not adequately reviewed when new responsibilities were introduced.

As a result, the user's combined permissions may exceed current business requirements.

### Contributing Factors

- Role accumulation
- Insufficient periodic access reviews
- Incomplete SoD analysis
- Unclear responsibility ownership
- Weak coordination between business and SAP security teams

## 7. Mitigation Options

### Option A – Remove Unnecessary Access

Preferred when conflicting access is not required.

Actions:

1. Identify the unnecessary permission.
2. Obtain business owner approval.
3. Request controlled role adjustment.
4. Retest authorized business activities.
5. Confirm the conflict is resolved.
6. Document evidence.

### Option B – Separate Responsibilities

Assign conflicting activities to different authorized users.

Example:

- Sales Support creates credit memo requests.
- Sales Manager independently approves requests.
- Billing Specialist creates credit memo billing documents.

Actual responsibility separation depends on the organization's configured process.

### Option C – Compensating Controls

If access separation is impractical, consider:

- Independent review of credit transactions
- Exception reporting
- Credit amount thresholds
- Monitoring of sensitive customer changes
- Documented risk-owner approval
- Periodic reassessment

Compensating controls do not automatically eliminate an SoD conflict. Residual risk must be evaluated and formally accepted where appropriate.

## 8. Recommended Mitigation

**Training recommendation:** Separate credit memo initiation from approval where operationally practical.

The recommended control design is:

1. Sales Support initiates the credit memo request.
2. An independent authorized approver reviews the business justification.
3. Billing processing proceeds only after required approvals.
4. Relevant transactions are logged and retained for audit.
5. Periodic monitoring identifies unusual or unauthorized activities.

Implementation depends on available SAP functionality and customer-specific configuration.

## 9. Validation Test Plan

| Test ID | Test Scenario | Expected Result |
|---|---|---|
| SOD-T01 | Sales Support creates credit memo request | Permitted |
| SOD-T02 | Sales Support attempts restricted approval | Prevented |
| SOD-T03 | Authorized manager approves request | Permitted |
| SOD-T04 | Billing Specialist processes approved request | Permitted |
| SOD-T05 | Unauthorized user modifies sensitive customer data | Prevented |
| SOD-T06 | Reviewer examines audit evidence | Required records available |

Test results should be recorded only after execution.

## 10. Audit Evidence Requirements

| Evidence ID | Description | Status |
|---|---|---|
| EVD-001 | User-role assignments | Not collected |
| EVD-002 | Effective authorization analysis | Not collected |
| EVD-003 | SoD rules and risk assessment | Not collected |
| EVD-004 | Approved mitigation decision | Not collected |
| EVD-005 | Validation test results | Not collected |
| EVD-006 | Business owner sign-off | Not collected |

## 11. Closure Checklist

- [ ] Potential conflict identified
- [ ] Actual access capabilities verified
- [ ] Business responsibilities reviewed
- [ ] Existing controls assessed
- [ ] Risk classification confirmed
- [ ] Mitigation selected
- [ ] Required approvals obtained
- [ ] Changes implemented
- [ ] Validation completed
- [ ] Residual risk documented
- [ ] Case formally closed

## 12. Consultant Lessons Learned

This scenario illustrates why SAP SD consultants need to understand both system authorizations and real business responsibilities.

Important lessons:

1. SoD conflicts involve combinations of business capabilities, not simply transaction codes.
2. SAP authorization analysis requires examination of effective access.
3. Business process knowledge is essential for evaluating actual risk.
4. Least-privilege role design reduces unnecessary access.
5. Independent approvals can reduce fraud and error exposure.
6. Mitigating controls must be verified, not merely documented.
7. Audit evidence is essential for defensible conclusions.

---

## Portfolio Disclaimer

This is a fictional SAP S/4HANA SD governance case developed for independent professional training.

No actual SAP production access review, SoD analysis, authorization modification, or mitigation test is claimed to have been performed.

All findings, risk ratings, and proposed controls are illustrative.
