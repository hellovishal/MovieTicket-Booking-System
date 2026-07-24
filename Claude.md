
# Agents.md — Movie Ticket Booking System (SDE-2)

## Objective
Build a production-quality Spring Boot backend for a Movie Ticket Booking System in **48 hours**.

The primary goal is not just to make the APIs work, but to demonstrate:
- Clean architecture
- Good domain modeling
- Concurrency handling
- Scalable design
- Production engineering practices
- Testability

The assignment explicitly values engineering decisions more than feature count.

---

# Tech Stack

- Java 21
- Spring Boot 3
- Spring Data JPA
- PostgreSQL
- Flyway
- Spring Security (JWT)
- Bean Validation
- Redis (Seat Hold)
- RabbitMQ/Kafka (Notification)
- JUnit5
- Testcontainers
- Mockito
- Lombok
- MapStruct

---

# Overall Development Strategy

Never generate everything at once.

Work in phases.

Every phase must:
1. compile
2. pass tests
3. have meaningful commits

---

# Architecture

Use Clean Architecture.

```
controller
service
repository
entity
dto
mapper
security
exception
config
event
notification
pricing
payment
booking
seat
hold
refund
```

Business logic must never be inside Controllers.

---

# Domain Model

Design entities:

- User
- Role
- City
- Theater
- Screen
- Seat
- Movie
- Show
- PricingRule
- SeatHold
- Booking
- BookingSeat
- Payment
- Refund
- Coupon

Relationships should be normalized.

---

# Functional Modules

## Phase 1

Project setup

Generate:

- Gradle/Maven
- Folder structure
- Docker Compose
- Flyway
- Base configs

---

## Phase 2

Authentication

Admin

Customer

JWT

RBAC

---

## Phase 3

Admin APIs

Implement CRUD for:

- City
- Theater
- Screen
- Movie
- Show
- Seat Layout
- Pricing
- Refund Policy

---

## Phase 4

Customer APIs

Implement:

Browse cities

Browse theatres

Browse movies

Browse shows

Show seat availability

---

## Phase 5

Seat Hold

Critical module.

Requirements:

- Hold seats
- 5 minute expiry
- Auto release
- Redis
- Prevent duplicate hold

Think carefully about race conditions.

---

## Phase 6

Booking

Critical.

Requirements:

- Atomic booking
- Pessimistic locking
OR
Optimistic locking + retries

Never allow double booking.

Booking transaction must be ACID.

---

## Phase 7

Pricing Engine

Support:

Regular

Premium

Weekend

Coupon

Extensible Strategy Pattern.

---

## Phase 8

Payment

Dummy payment provider.

Support:

INITIATED

SUCCESS

FAILED

REFUNDED

---

## Phase 9

Cancellation

Refund policy

Examples:

100%

75%

50%

0%

based on show timing.

---

## Phase 10

Notifications

Booking Confirmation

Cancellation

Reminder

Must be asynchronous.

Never block booking API.

---

## Phase 11

Booking History

Customer

Booking details

Booking status

Payment status

---

# Non Functional Requirements

Design for:

- Scalability
- High cohesion
- Low coupling
- SOLID
- DRY
- Separation of concerns

---

# Concurrency

This is probably the most important evaluation point.

Think deeply before implementing.

Handle:

Two users booking same seat

Hold expiry

Payment timeout

Retries

Transaction rollback

Never rely on application memory.

---

# Design Patterns

Prefer:

Strategy

Factory

Builder

Observer

State

Repository

Template Method (where useful)

Avoid over-engineering.

---

# Testing

Write:

Unit Tests

Integration Tests

Repository Tests

Controller Tests

Concurrency Test

Cover:

Seat booking race condition

Refund

Coupon

Pricing

---

# README

README must contain:

Architecture

ER Diagram

API list

Assumptions

Tradeoffs

How to run

Sample credentials

Future improvements

---

# Git Strategy

Commit after every phase.

Example:

setup

security

admin APIs

booking

seat hold

payment

notification

tests

documentation

---

# Coding Rules

- Small classes
- Constructor injection
- No field injection
- No business logic in controllers
- Validate all requests
- Centralized exception handling
- Proper logging
- Never ignore edge cases

---

# IMPORTANT

Before generating code for any module:

1. Explain the design.
2. List assumptions.
3. Identify edge cases.
4. Generate code.
5. Generate tests.
6. Verify compilation.

Never skip these steps.

Always prioritize correctness over speed.
