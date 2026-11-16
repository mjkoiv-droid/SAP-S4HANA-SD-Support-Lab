# M1 — Access Audit, Landscape Inventory and Baseline Monitoring

**Execution status:** M1 landscape and monitoring snapshot recorded on 16 November 2026. Tested access is evidenced; untested, restricted and later-module checks remain explicitly pending. This is **not** a blanket access-audit pass.  
**System:** SAP S/4HANA Cloud, Public Edition — SAP Learning Hub Hands-on Practice sandbox, JV2 / client 100 (per supplied account inventory; not rechecked in System → Status in this M1 sequence).  
**Evidence:** see the central [Evidence Register](../00-Project-Tracking/Evidence-Register.md) and local `evidence/` images.  
**Source:** Original Word guide §§2.2 and 4/M1. **No scheduling assumptions apply.**

## A01. System and boundaries

| Attribute | Observation | Source / certainty |
|---|---|---|
| SAP environment | S/4HANA Cloud Public Edition; Fiori native and GUI-style WebGUI screens both accessible | Account inventory and directly observed screenshots |
| System ID / client | JV2 / 100 | Supplied November 16 inventory; not independently re-read in this sequence |
| User account | Training user; identifiers retained privately in source inventory, omitted here | Supplied account details; relevant role assignments verified via IAM, EV-001 |
| Business roles | 14 assigned now; all 14 IDs match the user-supplied baseline | IAM Information System screenshot, EV-001 |
| Roles examined in old IAM workbook | Seven of fourteen; 5,294 role-app entries from seven role exports | Supplied workbook; not evidence of current count for all roles |
| Current IAM role-app entry count | 6,904 reported when selecting all 14 roles | User-reported current Fiori count; full export comparison not yet performed |
| Availability / reset | Sandbox reset stated as 6 Dec 2026 | Supplied account details; not confirmed in the app |
| Dedicated/client isolation | Training test customer 1000193 used, but tenant-sharing and permissible configuration scope not formally established | **Pending confirmation**; no shared customizing or user roles changed |

## A02–A08. Permission/feasibility matrix

| ID | Area | Verified result | Status / boundary | Evidence |
|---|---|---|---|---|
| A02 | Sales order & document flow | VA01/VA02/VA03 WebGUI-style actions executed; orders 1055, 1056 saved; delivery 80000784 created and document flow displayed | **Available for training writes**; no PGI/billing posted as part of M1 | EV-002, EV-009–EV-016 |
| A02 | Outbound deliveries | Manage Outbound Deliveries accessible; VL03N-style display accessible; shipping point and processing statuses observed | **Read/write capability partly verified**, delivery creation confirmed | EV-004, EV-011–EV-013 |
| A02 | Billing | Manage Billing Documents accessible; invoice display and historical posting attempt observed separately | **Read accessible**; posting of unrelated historical invoice produced error — excluded from controlled lab tickets | EV-006 |
| A03 | Configuration | CBC/direct access previously denied per supplied access inventory; no configuration edits attempted | **Restricted / not verified in M1**; evaluate suitable additional sandbox for M3 | Account inventory |
| A04 | IDocs | WE02/WE05/WE19/BD87 not found in currently examined app search/IAM list | **Not available here as tested**; investigate another Learning Hub sandbox for actual M4 exercises | User search and IAM investigation |
| A05 | General application logs | SLG1 not present; Fiori SituationDefinition-showLog accessible only in `SIT` category | **SIT-only monitoring verified**, not general SD log coverage | EV-005 |
| A05 | Output processing | Manage Output Items for Deliveries (`F4455`) opens; completed and in-preparation statuses counted | **Read accessible** | EV-007; aggregate counts user-reported |
| A05 | F5002 | IAM lists F5002 app authorization variants, but direct Fiori search and `/nF5002` launch unavailable | **Launch not verified**; do not confuse IAM entitlement with launchability | IAM screenshots in conversation |
| A06 | Security/role support | IAM Information System accessible; 14 business roles verified | **Read access verified**; SU53, SU01, PFCG not tested here | EV-001 |
| A07 | Transports | SE09/SE10, STMS not tested | **Unverified/deferred** to M7/alternate sandbox |
| A08 | Data segregation | Exercises conducted against test customer 1000193, own references `M1-TEST-001`, `REF TT0234`; no master/shared customizing changed | **Test data use verified**, shared-scope policy still unverified | EV-009–EV-016 |

## Access audit RAG summary (as required by original guide)

**GREEN** = tested and available for the stated action; **AMBER** = partly tested, source-limited or not yet verified; **RED** = explicitly unavailable through the tested route in this sandbox. These ratings apply **only to JV2/client 100 and the specific action**, not all of SAP Learning Hub or any alternate sandbox.

| Access area | RAG | Verified scope / limitation |
|---|---|---|
| System identity/release and tenancy boundary (A01) | AMBER | JV2/100 and expiry were supplied in the account inventory; `System → Status` was not independently captured; shared-sandbox rules remain unconfirmed |
| Sales orders and document flow (A02) | GREEN for tested tasks | Orders 1055/1056 created/changed/displayed; document flow inspected; no complete O2C run |
| Delivery processing (A02) | GREEN for tested tasks | Created and displayed delivery 80000784; picking, PGI and billing were not executed |
| Billing and accounting (A02) | AMBER | Billing display/filtering available; successful FI posting not demonstrated |
| Configuration change (A03) | AMBER | CBC reported denied from prior inventory; no safe dedicated customization client confirmed |
| IDoc interface tools (A04) | RED in examined Launchpad | WE02/WE05/WE19/BD87 not located there; reassess in a suitable alternate sandbox |
| Application logs / output (A05) | AMBER | SIT-only logs and delivery outputs available; SLG1/general SD monitor unavailable in tested view |
| Authorization support (A06) | AMBER | User role assignments checked; SU53/SU01/PFCG not verified |
| Transports (A07) | AMBER | SE09/SE10/STMS not verified; no import attempted |
| Test-data segregation (A08) | AMBER | Own sandbox test customer/order references used; shared-client rules still unconfirmed |

## M1.02. Organization, transactions and sample-data inventory

| Object | Actual observed value | Evidence |
|---|---|---|
| Company code | **Not verified**; sales organization number must not be assumed to be company code | — |
| Sales organization | 1010 — DE Sales Org | EV-002 |
| Distribution channel | 10 | EV-002 |
| Division | 00 | EV-002 |
| Plant | 1010 | EV-009 |
| Shipping point | 1010 — DE Shipping Point Standard | EV-012 |
| Sales document type | OR — Standard Order | EV-002 |
| Sales item category | TAN (TG11); CB1 (POWERRACK_472, third-party scenario) | EV-008, EV-009 |
| Delivery document | 80000784, open at end of M1 | EV-011, EV-013 |
| Delivery type | **Not yet verified** (do not infer from number) | — |
| Billing document type | F2 observed on unrelated historical document; **no M1 test billing executed** | separate historical display |
| Pricing procedure | Y10101 — Materials (Germany), observed for order 1056 item 10 | EV-015 |
| Standard pricing condition | PPR0 = EUR 17.55 for TG11, 1 PC; tax TTX1 = EUR 3.33 (19%) | EV-014, EV-016 |
| Customer | 1000193 — NPS Test Chemical GmbH (training test customer) | EV-009 |
| Test material | TG11, standard item TAN, 1 PC at plant 1010 | EV-009 |
| Stock | TG11 unrestricted stock 13,058 in plant 1010 / storage 101A reported in user-provided Materials.xlsx; not a live ATP quantity confirmation | Materials.xlsx; successful delivery creation EV-011 |
| Payment/terms | NT30, EXW Hamburg; shipping condition 01 Standard | EV-009, EV-012 |
| Shipment fulfillment | Delivery 80000784: picking A not yet picked; PGI A not started; billing A not invoiced; document checked | EV-013 |

## M1.03. Read-only monitoring baseline — 16 Nov 2026

These figures reflect SAP training data and the applied filters **at the time checked**. They are not live production metrics or a service-quality conclusion. Sources marked *reported* were read aloud from the SAP UI without a separate count screenshot.

| Monitoring area | App / scope | Actual baseline | Evidence / confidence | Interpretation |
|---|---|---|---|---|
| Sales volume | Manage Sales Orders, sales org 1010 | **999** total at time of initial query (before own new cases) | User-reported count | System data count, not current after own orders |
| Blocked/partially blocked sales orders | Manage Sales Orders, org 1010 | **0/0** at original baseline | User-reported result | Before deliberate blocked order 1055 |
| Fulfillment issues | Sales Order Fulfillment Issues | **44 issue flags** across **40** sales documents: 39 invoice, 4 order, 1 delivery | EV-003 | Existing unrelated training records; not our incidents |
| Outbound deliveries ready for GI | Manage Outbound Deliveries, default `Ready to Post GI` | **8** rows displayed, all GI not yet processed | EV-004 | Read-only, did not execute GI |
| Billing blocked for FI | Manage Billing Documents, sales org 1010, relevant posting status | **63** | EV-006 shows status options; count user-reported | Backlog indicator only; no historical error investigation included |
| Billing — account determination posting error | Same, corresponding posting status | **0** | User-reported count | Does not prove all accounting interfaces healthy |
| Billing — error in accounting interface | Same | **0** | User-reported count | Status-specific only |
| Delivery output — completed | Manage Output Items for Deliveries (`F4455`) | **1,543** | EV-007 shows app/filter; count user-reported | Successfully processed status |
| Delivery output — in preparation | Same | **802** | EV-007; count user-reported | Not necessarily failures |
| Delivery output — error/pending/to be output | Same | **0 reported in each status** | User stated only Completed and In Preparation | Subject to same filters as viewed; do not infer enterprise-wide coverage |
| Application logs | SituationDefinition-showLog, filter `SIT`, date 16 Nov 2026 | **36** log entries; Information and Warning | EV-005 | Only Situation Handling category, not general SD |
| Incomplete sales orders | Available filters not separately verified | **Not measured** | — | Clearly documented gap |
| IDoc failures | IDoc monitoring not found in this sandbox | **Not measured** | — | Defer live hands-on to M4 alternate sandbox |
| Interface monitor | No suitable monitor verified | **Not measured** | — | Do not invent a zero value |

## M1.06. KPI baseline and interpretation

| KPI | Lab baseline | Nature / calculation |
|---|---|---|
| Lab incident cases opened | 2 | Controlled cases based on orders 1055 and 1056 |
| Lab incident cases resolved and retested | 2 | Both have successful final SAP evidence EV-011 and EV-016 |
| Lab incident cases still open | 0 | **Only within this two-case training log** — not a system support backlog |
| Real-world support incidents open / aging | N/A | No real service desk or live production incident system |
| Mean time to resolution (MTTR) | N/A | Time-to-resolution not instrumented for both cases; do not manufacture metric |
| Failed IDoc/interface count | N/A | No suitable monitoring access tested in current tenant |
| Billing block backlog | 63 | Status `Billing document blocked for forwarding to FI`, 1010 |
| Billing account determination error count | 0 | Specific posting-status filter only |
| Delivery output preparation backlog | 802 | Status `In Preparation`; not automatically failed |
| Delivery output error count | 0 reported | From observed status set, with current-filter limitation |
| Sales fulfillment issue flags | 44 | 40 documents; do not call them 44 incidents |

## Remaining M1 access / evidence limitations

- [x] Verify sales order, delivery, billing-read and fulfillment-monitor access.
- [x] Verify 14 assigned business roles and same role IDs as supplied baseline.
- [x] Record organizational values, pricing, customer, test product, shipping point.
- [x] Capture monitored fulfillment, delivery, billing, output and SIT log counts.
- [x] Record two genuine controlled incident investigations and positive retests.
- [ ] Company code and actual delivery type not independently checked; optional follow-up if needed for complete organizational inventory.
- [ ] No comprehensive incomplete-sales-document count; no general SD application/IDoc/interface monitoring in this tenant.
- [ ] Shared-client write/configuration policy and A03/A06/A07 specialized permissions not fully tested; handle before restricted activities in later modules.
- [ ] Evidence snapshots must be reviewed for publication permissions and anonymized before making repo public.

**M1 classification:** Required M1 monitoring snapshot and two deliberate practice investigations executed; runbook is simulated. Specialized access checks explicitly deferred to M3/M4/M7/M8. Do not claim 100% access-audit coverage or real production support.
