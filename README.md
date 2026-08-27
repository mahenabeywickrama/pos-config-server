# Config-Server

Centralized external configuration server for the POS microservices ecosystem. It serves configuration properties to all registered services from a single source, enabling environment-specific settings without redeployment.

## About

This project is part of the Enterprise Cloud Architecture (ECA) module in the Higher Diploma in Software Engineering (HDSE) program at the Institute of Software Engineering (IJSE).

## Student & Submission Information

| Field | Details               |
| :--- |:----------------------|
| **Student Name** | Mahen Abeywickrama    |
| **Student Number** | 241711112             |
| **GCP Project ID** | `pos-project-506311`     |
| **GCP Region** | `asia-south2` (Delhi) |

## Project Description

Config-Server is the platform component responsible for centralized, externalized configuration for POS, a cloud-native Point-of-Sale system built on a microservice architecture. It allows every microservice — from inventory to sales to payments — to fetch environment-specific settings (datasource credentials, ports, feature flags) from one source, without requiring code changes or redeployment.

## Tech Stack

| Technology | Details |
|---|---|
| Java | 25 |
| Spring Boot | 4.1.0 |
| Spring Cloud | 2025.1.2 |
| Spring Cloud Config Server | Native filesystem backend |
| Spring Boot Actuator | Health & management endpoints |

## How It Works

The Config-Server uses a **native filesystem** backend, loading configuration files from the classpath. All microservices bootstrap by importing their configuration from this server before starting up.

### Configuration Layout

```
src/main/resources/configurations/
├── application.yaml           # Shared config for all services (Eureka URL, logging)
├── platform/
│   ├── api-gateway.yaml       # Api-Gateway routes & CORS config
│   └── service-registry.yaml  # Eureka server settings
└── services/
    ├── inventory-service.yaml # Inventory-Service datasource (PostgreSQL)
    ├── sales-service.yaml     # Sales-Service datasource (MongoDB)
    └── payment-service.yaml   # Payment-Service datasource (MySQL)
```

## Service Details

| Property | Value           |
|---|-----------------|
| Port | `9000`          |
| Artifact ID | `Config-Server` |
| Group ID | `com.pos`       |

## Setup / Getting Started

> **Important:** Config-Server must be started **first** before any other service, as all other services fetch their configuration from this server on startup.

```bash
./mvnw spring-boot:run
```

The server will be available at: `http://localhost:9000`

You can verify a service's configuration is being served correctly by visiting:

```
http://localhost:9000/{service-name}/default
```