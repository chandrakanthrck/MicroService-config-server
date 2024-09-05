# Microservice Config Server

## Overview
This project is a **Spring Cloud Config Server** that serves as a centralized configuration management system for a microservices-based architecture. It allows microservices to fetch their configuration properties from a remote repository, enabling easier management and version control of configuration files across multiple environments (development, testing, production, etc.).

## Features
- Centralized configuration management for all microservices
- Integration with **Spring Boot** applications
- Fetch configurations from **Git** repositories or other supported storage backends
- Environment-specific configuration files (e.g., `application-dev.yml`, `application-prod.yml`)
- Dynamic reloading of properties with Spring Cloud's `@RefreshScope`

## Technologies Used
- **Java 17**
- **Spring Boot 3.x**
- **Spring Cloud Config Server**
- **Git** (as the configuration source)

## Project Setup

### Prerequisites
- Java 17 or higher
- Maven 3.6+
- A remote Git repository (or local) to store configuration files

### Clone the Repository
```bash
git clone https://github.com/your-username/microservice-config-server.git
cd microservice-config-server

## Configure the Application

### Remote Git Configuration Source:
Update the configuration repository path in `src/main/resources/application.yml`:

```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-username/microservice-config-repo
          default-label: main

## Example Config Fetch URL

Microservices can fetch configurations for a specific profile and label using the following URL pattern:

```bash
http://localhost:8888/{application}/{profile}/{label}
```

### Example:

```bash
http://localhost:8888/hotelservice/dev/main
