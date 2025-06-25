# Order Service

## Overview
Manages order lifecycle and acts as the Saga initiator.

## Responsibilities
- Accept order requests & persist in `orders` table.
- Emit `order.created` event.
- Update order state machine on subsequent events (`paid`, `shipped`, `failed`).

## Public API
| Method | Path | Description |
|--------|------|-------------|
| POST   | /orders          | Create new order |
| GET    | /orders/{id}     | Order status |
| GET    | /orders/user/{u} | Orders by user |

## Data Model
```sql
CREATE TABLE orders (
  id            UUID PRIMARY KEY,
  user_id       UUID NOT NULL,
  status        VARCHAR(32) NOT NULL,
  total_amount  NUMERIC(12,2),
  created_at    TIMESTAMP DEFAULT now()
);
```

## Events
| Topic            | Direction |
|------------------|-----------|
| order.created    | →         |
| order.paid       | ←         |
| order.failed     | ← / →     |
| order.shipped    | ←         |

## Idempotency
Orders carry `client_reference_id` to deduplicate retries.

## Resilience
- State machine persisted; events replay‑safe
- Compensation on `order.failed`

## Metrics
- `orders_created_total`
- `order_state_change_latency_ms`