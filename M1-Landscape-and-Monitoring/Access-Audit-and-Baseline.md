# M1 — Access Audit, Landscape Inventory and Baseline Monitoring

**Execution status:** Not Started — fields below are unverified until populated from the actual SAP training system.  
**Evidence convention:** Use next unused `EV-###` in the central [Evidence Register](../00-Project-Tracking/Evidence-Register.md).  
**Source:** Original Word guide, sections 2.2 and 4/M1.

## A01. SAP system status — first practical step

**SAP GUI:** `System → Status` (read-only). Do not enter SAP credentials into this file.

| Observed field | Verified system result | Evidence ID |
|---|---|---|
| Date/time and timezone | Not inspected | — |
| System ID / product and release | Not inspected | — |
| Client | Not inspected | — |
| Own user / authorization context (redact name if needed) | Not inspected | — |
| System type and shared/dedicated-client boundary | Not confirmed | — |
| Practice access and data reset restrictions | Not confirmed | — |

**Safety check:** record observed fields only; do not publish unredacted user, host or infrastructure details.

## A02–A08. Permission and feasibility matrix

**Status options:** Not inspected / Available read-only / Available with approved training writes / Blocked / Requires confirmation.

| Audit ID | SAP area | Transaction(s) | Status | Actual observation / error | Evidence ID |
|---|---|---|---|---|---|
| A02 | Sales order and O2C | VA01, VA03, VL03N, VF03 | Not inspected | — | — |
| A03 | Configuration | SPRO, VOV8, V/08 | Not inspected | — | — |
| A04 | IDocs and reprocessing | WE02/WE05, WE19, BD87 | Not inspected | — | — |
| A05 | Application and output logs | SLG1, output monitor | Not inspected | — | — |
| A06 | Security and roles | SU53, SU01, PFCG | Not inspected | — | — |
| A07 | Transport | SE09/SE10, STMS | Not inspected | — | — |
| A08 | Data segregation | Dedicated test objects and shared-client policy | Not confirmed | — | — |

## M1.02. Organization and sample-data inventory

| Object | Observed actual value / availability | Evidence ID |
|---|---|---|
| Company code | Not inspected | — |
| Sales organization | Not inspected | — |
| Distribution channel | Not inspected | — |
| Division | Not inspected | — |
| Plant | Not inspected | — |
| Shipping point | Not inspected | — |
| Sales document type | Not inspected | — |
| Delivery and billing types | Not inspected | — |
| Pricing procedure | Not inspected | — |
| Sample customer/business partner | Not selected | — |
| Sample material and stock | Not selected | — |
| Credit/tax/partner configuration relevant to first O2C | Not inspected | — |

## M1.03. Monitoring baseline

| Monitoring check | Tool / app actually used | Observed total/status | Date/time | Evidence ID | Limitation |
|---|---|---|---|---|---|
| Incomplete sales orders | — | Not checked | — | — | — |
| Blocked orders | — | Not checked | — | — | — |
| Delivery/picking backlog or blocks | — | Not checked | — | — | — |
| Billing backlog/blocks | — | Not checked | — | — | — |
| IDoc failure/status counts | — | Not checked | — | — | — |
| SLG1/application errors | — | Not checked | — | — | — |
| Invoice/output processing failures | — | Not checked | — | — | — |
| Interface queue/monitoring | — | Not checked | — | — | — |

## M1.06. Baseline KPIs

| KPI | Actual value | Source/calc | Evidence | Classification |
|---|---|---|---|---|
| Open incident count | N/A | No real support-ticket system examined | — | Not measured |
| Incident aging | N/A | No real support-ticket system examined | — | Not measured |
| Failed IDoc/interface count | N/A | Pending system read | — | Not measured |
| Billing backlog count | N/A | Pending system read | — | Not measured |
| Mean time to resolution | N/A | No observed ticket history | — | Not measured |

If illustrative example metrics are later added, keep them visibly separate from actual measured values.

## Module 1 evidence closure

- [ ] A01–A08 evaluated with evidence, including honest blockers
- [ ] Organizational/sample data inventory captured
- [ ] Monitoring sweep completed where permitted
- [ ] Support operating model completed
- [ ] Two triage tickets recorded, with observed/simulated classification
- [ ] KPI sheet classified honestly
- [ ] Evidence register and R01 updated from verified activity

**Module completion:** Not Started.  
**Next action:** Open `System → Status` in SAP GUI and supply an anonymized screenshot of the status window.
