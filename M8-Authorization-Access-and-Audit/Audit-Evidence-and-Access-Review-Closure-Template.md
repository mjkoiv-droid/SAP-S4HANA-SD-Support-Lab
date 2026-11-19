
# SAP SD Audit Evidence and Access Review Closure Template

> **Portfolio classification: COMPLETE reusable template.** Blank fields, unselected checkboxes, hypothetical approvals and illustrative pending statuses in this document are **inputs for future use**, not unfinished actions or actual sign-offs in the SAP SD Support Lab. See [final portfolio validation](../PORTFOLIO-VALIDATION.md).

## 1. Review Overview

**Review ID:**

**SAP System / Client:**

**Review Period:**

**Business Process:** SAP SD / Order-to-Cash

**Review Owner:**

**SAP Security Reviewer:**

**Business Approver:**

**Review Status:** Open / In Progress / Pending Approval / Closed

## 2. Review Scope

Identify the business functions included in the access review.

Potential scope:

- Sales order management
- Customer master maintenance
- Pricing condition maintenance
- Outbound delivery processing
- Billing document processing
- Credit memo processing
- Relevant approval activities

### Organizational Scope

- Company code:
- Sales organization:
- Distribution channel:
- Division:
- Other relevant organizational restrictions:

### Review Population

- Number of users reviewed:
- Number of roles reviewed:
- Review population source:
- Completeness verification:

## 3. Audit Evidence Register

| Evidence ID | Evidence Description | Source | Status | Reviewer |
|---|---|---|---|---|
| EVD-001 | User-role assignment report | SUIM | Pending | |
| EVD-002 | Role authorization details | PFCG | Pending | |
| EVD-003 | User master access details | SU01 | Pending | |
| EVD-004 | Authorization failure analysis | SU53 / STAUTHTRACE | If applicable | |
| EVD-005 | SoD conflict analysis | Approved SoD rules / analysis tool | Pending | |
| EVD-006 | Business access approvals | Approval records | Pending | |
| EVD-007 | Corrective action evidence | Change records | Pending | |
| EVD-008 | Validation test results | Test records | Pending | |

Evidence should be collected by authorized personnel and stored in an approved location.

Do not upload confidential production user data, authorization exports, or customer information to a public GitHub repository.

## 4. Evidence Quality Assessment

For each relevant evidence item, verify:

- Source is identifiable
- System and client are recorded
- Extraction scope is documented
- Review period is appropriate
- Population is complete
- Information is accurate
- Reviewer can reproduce or independently validate the evidence
- Sensitive information is appropriately protected

### Evidence Assessment

| Evidence ID | Complete? | Accurate? | Relevant? | Accepted? |
|---|---|---|---|---|
| EVD-001 | | | | |
| EVD-002 | | | | |
| EVD-003 | | | | |

## 5. Access Review Findings

| Finding ID | Description | Risk | Responsible Owner | Status |
|---|---|---|---|---|
| FIND-001 | | | | |
| FIND-002 | | | | |
| FIND-003 | | | | |

Possible findings:

- Excessive authorization
- Unnecessary role assignment
- Incorrect organizational scope
- Potential SoD conflict
- Missing business approval
- Incomplete access documentation
- Ineffective compensating control

All findings must be supported by evidence.

## 6. Corrective Action Register

| Action ID | Related Finding | Required Action | Owner | Control / Evidence | Status |
|---|---|---|---|---|---|
| ACT-001 | | | | | |
| ACT-002 | | | | | |
| ACT-003 | | | | | |

### Corrective Action Procedure

1. Confirm the finding with the business owner.
2. Determine the required corrective action.
3. Evaluate operational and security impacts.
4. Obtain necessary approvals.
5. Implement the approved change.
6. Perform validation testing.
7. Collect implementation evidence.
8. Update the finding status.

## 7. Segregation of Duties Assessment

| Conflict ID | Conflicting Activities | Risk Level | Mitigation | Residual Risk | Status |
|---|---|---|---|---|---|
| SOD-001 | | | | | |
| SOD-002 | | | | | |

### SoD Review Questions

- Are potentially conflicting business activities assigned to the same user?
- Can the user actually execute both activities?
- Are organizational restrictions relevant?
- Does an independent approval control exist?
- Are compensating controls documented and operating?
- Has the residual risk been accepted by an authorized owner?

Transaction assignments alone are insufficient to establish an actual SoD violation.

## 8. Validation and Retesting

| Test ID | Related Finding | Validation Activity | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|
| VAL-001 | | | | | |
| VAL-002 | | | | | |
| VAL-003 | | | | | |

### Validation Requirements

Confirm that:

- Unnecessary access has been removed
- Required business activities remain available
- Organizational restrictions operate as intended
- SoD conflicts are resolved or appropriately controlled
- Corrective actions match approved changes
- Test evidence is retained

## 9. Outstanding Exceptions

| Exception ID | Description | Risk Owner | Approval Reference | Review Trigger | Status |
|---|---|---|---|---|---|
| EXC-001 | | | | | |
| EXC-002 | | | | | |

An outstanding exception must not be treated as resolved solely because it has been documented.

Exceptions require appropriate review, approval, monitoring, and reassessment.

## 10. Review Summary

### Quantitative Summary

- Total users reviewed:
- Total roles reviewed:
- Findings identified:
- Findings resolved:
- Findings remaining open:
- SoD conflicts identified:
- SoD conflicts mitigated:
- Exceptions approved:

### Qualitative Summary

**Overall access appropriateness:**

**Key control weaknesses:**

**Corrective actions completed:**

**Outstanding risks:**

**Recommendations for future reviews:**

## 11. Final Approval

| Approval Role | Name / Reference | Decision | Basis / Notes |
|---|---|---|---|
| Business Owner | | | |
| SAP Security Reviewer | | | |
| Risk / Compliance Approver | | | |

### Closure Decision

Select one:

- [ ] Closed — All required actions completed and verified
- [ ] Closed with formally approved exceptions
- [ ] Pending — Additional actions or approvals required
- [ ] Reopened — New evidence or unresolved issues identified

**Final Review Status:**


**Next Scheduled Review:**

## 12. Lessons Learned

Document improvements to:

- SAP SD authorization design
- User access provisioning
- Role assignment procedures
- Organizational authorization restrictions
- SoD control design
- Evidence collection
- Periodic review procedures
- Business and IT coordination

## 13. Portfolio Training Value

This template demonstrates familiarity with:

1. SAP SD authorization governance
2. User and role review methodology
3. Segregation-of-duties risk assessment
4. Audit evidence management
5. Corrective action tracking
6. Security validation
7. Formal access review closure

---

## Portfolio Disclaimer

This document is a reusable SAP S/4HANA SD training and portfolio template.

It does not represent an actual completed production access review or audit.

All operational findings, approvals, test results, and closure decisions must be supported by real evidence before being presented as completed work.
