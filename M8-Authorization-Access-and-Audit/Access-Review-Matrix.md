
# SAP SD Access Review Matrix

## 1. Purpose

This template supports periodic review of SAP S/4HANA SD user access, authorization assignments, and segregation-of-duties (SoD) risks.

Objectives:
- Verify that users have appropriate access
- Identify excessive or unnecessary permissions
- Detect potential SoD conflicts
- Document approvals and corrective actions
- Maintain evidence for audit and compliance

## 2. Review Information

- Review ID:
- SAP system / client:
- Review period:
- Business owner:
- Security reviewer:
- Review status: Open / In Progress / Completed

## 3. SAP SD Access Review Matrix

The following entries are illustrative. Actual access depends on configured roles, authorization objects, and organizational restrictions.

| Role / Function | Transaction | Business Activity | Access Requirement | Risk Level |
|---|---|---|---|---|
| Sales Representative | VA01 | Create sales order | Required | Low |
| Sales Representative | VA02 | Change sales order | Required | Medium |
| Sales Representative | VA03 | Display sales order | Required | Low |
| Sales Manager | VA05 | List sales orders | Required | Low |
| Shipping Specialist | VL01N | Create outbound delivery | Required | Medium |
| Shipping Specialist | VL02N | Change outbound delivery | Required | Medium |
| Billing Specialist | VF01 | Create billing document | Required | High |
| Billing Specialist | VF02 | Change billing document | Restricted | High |
| Customer Master Specialist | BP | Maintain customer master | Restricted | High |
| Sales Support | VA03 | Display sales order | Required | Low |

Risk ratings are illustrative and must be evaluated against the organization's control framework.

## 4. User Access Assessment

| User ID | Assigned Role | Business Need | Access Appropriate? | Action Required |
|---|---|---|---|---|
| USER001 | Sales Representative | Sales order processing | Yes | None |
| USER002 | Billing Specialist | Billing processing | Yes | None |
| USER003 | Customer Master Specialist | Customer maintenance | Under Review | Verify scope |

User IDs are fictional training examples.

## 5. Organizational Authorization Scope

Review whether assigned permissions are appropriately restricted by:

- Sales organization
- Distribution channel
- Division
- Company code
- Plant, where relevant
- Other applicable organizational authorization fields

| User / Role | Organization Scope | Expected Scope | Result |
|---|---|---|---|
| | | | |
| | | | |

## 6. Segregation of Duties Review

| Conflict ID | Activity A | Activity B | Potential Risk | Mitigation |
|---|---|---|---|---|
| SOD-001 | Maintain customer master | Process sensitive billing adjustments | Fraud or unauthorized adjustment | Independent review |
| SOD-002 | Create credit memo request | Approve credit memo request | Unauthorized credit | Separate approval authority |
| SOD-003 | Modify pricing conditions | Process affected sales transactions | Unauthorized discounts | Pricing controls and monitoring |

These are potential business-process conflicts, not proof of technical SoD violations. Confirm actual access paths, configurations, and mitigating controls before recording a finding.

## 7. Authorization Evidence

Relevant SAP tools may include:

- SU01 — User maintenance
- PFCG — Role maintenance
- SUIM — User information system
- SU53 — Authorization failure analysis
- STAUTHTRACE — Authorization trace

Evidence references:

| Evidence ID | Source | Description | Reviewer |
|---|---|---|---|
| EVD-001 | | | |
| EVD-002 | | | |

## 8. Findings and Corrective Actions

| Finding ID | Description | Severity | Action Owner | Control / Evidence | Status |
|---|---|---|---|---|---|
| FIND-001 | | | | | |
| FIND-002 | | | | | |

Corrective actions may include:
- Remove unnecessary role assignments
- Restrict organizational authorization values
- Separate conflicting responsibilities
- Implement documented compensating controls
- Retest access after approved changes

## 9. Review Approval

- Business owner:
- SAP security reviewer:
- Risk / compliance approver, if required:
- Outstanding exceptions:

## 10. Review Conclusion

Summarize:
- Access appropriateness
- Excessive authorizations identified
- SoD risks identified
- Corrective actions completed
- Outstanding risks and approvals

Final review status:

---

**Portfolio Note:** This matrix is intended for independent SAP S/4HANA SD training and demonstration. Example roles, users, risk classifications, and findings do not represent a completed production-system access review.
