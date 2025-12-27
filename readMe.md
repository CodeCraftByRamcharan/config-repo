Spring Cloud Config Learning Project

This is a learning setup for Spring Cloud Config, including:

Config Repository (Git-based)
Config Server (Spring Boot)
Order Service (Spring Boot microservice consuming config)

Runtime refresh using @RefreshScope with /actuator/refresh and /actuator/busrefresh

⚠️ For learning purposes only. Do not store sensitive credentials in Git in real projects.
⚠️ Note: For learning purposes only, I have included config-server and order-service inside the same config-repo. In a real-world scenario, each microservice and the config server would have its own separate Git repository.

1. Project Structure
config-repo/ → Stores YAML config files for all services and environments
config-server/ → Spring Boot project for Config Server
order-service/ → Spring Boot microservice consuming config

2. Config Repository
Create a Git repository for configuration.
Add files for each service (e.g., order-service.yml) and optionally environment-specific files (e.g., order-service-dev.yml, order-service-prod.yml).
Add a shared config file for all services (optional).

3. Config Server Setup
Create Spring Boot project for Config Server.
Add Spring Web, Config Server, and optionally Actuator dependencies.
Enable Config Server in the main application class.
Configure Git repository URL in the Config Server.
Run Config Server locally and verify configurations are served.

4. Order Service Setup
Create Spring Boot project for Order Service.
Add Spring Web, Config Client, and Actuator dependencies.
Configure Order Service to read from Config Server.
Start Config Server first, then start Order Service.
Verify that service reads configuration from Config Server.

5. Using Profiles
Create environment-specific config files (dev, prod, etc.) in the config repository.
Activate a profile in Order Service to use the corresponding configuration file.
Verify that the correct environment config is loaded.

6. @RefreshScope + /actuator/refresh
Add Actuator dependency to Order Service.
Expose /refresh endpoint.
Annotate beans that need runtime refresh with @RefreshScope.
Start applications and verify initial values.
Change config in GitHub without restarting the service.
Trigger refresh by calling /actuator/refresh.
Verify updated values are applied at runtime.

7. Spring Cloud Bus + /actuator/busrefresh

Add Spring Cloud Bus dependency (RabbitMQ or Kafka) to Order Service.
Configure the message broker (RabbitMQ or Kafka).
Expose /busrefresh endpoint.
Start multiple instances of Order Service.
Change config in GitHub.
Trigger bus refresh on one instance.
Verify that all instances are refreshed automatically.

