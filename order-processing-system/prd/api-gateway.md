# API Gateway

## Overview
Acts as the single entry‑point into the system, handling request routing, cross‑cutting concerns (auth, rate‑limiting), and simple edge aggregation.

## Responsibilities
- **Routing** incoming HTTP requests to the correct downstream service.
- **Authentication & Authorization** via OAuth2/JWT.
- **Rate‑Limiting & Quotas** per user/IP.
- **Cross‑Cutting Filters** (CORS, compression, tracing headers).
- **Fallbacks** for graceful degradation when downstream is unavailable.

## Endpoints
| Method | Path | Description | Auth |
|--------|------|-------------|------|
| GET    | /api/\* | Proxy to specific service | ✅ |
| POST   | /login | Token issuance | ❌ |

## Data Model
_No persistent storage._ Uses Redis for rate‑limit counters.

## Kafka Events
None (stateless).

## Failure Handling
- HTTP 429 for rate‑limit exhaustion  
- Circuit‑breaker fallback → static “Service Unavailable” page  
- Retries for **idempotent** GETs (configurable)

## Scaling
- **Horizontal:** K8s HPA on CPU+RPS
- **Peak Load:** 20K RPS

## Metrics
- `gateway_requests_total{status=…}`
- `gateway_latency_ms_bucket`
- `gateway_rate_limit_dropped`

## Configuration (env)
| Variable | Description | Default |
|----------|-------------|---------|
| GATEWAY_RATE_LIMIT_PER_MIN | Allowed requests/min per token | 1200 |
| GATEWAY_CIRCUIT_BREAKER_THRESHOLD | % errors to open breaker | 50 |