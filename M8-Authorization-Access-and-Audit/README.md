
# Module 8 — SAP SD Authorization, Access and Audit

## 1. Module Overview

This module focuses on SAP S/4HANA Sales (SD) authorization troubleshooting, user access governance, segregation of duties (SoD), and audit documentation.

The objective is to demonstrate a structured approach to investigating access issues, evaluating security risks, and supporting business controls within SAP SD processes.

The module combines **executed, read-only JV2/100 IAM role inspection** with a limited evidence-based training access review, two potential SoD risk analyses, retained reusable templates, and separately labeled fictional examples. No production access governance or role remediation is claimed.

## 2. Learning Objectives

- Understand SAP SD authorization concepts
- Investigate authorization-related incidents
- Review user roles and organizational restrictions
- Evaluate potential segregation-of-duties conflicts
- Recommend risk-based corrective actions
- Document audit evidence
- Validate authorization changes
- Support formal access review closure

## 3. Module Deliverables

| Step | Document | Purpose |
|---|---|---|
| 31 | Authorization and SoD Assessment Template | Structured authorization and security risk assessment |
| 32 | Access Review Matrix | User access and role evaluation |
| 33 | Authorization Incident Investigation Example | Simulated VA02 authorization incident |
| 34 | SoD Conflict Investigation and Mitigation Example | Simulated customer master and credit memo conflict |
| 35 | Audit Evidence and Access Review Closure Template | Evidence, corrective actions, and closure documentation |
| 36 | README and Module Completion Summary | Module navigation and overview |

### Documents

- **[M8 Evidence-Based Access, Authorization and SoD Review](M8-Access-Authorization-and-SoD-Review.md)** — completed training-scope assessment, four personas, two qualified SoD risk analyses, actual CBC-denial reference, audit findings and validation limits (EV-001, EV-079–EV-080, EV-094–EV-103).

1. [Authorization and SoD Assessment Template](Authorization-and-SoD-Assessment-Template.md)
2. [Access Review Matrix](Access-Review-Matrix.md)
3. [Authorization Incident Investigation Example](Authorization-Incident-Investigation-Example.md)
4. [SoD Conflict Investigation and Mitigation Example](SoD-Conflict-Investigation-and-Mitigation-Example.md)
5. [Audit Evidence and Access Review Closure Template](Audit-Evidence-and-Access-Review-Closure-Template.md)

## 4. Actual execution and tools

**Executed:** In **JV2 / client 100**, the Fiori **IAM Information System**, Business Role entity, was used read-only to inspect `BR_INTERNAL_SALES_REP`, `BR_BILLING_CLERK`, `BR_BUPA_MASTER_SPECIALIST`, and `BR_PRICING_SPECIALIST`. Key evidence: [EV-094–EV-103](../00-Project-Tracking/Evidence-Register.md). The review reused M1 role-assignment evidence and M5 CBC Unauthorized evidence.

**Not executed:** SU01, PFCG, SU53, STAUTHTRACE, effective-access negative tests, user-role edits, approved security changes, or business sign-off. T41/client 400 is a different SAP system and cannot diagnose JV2 CBC access.

### Reference tools and transactions (methodology, not execution claims)

| Transaction | Description | Application |
|---|---|---|
| SU01 | User maintenance | User and role assignments |
| SUIM | User information system | Authorization and role analysis |
| PFCG | Role maintenance | Role and authorization management |
| SU53 | Authorization failure analysis | Initial authorization troubleshooting |
| STAUTHTRACE | Authorization trace | Detailed authorization investigation |
| VA01 | Create sales order | Sales document processing |
| VA02 | Change sales order | Sales document processing |
| VA03 | Display sales order | Sales document review |
| BP | Maintain business partner | Customer master management |
| VF01 | Create billing document | Billing processing |

Actual transaction availability, access permissions, and authorization checks depend on the SAP system configuration.

## 5. Practical Business Scenarios

### Scenario A — Sales Order Authorization Failure

A sales representative attempts to modify a sales order belonging to a different sales organization.

Investigation approach:

1. Confirm the reported authorization error.
2. Review SU53 results.
3. Examine role assignments.
4. Verify organizational authorization restrictions.
5. Determine whether access should be granted.
6. Recommend an approved resolution.
7. Define validation tests.

Key learning:

An authorization restriction may be functioning correctly and should not automatically be removed.

### Scenario B — Segregation of Duties Conflict

An employee has potentially conflicting access to customer master maintenance and credit memo processing.

Investigation approach:

1. Identify potentially conflicting activities.
2. Confirm effective user permissions.
3. Review legitimate business responsibilities.
4. Assess existing approval controls.
5. Evaluate business and financial risks.
6. Recommend role separation or compensating controls.
7. Document mitigation and residual risk.

Key learning:

SoD assessments require understanding actual business capabilities, not simply assigned SAP transaction codes.

## 6. Governance Principles

The module emphasizes:

- Least-privilege authorization
- Business justification for access
- Organizational authorization restrictions
- Independent approvals
- Segregation of incompatible responsibilities
- Documented risk ownership
- Evidence-based incident resolution
- Periodic user access reviews
- Controlled authorization changes
- Audit-ready documentation

## 7. Standard Review Workflow

1. Identify the incident or access review requirement.
2. Establish the affected SAP SD business process.
3. Collect relevant authorization evidence.
4. Review effective user access.
5. Assess business justification and SoD risks.
6. Identify root causes or control weaknesses.
7. Recommend corrective actions.
8. Obtain appropriate approvals.
9. Validate approved changes.
10. Document evidence and close the review.

## 8. Module Completion Summary

### Documentation Checklist

- [x] Authorization assessment template prepared
- [x] Access review matrix prepared
- [x] Authorization incident example documented
- [x] SoD conflict example documented
- [x] Audit evidence and closure template prepared
- [x] Module README prepared

### Practical Experience Status

| Activity | Status |
|---|---|
| IAM role, catalog and organizational restriction inspection | **Executed read-only — JV2/100, EV-094–EV-103** |
| Four-persona access review | **Documented analysis**; not a formal four-user access certification |
| Two potential SoD scenarios | **Documented analysis**; no confirmed technical violation |
| CBC authorization incident | **Actual Unauthorized result reused** from M5 EV-079–EV-080; root cause and remediation open |
| VA02 incident example / fictional SoD example | **Simulated; preserved unchanged** |
| SU53 / PFCG / SU01 / STAUTHTRACE | **Not executed** |
| Production authorization testing / actual role changes | **Not performed** |
| Formal business approval / audit closeout | **Not performed** |

**M8 portfolio assessment: COMPLETE.** Real user-population recertification, authorized security remediation, effective SoD validation and risk-owner/audit sign-off were not project activities and are not claimed; CBC remains a documented unresolved technical observation.

## 9. Consultant Competencies Demonstrated

This module demonstrates knowledge of:

- SAP SD business process authorization requirements
- Structured incident investigation
- Business-oriented security risk assessment
- Access review documentation
- SoD conflict identification and mitigation planning
- Collaboration between business, SAP functional consultants, and security teams
- Audit evidence requirements
- Corrective action management

These competencies are particularly relevant to SAP SD application support, implementation support, testing, and governance-related assignments.

## 10. Portfolio Disclaimer

This module is part of an independent SAP S/4HANA SD professional development portfolio.

Examples are fictional or illustrative unless explicitly supported by cited system evidence. The M8 evidence-based report is based on actual read-only JV2 IAM observations plus qualified analysis.

No production authorization analysis, role modification, access review, or audit activity is claimed to have been performed.

---

**Module Status:** COMPLETE — bounded read-only training assessment and analytical governance documentation; formal operational approvals not applicable to lab completion

**Area:** SAP S/4HANA Sales (SD)

**Focus:** Authorization, Access Governance, Segregation of Duties, and Audit Readiness
