# Notification Service

## Overview
Sends transactional Emails/SMS/Push notifications.

## Responsibilities
- Consume domain events and map to templates.
- De‑duplication of messages per user.

## Events Consumed
- `order.created`, `order.shipped`, `order.failed`

## Providers
- SMTP (SendGrid)
- SMS (Twilio)

## Metrics
- `notifications_sent_total`
- `notification_delivery_failure_total`