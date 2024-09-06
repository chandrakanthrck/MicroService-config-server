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
git clone git@github.com:chandrakanthrck/MicroService-config-server.git
cd microservice-config-server
```
## Configure the Application

### Remote Git Configuration Source:
Update the configuration repository path in `src/main/resources/application.yml`:

```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: git@github.com:chandrakanthrck/MicroService-config-server.git
          default-label: main
```
### Usage of Configuration Repository
The configuration files for different environments (e.g., `application-dev.yml`, `application-prod.yml`) are stored in a separate repository, which is specified in the **Config Server's** configuration.

- **Configuration Repository**: [Config Repo](https://github.com/chandrakanthrck/env-config)
- This repository holds environment-specific configuration files for all microservices, such as:
  - `application.yml` (default config)
  - `application-dev.yml` (development environment)
  - `application-prod.yml` (production environment)

### How It Works
- When the **Config Server** starts, it fetches the configuration files from the linked repository.
- Microservices retrieve their environment-specific configurations dynamically from the **Config Server** based on the active profile.

## Example Config Fetch URL

Microservices can fetch configurations for a specific profile and label using the following URL pattern:

```bash
http://localhost:8888/{application}/{profile}/{label}
```

### Example:

```bash
http://localhost:8888/hotelservice/dev/main
```
- **{application}**: The name of the microservice (e.g., `hotelservice`).
- **{profile}**: The active profile (e.g., `dev`, `prod`).
- **{label}**: The Git branch or tag (default is `main`).

### Dynamic Refresh of Configuration
Use Spring Cloud’s `@RefreshScope` in your microservices to enable dynamic refresh of properties without restarting the services.
```bash
POST /actuator/refresh
```
This allows the microservices to reload properties dynamically without needing to restart.

### Important Notes
- Ensure sensitive data like passwords, API keys, etc., are not exposed in these configuration files. Consider using **encrypted values** or **environment variables** for sensitive information.
- This repository works in conjunction with the **Spring Cloud Config Server** to provide environment-specific configurations to microservices.

### License
This project is licensed under the MIT License.

### Changes made:
1. **Added usage of the `config-repo` repository**: Mentioned how the repository is linked and how it stores environment-specific files.
2. **Link to the config repo**: Provided a link to the **configuration repository** for reference.
3. **How it works**: Explained how the Config Server fetches the files and how microservices consume them.

This should now provide a clear explanation of how the **config-env repo** is used in this setup. Let me know if this fits or if you need more details!
