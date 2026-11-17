# M2 — Executed O2C Swimlane and Exception Decision Points

**System:** SAP S/4HANA Cloud Public Edition training sandbox JV2 / 100.  
**Dates:** 16–17 November 2026. **No production client activity.**  
**Scope:** Executed **Sales → Logistics → Finance** document links for orders 1055 and 1056, with two observed exceptions.

## Process swimlane — actual document identifiers

```mermaid
flowchart LR
    subgraph Sales[Sales]
        S1[Order 1055 • TG11 1 PC]
        S2[Order 1056 • TG11 1 PC • block 04]
    end
    subgraph Logistics[Logistics / MM]
        L1[Delivery 80000784]
        L2[Picking 1 PC + PGI 4900001488]
        L3[Delivery 80000785]
        L4[Picking 1 PC + PGI 4900001489]
    end
    subgraph Billing[SD Billing]
        B1[Invoice F2 90000303]
        B2[Invoice F2 90000304]
    end
    subgraph Finance[Finance / FI]
        F1{Customer 1000193 extended to company 1010?}
        F2[Master data corrected: 1010 / AR 12100000 / NT30]
        F3[FI RV 9400000057 • EUR 20.88]
        F4[FI RV 9400000058 • EUR 20.88]
    end
    S1 --> L1 --> L2 --> B1 --> F1
    F1 -->|Initially no| F2 --> F3
    S2 --> L3 --> L4 --> B2 --> F4
    S2 -.->|Block 04 persisted; NOT enforced for observed F2 delivery billing| B2
```

**Important:** The chart illustrates verified document chains, not actual physical delivery dates or an independently proven billing-block configuration mechanism. The failure at 90000303 was resolved via customer company-code setup. The billing-block behavior on order 1056 remains open.

## Exception decision points and control ownership

| Stage | Decision / control | Scenario 1 actual | Scenario 2 actual | Primary functional owner |
|---|---|---|---|---|
| Sales order | Sold-to/ship-to, material, sales area, pricing and ATP valid? | Standard item; prior M1 block removed | Confirmed 1 PC, schedule line CP | Sales / SD |
| Delivery creation | Eligible schedule/quantity and no delivery block? | 80000784 created | 80000785 created | Logistics / SD |
| Picking / PGI | Picked qty = delivery qty, material document created? | 1 PC; PGI 4900001488 | 1 PC; PGI 4900001489 | Warehouse / MM |
| Billing | Invoice correct and billing control enforced? | F2 90000303; no billing-block test | F2 90000304 **created despite block 04** | Billing / SD |
| FI interface | Customer accounting master present and journal created? | First failed for missing company code; corrected | RV 9400000058 created | FI / Customer master |
| FI reconciliation | Receivable = revenue + output tax? | 20.88 = 17.55 + 3.33 | 20.88 = 17.55 + 3.33 | FI |
| Receivables | Payment recorded and invoice cleared? | Not performed | Not performed | FI / AR |

## Related evidence

[Scenario 1 trace](O2C-Scenario-01-Standard-and-FI-Correction.md) · [Scenario 2 trace](O2C-Scenario-02-Billing-Block-Exception.md) · [Evidence register](../00-Project-Tracking/Evidence-Register.md).
