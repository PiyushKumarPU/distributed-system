# Shipping Service

## Overview
Interfaces with logistics partners to create shipments and tracking numbers.

## Responsibilities
- Create shipping labels after payment.
- Track shipment status updates via webhook polling.

## Events
| Topic            | Direction |
|------------------|-----------|
| order.shipped    | →         |
| payment.success  | ←         |

## External Integrations
- FedEx/UPS REST
- Webhook endpoint `/shipments/webhook`

## Failure Handling
- Retry label creation
- Fallback to alternate carrier