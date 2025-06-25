# Orchestrator Service (Saga Manager)

## Overview
Coordinates the Saga for distributed order processing.

## Responsibilities
- Listen for `order.created` events.
- Call Inventory → Payment → Shipping sequentially.
- Handle compensating actions on failure.

## Implementation
- Spring Boot + State Machine (Spring Statemachine).
- Persistent Saga instances in `saga_state` table.

## Failure Handling
- Timeout detection & compensation.
- DLQ handler for unrecoverable messages.