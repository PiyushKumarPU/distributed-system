# Product Service

## Overview
Catalog of products and stock metadata.

## Responsibilities
- CRUD for products.
- Expose search & filter APIs.
- Maintain product cache in Redis for fast lookups.

## Public Endpoints
| Method | Path | Description |
|--------|------|-------------|
| GET    | /products?query= | Search products |
| GET    | /products/{id}  | Get details |
| POST   | /products       | Create product |
| PUT    | /products/{id}  | Update product |

## Data Model
Tables: `products`, `product_images`, `product_attributes`.

## Kafka Events
| Topic              | Direction |
|--------------------|-----------|
| product.created    | →         |
| product.updated    | →         |

## Caching
- Redis hash per product: `product:{id}`
- TTL refreshed on update event

## Resilience
- Cache‑aside pattern
- Bulkhead pattern for DB calls