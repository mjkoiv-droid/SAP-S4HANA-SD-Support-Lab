
# SAP SD — Order-to-Cash Process Trace

## 1. Scenario Information

| Field | Value |
|---|---|
| Scenario ID | O2C-SD-XXX |
| Scenario Title | |
| Scenario Type | Standard / Partial Delivery / Return / Export |
| SAP System / Client | |
| Execution Date | |
| Executed By | Mikko Koivistoinen |
| Status | Not Started |
| Execution Type | Executed / Simulated / Blocked |
| Related Requirement | R02 |

## 2. Business Scenario

**Business background:**

**Customer requirement:**

**Products / Materials:**

**Expected business outcome:**

**Special conditions or exceptions:**

## 3. Organizational and Master Data

| Data Object | SAP Value | Description |
|---|---|---|
| Company Code | | |
| Sales Organization | | |
| Distribution Channel | | |
| Division | | |
| Sales Area | | |
| Plant | | |
| Shipping Point | | |
| Customer / Business Partner | | |
| Material | | |
| Order Quantity | | |
| Currency | | |

## 4. Sales Order Processing

**Transaction:** VA01 / VA02 / VA03 or Fiori equivalent

| Field | Value / Result |
|---|---|
| Sales Document Type | |
| Sales Order Number | |
| Sold-to Party | |
| Ship-to Party | |
| Material | |
| Order Quantity | |
| Net Value | |
| Requested Delivery Date | |
| Confirmed Quantity | |
| Delivery Block | |
| Billing Block | |

### Pricing Verification

| Pricing Element | Condition Type | Expected Value | Actual Value |
|---|---|---|---|
| Base Price | | | |
| Discount | | | |
| Freight | | | |
| Tax | | | |
| Net Value | | | |

**Pricing analysis findings:**

**Availability and scheduling findings:**

**Sales order status:**

**Evidence references:**

## 5. Outbound Delivery

**Transaction:** VL01N / VL02N / VL03N or Fiori equivalent

| Field | Value / Result |
|---|---|
| Outbound Delivery Number | |
| Delivery Type | |
| Shipping Point | |
| Plant | |
| Storage Location | |
| Delivery Quantity | |
| Picking Quantity | |
| Picking Status | |
| Goods Movement Status | |

### Delivery Processing

**Delivery creation:**

**Picking execution:**

**Quantity verification:**

**Exceptions or warnings:**

**Evidence references:**

## 6. Post Goods Issue (PGI)

**Transaction:** VL02N or Fiori equivalent

| Field | Value / Result |
|---|---|
| PGI Posting Date | |
| Material Document Number | |
| Movement Type | |
| Quantity Posted | |
| Stock Before PGI | |
| Stock After PGI | |
| Goods Movement Status | |

**Inventory impact:**

**Accounting impact, if applicable:**

**Evidence references:**

## 7. Billing

**Transaction:** VF01 / VF03 or Fiori equivalent

| Field | Value / Result |
|---|---|
| Billing Document Number | |
| Billing Type | |
| Billing Date | |
| Billing Quantity | |
| Net Amount | |
| Tax Amount | |
| Gross Amount | |
| Accounting Status | |

**Billing relevance and copy control:**

**Billing exceptions or blocks:**

**Evidence references:**

## 8. SD–FI Integration

| Field | Value / Result |
|---|---|
| Accounting Document Number | |
| Company Code | |
| Fiscal Year | |
| Customer Receivables Account | |
| Revenue Account | |
| Tax Account, if applicable | |
| Posting Date | |
| Accounting Document Status | |

### FI Verification

**Customer receivable posting:**

**Revenue recognition / posting:**

**Tax posting:**

**Reconciliation findings:**

**Evidence references:**

## 9. Complete O2C Document Flow

| Process Step | SAP Document Number | Status | Evidence ID |
|---|---|---|---|
| Sales Order | | | |
| Outbound Delivery | | | |
| Material Document / PGI | | | |
| Billing Document | | | |
| FI Accounting Document | | | |

### Document Flow Verification

**Transaction:** VA03 / VL03N / VF03 or equivalent

**Ordered quantity:**

**Delivered quantity:**

**Billed quantity:**

**Document chain completeness:**

**Unresolved inconsistencies:**

## 10. Exception and Troubleshooting Analysis

**Observed exception:**

**Business impact:**

**Investigation:**

**Root cause / findings:**

**Correction or proposed action:**

**Retest result:**

**Related incident ID, if applicable:**

## 11. Process Validation

| Test | Expected Result | Actual Result | Status |
|---|---|---|---|
| Sales order creation | | | |
| Pricing determination | | | |
| Availability confirmation | | | |
| Delivery creation | | | |
| Picking completion | | | |
| PGI posting | | | |
| Billing creation | | | |
| FI integration | | | |
| Document flow reconciliation | | | |

## 12. Business Process Assessment

**Sales perspective:**

**Logistics perspective:**

**Finance perspective:**

**Process risks and controls:**

**Improvement opportunities:**

## 13. Final Results

**Scenario outcome:** Pass / Fail / Partial / Blocked

**Successfully completed steps:**

**Outstanding issues:**

**Business outcome:**

**Lessons learned:**

## 14. Evidence Register

| Evidence ID | Description | File / Link |
|---|---|---|
| EV-XXX | Sales order and pricing | |
| EV-XXX | Outbound delivery and picking | |
| EV-XXX | Post Goods Issue | |
| EV-XXX | Billing document | |
| EV-XXX | FI accounting document | |
| EV-XXX | Complete document flow | |

---

**Evidence integrity:** Record actual SAP document numbers and verified results. Clearly distinguish executed transactions from simulated or blocked steps. Do not claim a complete O2C cycle unless the required documents and integration steps have been verified.
