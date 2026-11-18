# M9-SD-001 — Global support handover and bilingual communication

**Classification:** **Documented simulation using earlier verified SAP evidence**. No new SAP execution, live customer incident, sent message, actual global handover, regional ownership acceptance, or SLA result.

**Requirements:** R14 (global support model) and R15 (Japanese/English communication); M9.01–M9.02.  
**Source case:** [INC-SD-003](../M5-Incident-and-Root-Cause-Management/Incident-INC-SD-003-Billing-FI.md), [RCA-SD-003](../M5-Incident-and-Root-Cause-Management/RCA-SD-003-Billing-FI.md), and [M2 O2C-SD-001](../M2-Order-to-Cash/O2C-Scenario-01-Standard-and-FI-Correction.md).

## 1. Business case and evidence boundary

A **fictional** multinational support organization has three cooperating groups: **Japan Sales/APAC**, **Singapore Logistics/APAC**, and **UK Finance/EMEA**. These are proposed *support responsibilities*, **not** verified SAP countries, actual participants, or legal entities in JV2.

The **actual historical training case** occurred in **JV2 / client 100**, sales organization **1010 / 10 / 00**, company code **1010**, with customer **1000193**. This was not a Japan-to-UK business transaction. Sales order **1055** progressed to delivery **80000784**, PGI material document **4900001488** and F2 invoice **90000303**. The invoice was created, but its **FI transfer failed**, displaying `Error in Accounting Interface` and `Customer 1000193 is not defined in company code 1010` (EV-021–EV-023). A customer company-code record was maintained; subsequent posting created balanced FI journal **9400000057** (EV-024–EV-026). Thus the historical case is **resolved in the sandbox**.

The exercise below deliberately **replays the diagnostic state before that correction** to practice handing off an investigation. It is **not** an open real incident and must not be misrepresented as one.

## 2. Simulated incident record and proposed support ownership

| Field | Recorded training detail |
|---|---|
| Simulation identifier | M9-SD-001 (not a service desk ticket) |
| Case classification | Retrospective simulation of a previously resolved SAP billing-to-FI error |
| Proposed business priority | P2 **illustrative only**, conditional on material business impact; no actual priority or SLA |
| Technical system | JV2 / 100; **not** T41 / 400 |
| Process | Standard order → outbound delivery → PGI → F2 invoice → FI accounting transfer |
| Affected SAP objects | Order 1055; delivery 80000784; invoice 90000303; customer 1000193; company code 1010 |
| Observed symptom | F2 document exists; no accounting document at the initial failure point |
| Established technical cause | Missing customer company-code FI data for 1010 |
| Historical outcome | Customer/company-code data maintained; journal 9400000057 posted and balanced |
| Regional routing | APAC Sales → APAC Logistics check → EMEA Finance check; **fictional team map** |
| Handover acceptance | **Not requested, not performed, not accepted** |

### RACI-style routing (proposed, not assigned)

| Support role | Investigation or decision responsibility | Explicit limit |
|---|---|---|
| Japan Sales key user / L1 | Report customer, order, invoice and exact user-visible status; preserve evidence | No master-data changes or additional billing attempt |
| Singapore Logistics key user | Confirm picking, PGI and delivery reference; check whether logistics work is already complete | Do not treat an FI-transfer failure as an outstanding shipment |
| APAC SAP SD L2 | Review document flow and FI error, isolate process boundary, collate evidence, maintain case ownership until accepted | Cannot grant FI-master approval |
| UK FI L2 / business master-data owner | Validate company-code requirement and authorized master correction; arrange posting/reconciliation retest | Approval to maintain real business partner data is not implied |
| SAP Security / configuration | Escalation only if an actual permission/configuration fault is established | Not automatically needed for this known master-data error |

**Proposed handover rule:** APAC retains simulated ownership until an explicitly designated EMEA receiver accepts the case. No acceptance has occurred here. No follow-the-sun timings or response-time performance are claimed.

## 3. Technical handover packet — English (prepared, not sent)

**Subject:** Training scenario / SD–FI posting investigation — invoice 90000303, JV2/100

> **Case context:** In the sandbox historical sequence, order 1055 and delivery 80000784 completed the logistics steps, with PGI material document 4900001488. Delivery-related F2 invoice 90000303 was created; the initial transfer to FI failed. This is **not** a billing-document creation failure.  
> **Observed error:** `Customer 1000193 is not defined in company code 1010` and `Error in Accounting Interface`. See EV-021–EV-023.  
> **Finding at the simulated handover point:** Company-code data for the customer was absent. The posting error is consistent with this omission; do not restart logistics or create a duplicate invoice.  
> **Suggested receiving-team action:** Confirm the relevant customer/company-code master-data maintenance owner, request authorized completion of the missing company-code fields, then validate FI transfer, journal linkage, amounts and duplicate prevention.  
> **Historical verification supplied for training:** The original exercise subsequently maintained customer/1010 data and obtained FI journal 9400000057, debits EUR 20.88 and credits EUR 20.88 (EV-024–EV-026). No actual pending correction remains on this historical case.  
> **Ownership:** Proposed APAC → EMEA only. **Receiver acceptance, SLA and outbound communication are not evidenced.**

### Avoid repeated work / close the information gap

| Already verified in the original SAP case | Still needed if this were a live customer case |
|---|---|
| Delivery, PGI and invoice exist (EV-017–EV-021) | Confirm live case scope, affected invoice set and business owner |
| Exact missing-company-code error (EV-022–EV-023) | Verify permissions/approval for maintenance in the customer's environment |
| Corrected-case FI journal posted and balanced (EV-025–EV-026) | Reconcile the customer's affected accounting/output interfaces; prevent duplicate postings |
| Invoice FI journal showed Not Cleared in later follow-up (EV-074–EV-076) | Treat payment/clearing as separate AR process, not a posting defect |

## 4. Japanese end-user response (draft, not sent)

**件名：請求書の会計転記エラーについて（確認結果）**

> ご連絡ありがとうございます。対象の請求書は作成されていますが、会計（FI）への転記でエラーが発生している状態です。出荷処理が未完了という意味ではありません。  
>  
> 検証環境で確認したエラーは「得意先 1000193 が会社コード 1010 に定義されていない」という内容です。得意先の会社コードデータが不足している可能性があるため、会計・マスタデータ担当への確認が必要です。  
>  
> 重複請求を避けるため、同じ出荷に対して新しい請求書を作成したり、マスタデータを独自に変更したりせず、現在の請求書番号とエラーメッセージをサポート担当へお知らせください。  
>  
> なお、この文面は過去のSAP検証結果を使った**連絡文の練習**です。実際のユーザーへの連絡・作業依頼ではありません。

**Message assessment:** Explains invoice existence versus FI transfer, names the error, identifies the correct cross-functional owner and avoids recommending an unauthorized or duplicate transaction. No Japanese-language reviewer, recipient or actual business confirmation is recorded.

## 5. Proposed cross-regional communication and escalation sequence

1. **Japan Sales** captures invoice identifier, exact error, business impact estimate, and contact channel, with no invented production impact.
2. **Singapore Logistics** provides already-completed pick/PGI references; do not reopen fulfillment without evidence of a logistics issue.
3. **APAC L2 SD** records the verified SAP findings, data gap and outstanding approval, then prepares the English handover packet.
4. **UK FI L2** would explicitly accept ownership before performing authorized master-data review; the acceptance is **hypothetical**.
5. Following an approved correction, the responsible team would verify the original invoice's FI journal and balances; the historical training retest **already** showed journal 9400000057.
6. **APAC Sales** would communicate a verified outcome and close only with business agreement in a real support service. No such communications or closure occurred in M9.

### Escalation triggers for a real operation

Escalate to **FI/master-data owner** for missing customer company-code data; to **SD configuration** only if the problem persists with correct data or involves actual billing-control behavior; to **Security** if an authorized role is denied access; and to **business/change governance** before an unapproved process or configuration change. The separate CBC denial (INC-SD-006) is **not** the demonstrated cause of the historical FI error.

## 6. Evidence and exercise result

| Reference | How used | Classification |
|---|---|---|
| EV-017–EV-020 | Fulfillment / saved invoice context | Reused executed JV2 evidence |
| EV-021–EV-023 | FI transfer error and missing data | Reused executed JV2 evidence |
| EV-024–EV-026 | Historical corrective activity and balanced FI retest | Reused executed JV2 evidence; EV-024 shows draft fields only |
| EV-074–EV-076 | Independent invoice / journal follow-up | Reused executed JV2 evidence |
| This document | Hand-over scenario, English escalation and Japanese response | **New documentation / simulated**, no SAP action |

**Outcome:** M9.01–M9.02 documentation exercises prepared. **R14/R15 supported at a simulated communication-design level only.** No real multinational incident ownership, communication performance, or Japanese/English customer support delivery is evidenced.
