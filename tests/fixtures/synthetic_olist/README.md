# Synthetic Olist contract fixture

This test-only dataset contains eight deliberately designed orders. It is not used for portfolio
findings and does not replace the real Olist source data.

| Order | Edge case | Expected governed behavior |
|---|---|---|
| `ORDER_A` | Delivered later on the promised calendar day | On time; timestamp comparison would be wrong |
| `ORDER_B` | Delivered one day late and handed over after item deadline | Delivery late; Handover SLA breached |
| `ORDER_C` | Two sellers in one order | Included in customer SLA; excluded from primary seller SLA |
| `ORDER_D` | Missing `shipping_limit_date` | Handover candidate but excluded from denominator |
| `ORDER_E` | Canceled order with an item | Counted as canceled; excluded from delivery and Handover SLA |
| `ORDER_F` | Unavailable order without items | Counted separately from cancellations |
| `ORDER_G` | Carrier timestamp before approval | Excluded only from pre-carrier duration |
| `ORDER_H` | Two items, two payments, two reviews | No join inflation; latest answered review is representative |

Expected January 2018 KPI contract:

- total orders: 8;
- delivered orders: 6;
- canceled orders: 1;
- unavailable orders: 1;
- delivery-SLA eligible: 6;
- on-time deliveries: 4;
- primary Handover candidates: 5;
- primary Handover-SLA eligible: 4;
- Handover breaches: 1.

