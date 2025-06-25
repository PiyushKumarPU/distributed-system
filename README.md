Here is an updated and more meaningful `README.md` for your `distributed-system` GitHub repository. It includes a clear description, structure, and a table linking to the individual projects:

---

````markdown
# Distributed System

A curated collection of hands-on projects, solutions, and patterns to help understand and solve real-world problems in distributed systems.

This repository is designed for engineers and architects aiming to build scalable, fault-tolerant, and resilient distributed systems. Each project demonstrates a specific aspect of distributed computing such as consistency, availability, partition tolerance, data replication, distributed transactions, rate limiting, logging, and monitoring.

## 📌 Repository Structure

Each folder in this repository is a standalone Spring Boot-based microservice or component demonstrating one or more distributed systems principles. Technologies used include:

- **Java & Spring Boot**
- **Kafka / RabbitMQ**
- **PostgreSQL / Redis**
- **Docker / Kubernetes**
- **OpenTelemetry / Prometheus / Grafana**

## 🧠 Topics Covered

- Service Discovery & Load Balancing
- Distributed Transactions (2PC, Saga)
- Rate Limiting Algorithms
- Distributed Logging & Tracing
- Event-Driven Architecture with Kafka
- Fault Tolerance & Retry Mechanisms
- CAP Theorem-Based Design Scenarios
- Consistency Patterns and Versioning
- Schema Evolution in ETL Pipelines

## 📂 Project Index

| Project Name                                      | Description                                                              | Link                                                                 |
|--------------------------------------------------|--------------------------------------------------------------------------|----------------------------------------------------------------------|
| **01-rate-limiter**                              | Implementation of Token Bucket, Leaky Bucket, and Sliding Window models | [View Project](./01-rate-limiter)                                    |
| **02-saga-orchestration**                        | Saga pattern using orchestration via Spring Boot + Kafka                | [View Project](./02-saga-orchestration)                              |
| **03-saga-choreography**                         | Choreography pattern with decoupled microservices & Kafka               | [View Project](./03-saga-choreography)                               |
| **04-2pc-coordinator**                           | Two-phase commit implementation with a transaction coordinator          | [View Project](./04-2pc-coordinator)                                 |
| **05-open-telemetry-logging-library**            | Custom tracing and logging library using OpenTelemetry                  | [View Project](./05-open-telemetry-logging-library)                  |
| **06-kafka-keycloak-auth**                       | Kafka integration with Keycloak for OAuth2-secured producers/consumers | [View Project](./06-kafka-keycloak-auth)                             |
| **07-recommendation-engine**                     | Product recommendation using clickstream data                           | [View Project](./07-recommendation-engine)                           |
| **08-microservices-observability**               | Distributed observability stack: Prometheus + Grafana + OpenTelemetry   | [View Project](./08-microservices-observability)                     |
| **09-etl-spring-batch-pipeline**                 | ETL processing using Spring Batch with fault tolerance & partitioning   | [View Project](./09-etl-spring-batch-pipeline)                       |
| **10-api-gateway-eureka-loadbalancer**           | Microservice ecosystem with API Gateway, Eureka, load-balanced services| [View Project](./10-api-gateway-eureka-loadbalancer)   
| **11-order-processing-system**           | Microservices architecture designed to simulate a high-throughput, high-load order processing system | [View Project](./11-order-processing-system/) |            |

> 📁 *More projects coming soon...*

## 🚀 Getting Started

To run any project:

```bash
cd <project-folder>
./mvnw spring-boot:run
````

Docker-based projects can be run using:

```bash
docker-compose up --build
```

## 🤝 Contributions

Feel free to fork, raise PRs, or open issues. This repo is a continuous learning exercise—improvements, suggestions, and bug fixes are always welcome!

## 📜 License

[MIT License](LICENSE)

```

---

Let me know if you'd like me to generate the folder structures and `README.md` for each subproject (`01-rate-limiter`, `02-saga-orchestration`, etc.), or if you'd like the full content as a downloadable ZIP.
```
