
# Real-Time Distributed Order Processing System – PRD

## 📌 Title
**Real-Time Distributed Order Processing System**

## 🧭 Objective
To build a distributed, scalable microservices-based application that handles real-time user order submissions, payments, inventory management, and shipping coordination. The system must maintain resilience, eventual consistency (using patterns like Saga), and guarantee high availability and horizontal scalability to handle **10,000+ requests per minute**.

---

## 🧑‍💼 Target Users
- E-commerce platforms
- Logistics and delivery providers
- SaaS-based retail backend platforms

---

## 💼 Business Use Cases
- User places an order via mobile/web interface
- System processes the order:
  - Validates inventory
  - Reserves stock
  - Processes payment
  - Initiates shipping
  - Notifies user via Email/SMS
- System must remain functional under partial failure
- Admin should monitor the real-time status of orders

---

## 🔧 Functional Requirements

| Service              | Responsibilities                                         |
|----------------------|----------------------------------------------------------|
| [API Gateway](./api-gateway.md)          | Authentication, routing, rate-limiting                  |
| [User Service](./user-service.md)         | Register/login user, manage profile                     |
| [Product Service](./product-service.md)      | List/search products, manage stock                      |
| [Order Service](./order-service.md)        | Create/track orders, persist order status               |
| [Inventory Service](./inventory-service.md)    | Check/reserve/update stock levels                       |
| [Payment Service](./payment-service.md)      | Handle payment processing and validation                |
| [Shipping Service](./shipping-service.md)     | Schedule pickup, generate tracking                      |
| [Notification Service](./notification-service.md) | Email/SMS notifications                                 |
| [Orchestrator Service](./orchestrator-service.md) | Coordinates Sagas for distributed consistency (optional)|

---

## ⚙️ Non-Functional Requirements

- **Performance**: Handle 10K RPM with < 300ms latency (P95)
- **Availability**: ≥99.99%
- **Scalability**: Auto-scale via Kubernetes HPA
- **Fault Tolerance**: Services are isolated; circuit-breakers/retries in place
- **Consistency**: Eventual consistency using Saga pattern
- **Monitoring**: Prometheus, Grafana, OpenTelemetry
- **Security**: OAuth2 / JWT
- **Deployment**: Docker + Kubernetes (Minikube/GKE/EKS)

---

## 📐 Architecture Overview

```
              ┌──────────────┐
              │   Client     │
              └────┬─────────┘
                   │
         ┌─────────▼────────────┐
         │   API Gateway        │
         │(Routing + Security)  │
         └────────┬─────────────┘
     ┌────────────▼───────────────┐
     │         Order Service      │────────┐
     └────────────────────────────┘        │
     ┌────────────┐  ┌──────────────┐      │
     │User Service│  │Product Service│     │
     └────────────┘  └──────────────┘      ▼
     ┌────────────────────────────┐     Kafka Topics
     │      Inventory Service     │◄───────order.created
     └────────────────────────────┘
     ┌────────────────────────────┐       ▲
     │      Payment Service       │◄──────┘
     └────────────────────────────┘
     ┌────────────────────────────┐
     │     Shipping Service       │
     └────────────────────────────┘
     ┌────────────────────────────┐
     │  Notification Service      │
     └────────────────────────────┘
```

---

## 🧵 Data Flow (Happy Path)

1. User submits an order (`/api/orders`)
2. Order Service emits `order.created` Kafka event
3. Inventory Service reserves stock → emits `inventory.reserved`
4. Payment Service charges card → emits `payment.success`
5. Shipping is scheduled → emits `order.shipped`
6. Notification Service sends emails/SMS

---

## 🧪 Failure Scenarios and Resilience

| Scenario               | Strategy                                  |
|------------------------|-------------------------------------------|
| Inventory unavailable  | Emit `order.failed` → trigger refund      |
| Payment failure        | Compensating transaction → release stock  |
| Kafka down             | Use Outbox pattern and retry              |
| Duplicate requests     | Enforce idempotency keys                  |
| Service crash          | Use K8s restart + retries + DLQ           |
| Load spike             | Rate-limit at Gateway + auto-scale        |

---

## 🔁 Consistency Strategy

- Saga Pattern (Orchestration or Choreography)
- Kafka + Idempotent Events
- Distributed locks via Redis (if needed)
- Outbox pattern for atomic event publishing
- Retry + Dead-letter queue for failures

---

## 📦 Sample API Contracts

### Order Service
```
POST   /api/orders
GET    /api/orders/{orderId}
```

### Product Service
```
GET    /api/products
POST   /api/products
```

### Inventory Service
```
POST   /api/inventory/reserve
POST   /api/inventory/release
```

---

## 📊 Observability

- **Metrics**: Prometheus (latency, throughput, error rates)
- **Tracing**: OpenTelemetry + Jaeger
- **Logging**: Loki or ELK
- **Dashboards**: Grafana

---

## 🧪 Testing Strategy

- Spring Boot Unit & Integration tests
- Kafka event testing using TestContainers
- Chaos testing (random failure injection)
- Load testing: Gatling / JMeter (10K+ RPM)
- Contract Testing: Pact

---

## 🚀 Deployment Plan

- Local: Docker Compose
- Production: Kubernetes + Helm
- CI/CD: GitHub Actions / Jenkins
- Secrets: Kubernetes Secrets / Vault
- Monitoring: Prometheus Operator
- Tracing: OpenTelemetry Collector

---

## 📚 Deliverables

- Microservices source code (GitHub)
- Dockerfiles for each service
- Helm charts for Kubernetes deployment
- OpenAPI Specs (Swagger)
- Prometheus + Grafana dashboards
- Load testing report and tuning insights
- README and runbook documentation
