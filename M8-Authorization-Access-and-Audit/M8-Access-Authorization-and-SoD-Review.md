# M8 — Evidence-Based Authorization, Access and SoD Review

**Assessment:** M8-SD-001  
**System/client for new inspections:** JV2 / 100 — SAP S/4HANA Cloud Public Edition  
**Primary application:** IAM Information System (Fiori), **Business Role** entity  
**Classification:** **Executed read-only SAP inspections + documented analytical access/SoD assessment**  
**Review disposition:** Training assessment documented; **formal access certification and security incident closure not performed**  
**Scope:** Training-user role assignments, selected SAP business-role catalogs and sales-organization restrictions. No production data or operational approvals.

## 1. Scope and evidence boundary

The starting point is the **14 assigned business roles** previously verified for the training user in M1 ([EV-001](../M1-Landscape-and-Monitoring/evidence/iam-14-roles-crop.png)). M8 reused actual SAP order-to-cash activities from M1–M6 to identify business-process needs, but did **not** repeat transactions or infer the authorization contribution of an individual role from successful actions under a multi-role user.

New M8 read-only observations cover four role IDs through filtered IAM role/catalog/restriction views (EV-094–EV-103). The inspection **does not** establish complete effective user authorization, a complete review population, independent business need, an approved SoD rule-set, or operating compensating controls. No roles, users, configuration, sales orders or billing documents were changed for M8.

### New read-only role observations

| Business role | Observed IAM evidence | What it establishes | What it does not establish |
|---|---|---|---|
| `BR_INTERNAL_SALES_REP` | **84 business catalogs** (EV-094); **15** Sales Organization restriction rows: 6 Read, 4 Write, 5 Value Help, **Unrestricted** in each returned row (EV-095) | Assigned catalogs and configured unrestricted scope for those *particular* sales-organization restriction records | Full effective access, authorization to edit every sales order, or coverage of all restriction fields |
| `BR_BILLING_CLERK` | **153 business catalogs** (EV-103); Sales Organization filter returned **32** rows, with the **visible** Read/Write/Value Help rows Unrestricted (EV-096); billing catalog comparison showed **18** matching assignments across this role and Internal Sales (EV-097) | Billing-related catalog exposure; wide-looking organizational scope in the inspected rows | Every one of the 32 rows individually verified, credit-memo approval rights, or unapproved access |
| `BR_BUPA_MASTER_SPECIALIST` | **5 customer-related catalogs**, including `Master Data - Customer Master` (`SAP_CMD_BC_CUST_MAINT_PC`) (EV-098); **3** Sales Organization rows: Read/Write/Value Help all Unrestricted (EV-099) | Customer-master maintenance catalog and broad configured Sales Organization scope in the three returned rows | Actual write execution, access to every customer attribute, or approved business responsibilities |
| `BR_PRICING_SPECIALIST` | **2** catalogs matching `*Pricing*`: `Sales - Pricing Inbox` and `Sales - Pricing Scheduling` (EV-100) | Two pricing-related catalog assignments | Condition-record creation/change rights or an executable pricing-maintenance conflict |

In the Internal Sales role, filtered **Business Role - Restriction Value** and **Business Role - Application** views returned **No results found** (EV-101/EV-102). This is a view/filter result, **not proof that the role has no apps or restrictions**; the business catalog and restriction views returned records.

**Interpretation:** A reported **Unrestricted** Sales Organization field applies to the specific IAM restriction record and access category. It is not a grant of unrestricted privileges across SAP SD, other organizational fields, approvals or transactions. For Billing Clerk only the displayed subset of the 32 rows was individually seen.

## 2. Four-persona access review — training analysis

The following are **four representative job-function personas**, not four different identified users. The actual evidence is a training user's combined role inventory and selected role details; business-need approval is not available.

| Persona | Illustrative job need | Role / evidence used | Appropriateness conclusion | Review action |
|---|---|---|---|---|
| **Sales Clerk** | Create and change authorized customer sales orders; display status | `BR_INTERNAL_SALES_REP`: EV-001, EV-094–EV-095; executed historical SD processing in M1–M6 | **Portfolio assessment complete; business suitability not evaluated.** The role exposes many catalogs and the observed Sales Org scopes are Unrestricted; not a finding of unauthorized access | Business owner to confirm required sales organizations and sales-order modification scope; restrict where appropriate |
| **Warehouse Operator** | Manage assigned outbound deliveries, picking and PGI | `BR_WAREHOUSE_CLERK`: assigned in EV-001; actual delivery/PGI work observed earlier, but executed under a **multi-role** training user | **Not role-specifically verified.** Historical execution cannot be attributed to the warehouse role alone | Confirm role/catalog restrictions and separation from sensitive order/billing activities in a governed access review |
| **Billing Specialist** | Process permitted invoices and related follow-up | `BR_BILLING_CLERK`: EV-001, EV-096–EV-097 | **Portfolio assessment complete; business suitability not evaluated.** Billing catalogs present; the displayed Sales Org restrictions are Unrestricted | Verify billing, cancellation, credit memo and approval capabilities separately; independent review for sensitive adjustments |
| **SD Support Analyst** | Investigate and display sales-order, delivery, billing and interface issues; request escalated changes | Training role set (EV-001) and real CBC access denial (EV-079–EV-080); **no separately verified SD Support Analyst role** | **Proposed access model only**, not a completed account entitlement test | Prefer diagnostic display/read roles; separate production writes, authorizations and configuration access; route CBC access request through authorized owner |

**Population qualification:** One known training-user role inventory was reviewed. Neither a production user list nor a complete tenant population was assessed. Even where a named role appears in EV-001, assigned-role overlap is not proof of effective conflicting capabilities.

## 3. SoD assessment 1 — Customer master vs sensitive billing

**ID:** M8-SOD-01  
**Classification:** **Potential SoD risk — not a confirmed violation**

- **Activity A:** Maintain sensitive customer master and customer sales-area data. `BR_BUPA_MASTER_SPECIALIST` includes a Customer Master catalog and Sales Organization Write/Unrestricted restriction entry (EV-098–EV-099).
- **Activity B:** Process billing and potentially sensitive customer adjustments. `BR_BILLING_CLERK` includes Sales - Billing Documents and other billing catalogs, with selected Sales Organization Write/Unrestricted rows (EV-096–EV-097).
- **Intersection:** Both named business roles occur in the previously evidenced 14-role training-user inventory (EV-001).
- **Business risk:** A user able to change sensitive customer details and post inappropriate credits/refunds might conceal or cause erroneous financial adjustments.
- **Verification gaps:** Credit memo initiation, release/approval and financial adjustment privileges **were not tested**; maintenance privileges are inferred only from catalog and restriction metadata, not an actual write test. No approved SoD rule-set, workflow, change log review, business approval or mitigation effectiveness evidence.
- **Recommended least-privilege design:** Separate sensitive customer maintenance from credit memo approval and adjustment processing. Require independent approval of sensitive credits, monitor changes, and review any documented exception with a business owner.
- **Disposition:** **Potential risk, control design documented; technical conflict, risk acceptance, mitigation and closure unverified.** No role change made.

## 4. SoD assessment 2 — Pricing vs sales-order execution

**ID:** M8-SOD-02  
**Classification:** **Conceptual potential SoD risk; pricing-maintenance entitlement unverified**

- **Activity A:** Create or amend pricing condition records (hypothetical sensitive authorization). `BR_PRICING_SPECIALIST` is assigned (EV-001); the only M8-filtered pricing catalogs found were Pricing Inbox and Pricing Scheduling (EV-100).
- **Activity B:** Create/change sales orders with pricing consequences. `BR_INTERNAL_SALES_REP` is assigned (EV-001), has multiple sales catalogs (EV-094), and the training user has executed sales-order work in prior modules.
- **Business risk if both activities are authorized:** An individual might alter a condition record and apply it in an order without independent price governance.
- **Verification gaps:** **No pricing condition maintenance access was demonstrated**; the pricing catalogs observed do **not** establish such access. No rule-set, pricing approval control, same-org effective access or actual price manipulation test.
- **Recommended control design:** Keep pricing condition maintenance with authorized pricing owners, apply approval or independent exception review for price changes/overrides, and monitor sensitive overrides and condition changes.
- **Disposition:** **Illustrative design risk only**, not a verified technical conflict. No authorization change or control test.

## 5. Actual authorization incident — existing CBC denial

**Case:** [INC-SD-006 — JV2 CBC Unauthorized](../M5-Incident-and-Root-Cause-Management/Incident-INC-SD-006-CBC-Access.md)  
**Actual evidence:** [EV-079](../M5-Incident-and-Root-Cause-Management/evidence/jv2-cbc-management.png) (CBC-managed configuration), [EV-080](../M5-Incident-and-Root-Cause-Management/evidence/jv2-cbc-unauthorized.png) (CBC application **Unauthorized** response).

- **Observed:** The training user's CBC application entry returned **Unauthorized**, preventing that route of read-only JV2 configuration review.
- **Not established:** Which identity, tenant entitlement, CBC role, permission or service setting caused the denial.
- **Appropriate response:** Route proposed **SR-SD-002** to an authorized CBC/identity administrator; verify business justification for narrowly scoped read access, then retest only with permission.
- **Separation of systems:** T41/400 read-only IMG checks in M5 do not establish JV2/100 CBC permissions. SU53 in T41/400 was **not** used to diagnose a separate CBC application denial.
- **Status:** **Open / unresolved.** No SU53, STAUTHTRACE, role change, remediation, retest or incident closure claimed.

The existing [fictional VA02 incident](Authorization-Incident-Investigation-Example.md) remains **a separate simulated training example** and is **not** presented as a reproduced SAP error.

## 6. Audit evidence and findings packet — limited training scope

### Evidence included and provenance

| Evidence | Source | Coverage | Quality / limit |
|---|---|---|---|
| EV-001 | M1 JV2 IAM role list (cropped) | Training user's 14 assigned role IDs | Real role listing; does not indicate approved need |
| EV-094–EV-100 and EV-103 | JV2 IAM Business Role filters | Catalog counts, selected catalog names, and Sales Organization restriction rows | Actual read-only observations; only filtered role views, not full authorization trace |
| EV-101–EV-102 | JV2 IAM filtered result views | No results in two relation views | Negative query output only; not evidence of no authorizations |
| EV-079–EV-080 | M5 JV2 configuration/CBC launch | Reproduced Unauthorized response | Real denial; no underlying authorizing check captured |
| M1–M6 prior process evidence | Executed SD tasks under combined training-user role set | Business context and process-capability baseline | **Cannot** tie a specific activity to a specific role |
| T41/400 M7 EV-090–EV-093 | Read-only SE09/STMS inspection | Separate SAP GUI/transport context | **Not** evidence of JV2 role or CBC configuration |

### Findings and follow-ups

| Finding | Evidence-based status | Recommendation | Owner / approval |
|---|---|---|---|
| **M8-F01 — Wide observed Sales Organization scope** | **Observation**, not proven excess: specified `Read/Write` restriction rows Unrestricted in Sales, Billing, Customer Master roles | Review authorized organizational boundaries against job responsibility; only then consider restricted values | Business/process owner and authorized SAP security administrator — **not assigned / not approved** |
| **M8-F02 — Customer master + billing combination** | **Potential risk**; roles overlap in training user, effective sensitive privileges unverified | Business owner SoD review; separate credit approval and master-data maintenance; monitor sensitive changes | **Not assigned / not approved** |
| **M8-F03 — Pricing + sales-order activities** | **Conditional control-design risk**; pricing condition maintenance access unverified | Verify real maintenance rights before declaring conflict; design pricing approval and overrides monitoring | **Not assigned / not approved** |
| **M8-F04 — CBC application denied** | **Verified symptom**, unresolved root cause (INC-SD-006) | Route existing SR-SD-002 for least-privilege access review and approved retest | CBC/identity owner **not confirmed**; request **not submitted** |

### Access request and approval trail

| Item | Recorded status |
|---|---|
| Review request / access recertification population | **Training assessment only**; no real business access request or complete production user population |
| Role/organization inspection | **Performed read-only** in JV2 IAM; no PFCG/SU01 modification |
| SoD control/rule approval | **Not obtained**; two analytical risk scenarios documented |
| Mitigation / change request | **Recommendations only**; SR-SD-002 proposed earlier, **not submitted** |
| Change log / user-role modification | **No changes made** in M8; no approval or applied mitigation record |
| Validation and retest | **Not executed** — no approved correction or authorization change |
| Periodic review sign-off | **Not obtained**; no business owner, security or compliance signature |
| Formal audit closure | **Not performed**; findings are open observations / potential risks |

## 7. Consultant conclusion and limits

The practical M8 result is a **verified read-only IAM role and organizational restriction inspection**, supported by a four-persona **training governance review**, **two bounded potential SoD analyses**, and an **actual unresolved CBC access-denial case** reused from M5. The analysis intentionally avoids equating business catalogs with effective authorization or asserting an unverified conflict.

**Completed within training scope:** Documentation, role metadata observations, potential risk identification, recommendations and audit evidence inventory.  
**Outside the assessed training scope:** Individual role attribution of transactions, technical SoD proof, a full user-access recertification, administrator trace, approvals, remediation, retest, formal risk acceptance and production audit. The independent access analysis is complete within its recorded evidence boundary.  
**Linked issue:** The billing-block control problem from M2–M7 remains **unresolved**; this M8 review does not fix it.
