# Payment Service

## Overview
Handles payment authorisation and capture via third‑party PSP.

## Responsibilities
- Authorise card/payment.
- Capture funds on shipment confirmation (if deferred).
- Emit payment success/failure events.

## Endpoints (Internal)
| Method | Path | Description |
|--------|------|-------------|
| POST   | /payments          | Authorise payment |

## External Integrations
- Stripe (REST API)
- Use Webhooks → `/payments/webhook`

## Events
| Topic            | Direction |
|------------------|-----------|
| payment.success  | →         |
| payment.failed   | →         |
| inventory.reserved | ←       |

## Resilience
- Retry with exponential back‑off (Resilience4j)
- Circuit breaker for PSP API

## Secrets
- `PAYMENT_API_KEY` (K8s Secret)