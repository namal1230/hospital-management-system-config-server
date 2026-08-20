# Hospital Management System - Config Server

This repository contains the configuration server for the Hospital Management System. It centralizes configuration for microservices used in the hospital management platform and serves configuration properties (e.g., application.yml, secrets, and service-specific properties) to client services at runtime.

## Features

- Spring Cloud Config Server (recommended) to serve configuration from a Git backend or filesystem
- Centralized management of service configurations and profiles
- Secure endpoints for serving secrets and config (configure authentication as needed)

## Requirements

- Java 17+ (or Java 11 depending on the project setup)
- Maven or Gradle (depending on how the project is built)
- Git (if using a Git-backed config repository)

## Getting Started

1. Clone the repository:

   git clone https://github.com/namal1230/hospital-management-system-config-server.git
   cd hospital-management-system-config-server

2. Configure the backend (example for Spring Cloud Config Server using a local Git repo):

   In `application.yml` (or `bootstrap.yml`) set the `spring.cloud.config.server.git.uri` to the repository containing service configs.

   Example:

   spring:
     cloud:
       config:
         server:
           git:
             uri: https://github.com/your-org/hospital-management-configs
             default-label: main

3. Build and run

   Using Maven:

   mvn clean package
   java -jar target/config-server.jar

   Or using Gradle:

   ./gradlew bootRun

4. Accessing configuration

   With Spring Cloud Config Server running on http://localhost:8888, clients can fetch their configuration using URLs like:

   - http://localhost:8888/{application}/{profile}
   - http://localhost:8888/{application}/{profile}/{label}

   Example: http://localhost:8888/patient-service/default

## Security

- Protect the config server endpoints (actuator, /encrypt, /decrypt, and `/monitor`) using HTTP basic auth, OAuth2, or other authentication mechanisms.
- When storing secrets in the backend Git repository, consider using an encrypted store (e.g., Jasypt or the Spring Cloud Vault integration).

## Environment & Profiles

- Use Spring profiles (e.g., `dev`, `staging`, `prod`) to manage environment-specific properties.
- Keep sensitive values out of plain Git history; use encryption or a secret manager.

## Contributing

Contributions are welcome. Please open issues for bugs or feature requests, and submit pull requests with a clear description of changes.

## License

Specify your license here (e.g., MIT, Apache 2.0). If you don't have one yet, add a LICENSE file to the repository.

---

If you'd like, I can: 
- add example `application.yml`/`bootstrap.yml` for the config server,
- add CI workflow to build and publish the server,
- or create a sample `hospital-management-configs` repo structure with example service configs.
