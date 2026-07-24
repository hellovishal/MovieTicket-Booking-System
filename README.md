# 🎬 Movie Ticket Booking System

> A production-grade backend for an online Movie Ticket Booking platform built using **Java 21**, **Spring Boot 3**, **PostgreSQL**, **Redis**, **Apache Kafka**, and modern backend engineering practices.

---

## 📖 Overview

The Movie Ticket Booking System is a scalable, cloud-ready backend service that enables users to discover movies, browse theatres, reserve seats, make bookings, and receive booking notifications.

The project is intentionally designed using **real-world software engineering principles** instead of an academic CRUD application. Every feature is implemented incrementally with production-quality architecture, clean code, proper layering, comprehensive testing, and Git history that mirrors an enterprise development workflow.

The primary goals of this project are:

* Demonstrate strong backend engineering skills
* Showcase scalable system design principles
* Implement concurrency-safe seat booking
* Follow enterprise development standards
* Serve as an interview-ready portfolio project

---

# ✨ Features

## Customer Features

* User Registration & Login
* JWT Authentication
* Browse Movies
* Browse Cities
* Browse Theatres
* Browse Shows
* Seat Availability
* Seat Hold with Expiration
* Book Tickets
* Cancel Booking
* Booking History
* View Booking Details
* Dynamic Pricing
* Coupon Support
* Notification Delivery

---

## Admin Features

* Manage Movies
* Manage Cities
* Manage Theatres
* Manage Screens
* Manage Seat Layouts
* Manage Shows
* Configure Pricing Rules
* Configure Coupons

---

# 🏗️ System Architecture

```
                    Client Applications
        Web | Mobile | Swagger | Postman
                       |
                REST Controllers
                       |
                Service Layer
                       |
    ------------------------------------------
    |                 |                      |
 Redis (Seat Hold)   PostgreSQL        Kafka Events
    |                 |                      |
    |                 |              Notification Service
    |                 |
  Caching        Persistent Storage
```

---

# 🛠️ Technology Stack

| Category              | Technology            |
| --------------------- | --------------------- |
| Language              | Java 21               |
| Framework             | Spring Boot 3         |
| Build Tool            | Gradle (Kotlin DSL)   |
| Database              | PostgreSQL            |
| Cache                 | Redis                 |
| Messaging             | Apache Kafka          |
| ORM                   | Spring Data JPA       |
| Migration             | Flyway                |
| Security              | Spring Security + JWT |
| API Documentation     | OpenAPI / Swagger     |
| Testing               | JUnit 5               |
| Integration Testing   | Testcontainers        |
| Logging               | Logback               |
| Validation            | Jakarta Validation    |
| Mapping               | MapStruct             |
| Boilerplate Reduction | Lombok                |

---

# 📂 Project Structure

```
src/main/java/com/moviebooking

├── auth
├── booking
├── city
├── common
├── config
├── exception
├── infrastructure
│     ├── kafka
│     ├── redis
│     └── persistence
├── movie
├── notification
├── payment
├── pricing
├── refund
├── screen
├── security
├── seat
├── show
├── theatre
└── user
```

Each module follows a feature-based architecture:

```
feature/

controller/

service/

repository/

entity/

dto/

mapper/

exception/
```

---

# 🚀 Architecture Principles

This project follows:

* Feature-based modular architecture
* Layered design
* SOLID principles
* Clean Code
* DRY
* Dependency Injection
* Single Responsibility Principle
* Stateless APIs
* RESTful API Design
* Exception-first development

---

# 🔐 Authentication

Authentication is implemented using JWT.

Features include:

* User Registration
* Login
* BCrypt Password Encoding
* Stateless Authentication
* Role-Based Authorization
* JWT Token Validation
* Spring Security Filter Chain

Roles:

* CUSTOMER
* ADMIN

---

# 💺 Seat Booking Workflow

```
User

↓

Browse Shows

↓

View Seat Availability

↓

Hold Seats (Redis)

↓

Mock Payment

↓

Booking Confirmed

↓

Persist Booking

↓

Kafka Event Published

↓

Notification Sent
```

---

# ⚡ Seat Hold Mechanism

To avoid double booking:

* Seats are first placed on hold.
* Seat holds are stored in Redis.
* Holds automatically expire.
* Expired seats become available again.
* Only confirmed bookings are persisted.

---

# 💰 Pricing Engine

The pricing module supports:

* Base Price
* Premium Seats
* Weekend Pricing
* Holiday Pricing
* Coupon Discounts
* Dynamic Pricing Rules

Pricing follows the Strategy Pattern, allowing new pricing rules to be added without modifying existing code.

---

# 📩 Notification System

Booking events are published to Kafka.

Supported notifications:

* Booking Confirmed
* Booking Cancelled
* Refund Processed

Future integrations:

* Email
* SMS
* Push Notifications

---

# 💳 Payment

To keep the project focused on backend architecture, payment gateways are mocked.

The project includes:

* PaymentService Interface
* Mock Payment Provider

Supported outcomes:

* SUCCESS
* FAILURE
* TIMEOUT

This abstraction allows easy integration with providers such as Stripe or Razorpay in the future.

---

# 🗄️ Database

Schema management is handled using Flyway.

Each feature introduces its own migration.

Example:

```
V1__init.sql

V2__create_users.sql

V3__create_movies.sql

V4__create_theatres.sql

V5__create_shows.sql
```

No schema is managed using Hibernate auto-DDL.

---

# 📚 API Documentation

Swagger UI is available at:

```
http://localhost:8080/swagger-ui
```

OpenAPI Specification:

```
http://localhost:8080/api-docs
```

---

# ❤️ Health Checks

Spring Boot Actuator exposes:

```
/actuator/health

/actuator/info

/actuator/metrics
```

---

# 🐳 Running the Project

## Prerequisites

* Java 21
* Docker
* Docker Compose
* Gradle

---

### Clone Repository

```bash
git clone <repository-url>

cd movie-ticket-booking
```

---

### Start Infrastructure

```bash
docker compose up -d
```

This starts:

* PostgreSQL
* Redis
* Kafka

---

### Run Application

```bash
./gradlew bootRun
```

---

### Execute Tests

```bash
./gradlew test
```

---

### Build Project

```bash
./gradlew clean build
```

---

# 🧪 Testing Strategy

The project includes:

* Unit Tests
* Repository Tests
* Service Tests
* Controller Tests
* Integration Tests
* Concurrency Tests
* Testcontainers

Coverage target:

* **90%+**

---

# 📈 Planned Development Roadmap

The project is developed incrementally across multiple commits.

| Commit | Description                        |
| ------ | ---------------------------------- |
| 1      | Project Bootstrap & Infrastructure |
| 2      | JWT Authentication & Authorization |
| 3      | City, Theatre, Screen Management   |
| 4      | Movies & Show Scheduling           |
| 5      | Browse APIs                        |
| 6      | Redis Seat Hold Engine             |
| 7      | Booking Workflow                   |
| 8      | Cancellation & Refund              |
| 9      | Kafka Notification System          |
| 10     | Testing & Concurrency              |
| 11     | Observability                      |
| 12     | Production Readiness               |

---

# 🚀 Future Enhancements

Potential improvements include:

* Multi-language support
* Elasticsearch-powered movie search
* Recommendation engine
* Loyalty & rewards program
* Waitlist for sold-out shows
* QR-code based ticket validation
* WebSocket live seat availability
* Distributed locking
* Kubernetes deployment
* CI/CD with GitHub Actions
* Prometheus & Grafana dashboards
* Distributed tracing with OpenTelemetry

---

# 📖 Learning Objectives

This project demonstrates practical experience with:

* Spring Boot
* Distributed Systems
* REST API Design
* Security
* Authentication
* Database Design
* Redis
* Kafka
* Flyway
* Docker
* Clean Architecture
* Feature-Based Modular Design
* Concurrent Programming
* Event-Driven Architecture
* Enterprise Backend Development

---

# 🤝 Contributing

Contributions, suggestions, and improvements are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Commit your changes.
4. Open a Pull Request.

---

# 📄 License

This project is licensed under the MIT License.

---

# 👨‍💻 Author

**Vishal Rajak**

Backend Software Engineer

Java • Spring Boot • Distributed Systems • Kafka • Redis • PostgreSQL • Cloud-Native Applications
