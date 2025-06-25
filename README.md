# 🌐 Distributed System Projects

Welcome to the **Distributed System Learning Repository** — a curated collection of real-world projects focused on solving common challenges in distributed systems using modern Java backend technologies.

This repository is built for **engineers, architects, and learners** who want to understand the internals of distributed systems by working with practical, production-grade microservices examples.

---

## 🧭 Goals

- Design and implement fault-tolerant, scalable systems
- Master patterns like Saga, 2PC, and event-driven architecture
- Handle real-world challenges: rate limiting, retries, observability, data consistency
- Build distributed systems that can handle **10K+ RPM**

---

## 🏗️ Repository Overview

Each folder in this repository is a **standalone Spring Boot project** with its own purpose and configuration. These projects cover architectural patterns, system design practices, and infrastructure capabilities essential to distributed computing.

### 📁 Directory Layout

```bash
distributed-system/
├── 01-rate-limiter/
├── 02-saga-orchestration/
├── 03-saga-choreography/
├── 04-2pc-coordinator/
├── 05-open-telemetry-logging-library/
├── 06-kafka-keycloak-auth/
├── 07-recommendation-engine/
├── 08-microservices-observability/
├── 09-etl-spring-batch-pipeline/
├── 10-api-gateway-eureka-loadbalancer/
└── 11-order-processing-system/
```

---

## 🔧 Tech Stack

| Layer            | Technologies                                                                 |
|------------------|------------------------------------------------------------------------------|
| **Backend**       | Java, Spring Boot, Spring Cloud                                              |
| **Messaging**     | Kafka, RabbitMQ                                                              |
| **Database**      | PostgreSQL, MySQL, Redis                                                     |
| **Security**      | Keycloak, OAuth2, Spring Security                                            |
| **Infrastructure**| Docker, Docker Compose, Kubernetes                                           |
| **Monitoring**    | OpenTelemetry, Prometheus, Grafana                                           |
| **ETL/Batch**     | Spring Batch                                                                 |
| **Testing**       | JUnit, TestContainers, Mockito                                               |

---

## 📦 Project Index

Each project below is an isolated Spring Boot module demonstrating a specific distributed system concept.

### 🔄 Core Distributed Patterns

- 🧱 **[01 - Rate Limiter](./01-rate-limiter/README.md)**  
  Token Bucket, Leaky Bucket, and Sliding Window rate limiting strategies.

- ⚙️ **[02 - Saga Orchestration](./02-saga-orchestration/README.md)**  
  Orchestrated Saga pattern using a command-based transaction manager and Kafka.

- 🔗 **[03 - Saga Choreography](./03-saga-choreography/README.md)**  
  Decentralized Saga pattern where services react to events and trigger next actions.

- 💡 **[04 - 2PC Coordinator](./04-2pc-coordinator/README.md)**  
  Two-phase commit protocol with a coordinator ensuring distributed transaction integrity.

### 🔐 Security & Access Control

- 🔒 **[06 - Kafka Keycloak Auth](./06-kafka-keycloak-auth/README.md)**  
  OAuth2-secured Kafka client integration using Keycloak for producer/consumer authentication.

### 🧠 Recommendation & Business Logic

- 🛍️ **[07 - Recommendation Engine](./07-recommendation-engine/README.md)**  
  Product suggestion system based on user clickstream frequency.

- 📦 **[11 - Order Processing System](./11-order-processing-system/prd/real-time-order-processing-prd.md)**  
  High-throughput microservice architecture simulating scalable order workflows.

### 🔭 Observability & Logging

- 📈 **[05 - OpenTelemetry Logging Library](./05-open-telemetry-logging-library/README.md)**  
  Centralized, reusable tracing and logging library using OpenTelemetry SDK.

- 📊 **[08 - Microservices Observability](./08-microservices-observability/README.md)**  
  Distributed monitoring with Prometheus, Grafana, and OpenTelemetry integration.

### 🔄 ETL & Data Pipelines

- 🔄 **[09 - ETL Spring Batch Pipeline](./09-etl-spring-batch-pipeline/README.md)**  
  Batch data processing using Spring Batch with fault tolerance and partitioning.

### 🌐 Infrastructure & Routing

- 🌍 **[10 - API Gateway & Eureka Load Balancer](./10-api-gateway-eureka-loadbalancer/README.md)**  
  Spring Cloud Gateway setup with Eureka for service discovery and load-balanced routing.

---

## 🚀 Getting Started

### 🧪 Run a Project Locally

```bash
cd <project-folder>
./mvnw spring-boot:run
```

### 🐳 Run with Docker

```bash
docker-compose up --build
```

> Each sub-project includes its own `README.md` with usage instructions, config, and API reference.

---

## 🤝 Contribution Guidelines

We welcome contributions! Please consider the following before submitting PRs:

- Follow the existing code style and architecture
- Write meaningful commit messages
- Add test coverage for new features
- Raise an issue for discussion before proposing large changes

---

## 📜 License

This project is licensed under the **MIT License**. See [LICENSE](LICENSE) for details.

---

## 💬 Feedback

If you find this repository helpful, consider ⭐ starring it.  
Feel free to open issues for suggestions, bugs, or improvements.
