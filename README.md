# Enterprise Java Lab: Student Management System (Experiments 1–9)

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-17%2B-orange.svg)](https://www.oracle.com/java/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue.svg)](https://www.mysql.com/)
[![License](https://img.shields.io/badge/License-Academic-lightgrey.svg)]()

A comprehensive Enterprise Java laboratory project tracking the progressive development of a production-grade RESTful API. The system handles student and course lifecycles using **Spring Boot**, **Spring Data JPA**, **Hibernate ORM**, **MySQL**, **Bean Validation**, **MockMvc Automated Testing**, and **Spring Security**.

---

## 📑 Table of Contents
- [Course Experiments Overview](#-course-experiments-overview)
- [Key Concepts & Learning Outcomes](#-key-concepts--learning-outcomes)
- [System Architecture & Database Design](#-system-architecture--database-design)
- [Detailed Experiment Implementation Steps (1 to 9)](#-detailed-experiment-implementation-steps-1-to-9)
  - [Experiment 1: Project Initialization & Spring Boot Setup](#experiment-1-project-initialization--spring-boot-setup)
  - [Experiment 2: Building First REST Endpoints](#experiment-2-building-first-rest-endpoints)
  - [Experiment 3: Database Integration with MySQL & Spring Data JPA](#experiment-3-database-integration-with-mysql--spring-data-jpa)
  - [Experiment 4: Full CRUD Operations via REST APIs](#experiment-4-full-crud-operations-via-rest-apis)
  - [Experiment 5: Derived Queries, Pagination & Sorting](#experiment-5-derived-queries-pagination--sorting)
  - [Experiment 6: One-to-Many Relational Mapping (Student–Course)](#experiment-6-one-to-many-relational-mapping-studentcourse)
  - [Experiment 7: Input Validation & Centralized Exception Handling](#experiment-7-input-validation--centralized-exception-handling)
  - [Experiment 8: Automated Testing with MockMvc & cURL CLI](#experiment-8-automated-testing-with-mockmvc--curl-cli)
  - [Experiment 9: Basic Authentication with Spring Security](#experiment-9-basic-authentication-with-spring-security)
- [API Reference & Testing Guide](#-api-reference--testing-guide)
- [Prerequisites & Execution Instructions](#-prerequisites--execution-instructions)

---

## 🔬 Course Experiments Overview

| Exp # | Focus Area | Core Technologies / Annotations |
|:---:|:---|:---|
| **1** | Project Bootstrapping | Spring Initializr, Maven, `@SpringBootApplication` |
| **2** | REST Controllers | `@RestController`, `@GetMapping`, JSON serialization |
| **3** | Persistence & ORM | `@Entity`, `@Id`, `JpaRepository`, MySQL driver |
| **4** | CRUD Operations | `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `ResponseEntity` |
| **5** | Derived Queries, Page & Sort | `findByName`, `Pageable`, `Page<T>`, `Sort` |
| **6** | Entity Relationships | `@OneToMany`, `@ManyToOne`, `@JsonManagedReference`, `@JsonBackReference` |
| **7** | Validation & Error Handling | `@Valid`, `@NotBlank`, `@Email`, `@RestControllerAdvice` |
| **8** | Automated & CLI Testing | JUnit 5, `MockMvc`, cURL HTTP status code assertions |
| **9** | Security & Authentication | Spring Security, HTTP Basic, `SecurityFilterChain`, CSRF |

---

## 🎯 Key Concepts & Learning Outcomes

By progressing through Experiments 1 through 9, the following skills were developed:
1. **Architectural Separation:** Structuring software into Models, Repositories, Services, and REST Controllers.
2. **Declarative Persistence:** Leveraging Spring Data JPA to eliminate repetitive boilerplate SQL.
3. **Database Performance:** Implementing pagination and sorting directly at the database layer.
4. **Relational Integrity:** Managing foreign keys, cascading entity lifecycles, and preventing circular JSON recursion.
5. **Defensive API Engineering:** Validating request payloads before database transmission and delivering client-friendly HTTP 400 error bodies.
6. **Integration Testing:** Simulating web client calls with `MockMvc` without starting an external web container.
7. **Access Control:** Intercepting unauthorized requests and securing resources via Basic Authentication.

---

## 🏛 System Architecture & Database Design

### Relational Schema:
```text
  ┌─────────────────────────────────┐           ┌─────────────────────────────────┐
  │            students             │           │             courses             │
  ├─────────────────────────────────┤           ├─────────────────────────────────┤
  │ id          INT (PK, AUTO_INC)  │1         *│ id          INT (PK, AUTO_INC)  │
  │ name        VARCHAR(255) NOT NULL           │ course_name VARCHAR(255)        │
  │ email       VARCHAR(255) NOT NULL           │ credits     INT                 │
  └─────────────────────────────────┘           │ student_id  INT (FK -> students)│
                                                └─────────────────────────────────┘
