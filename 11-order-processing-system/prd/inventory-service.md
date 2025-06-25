# Inventory Service

## Overview
Ensures stock consistency with optimistic locking.

## Responsibilities
- Reserve / release inventory for orders.
- Synchronize stock levels from warehouse feed.

## Internal Endpoints
| Method | Path | Description |
|--------|------|-------------|
| POST   | /inventory/reserve   | Reserve items |
| POST   | /inventory/release   | Release items |

## Data Model
```sql
CREATE TABLE inventory (
  product_id   UUID PRIMARY KEY,
  quantity     INTEGER NOT NULL,
  reserved     INTEGER NOT NULL DEFAULT 0,
  updated_at   TIMESTAMP
);
```

Uses PostgreSQL row‑level locks (`SELECT ... FOR UPDATE`) to avoid race conditions.

## Events
| Topic                 | Direction |
|-----------------------|-----------|
| inventory.reserved    | →         |
| inventory.not_enough  | →         |
| inventory.released    | →         |
| order.created         | ←         |

## Failure Strategy
- If reservation fails → publish `inventory.not_enough`
- Timeout watcher releases stale reservations