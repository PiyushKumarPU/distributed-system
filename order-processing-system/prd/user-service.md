# User Service

## Overview
Provides CRUD operations for user profiles and issues JWT tokens.

## Responsibilities
- Register / authenticate users.
- Manage profile preferences & addresses.
- Issue / refresh OAuth2 JWT tokens.
- Publish user‑related domain events.

## Public Endpoints
| Method | Path | Description |
|--------|------|-------------|
| POST   | /users           | Register new user |
| POST   | /auth/login      | Login & token issuance |
| GET    | /users/{id}      | Fetch user profile |
| PUT    | /users/{id}      | Update user profile |

## Data Model (PostgreSQL)
```sql
CREATE TABLE users (
  id               UUID PRIMARY KEY,
  email            VARCHAR(255) UNIQUE NOT NULL,
  password_hash    VARCHAR(95) NOT NULL,
  full_name        VARCHAR(255),
  created_at       TIMESTAMP WITH TIME ZONE DEFAULT now(),
  updated_at       TIMESTAMP WITH TIME ZONE
);
```

## Kafka Events
| Topic            | Direction | Payload |
|------------------|-----------|---------|
| user.registered  | →         | `{ id, email, createdAt }` |

## Failure & Resilience
- Password hashing via BCrypt (12 rounds)
- Rate‑limit login attempts (Redis counter)
- Transactional outbox for event publishing

## Metrics
- `user_login_success_total`
- `user_login_failure_total`
- `db_query_latency_ms`