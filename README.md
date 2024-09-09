# Expense Management System (Microservices Architecture)

This project demonstrates a microservices-based architecture for an **Expense Management System** using **Spring Boot**. The system is composed of multiple services that handle different functionalities such as user management, expense tracking, category management, and report generation. Each service is developed independently and communicates via REST APIs. The project utilizes Eureka Server for service discovery and API Gateway for routing.

## Project Structure
Expense-Management-System/
├── api-gateway/
│   ├── src/
│   └── pom.xml
├── category-service/
│   ├── src/
│   └── pom.xml
├── eureka-server/
│   ├── src/
│   └── pom.xml
├── expense-service/
│   ├── src/
│   └── pom.xml
├── report-service/
│   ├── src/
│   └── pom.xml
└── user-service/
    ├── src/
    └── pom.xml
Services Overview
1.Eureka Server
The Eureka Server acts as the service registry where all other microservices register themselves. This enables service discovery and load balancing.

Dependencies:
*Spring Boot DevTools
*Eureka Server
Key Configuration: application.yml
server:
  port: 8761      
eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
  server:
    enable-self-preservation: false
2.API Gateway
The API Gateway serves as the entry point for all client requests and routes them to the appropriate services. It also handles cross-cutting concerns like authentication, authorization, and load balancing.

Dependencies:
Spring Cloud Gateway
Eureka Client
Key Configuration: application.yml
server:
  port: 8080
spring:
  cloud:
    gateway:
      routes:
        - id: user-service
          uri: lb://USER-SERVICE
          predicates:
            - Path=/users/**
eureka:
3.client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
      User Service
The User Service manages user-related functionalities such as user registration, login, and profile management.

Dependencies:
Spring Web
Spring Data JPA
MySQL Driver
Lombok
Eureka Client
Key Configuration: application.yml
yaml
Copy code
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/user_db
    username: root
    password: root_password
  jpa:
    hibernate:
      ddl-auto: update
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
4.Expense Service
The Expense Service handles expense tracking and management for each user.

Dependencies:
Spring Web
Spring Data JPA
MySQL Driver
Lombok
Eureka Client
Key Configuration: Similar to the User Service.
Category Service
The Category Service manages categories for organizing user expenses.

Dependencies:
Spring Web
Spring Data JPA
MySQL Driver
Lombok
Eureka Client
Key Configuration: Similar to the User Service.
Report Service
The Report Service generates reports based on the user's expenses across different categories.

Dependencies:
Spring Web
Spring Data JPA
MySQL Driver
Lombok
Eureka Client
Key Configuration: Similar to the User Service.
Steps to Run the Project
Clone the Repository:

bash
Copy code
git clone https://github.com/yourusername/Expense-Management-System.git
cd Expense-Management-System
Run the Eureka Server:

Navigate to the eureka-server folder:
bash
Copy code
cd eureka-server
mvn spring-boot:run
Run the API Gateway:

Navigate to the api-gateway folder:
bash
Copy code
cd ../api-gateway
mvn spring-boot:run
Run Other Microservices: Repeat the steps for running each service (user-service, expense-service, category-service, report-service). For example:

bash
Copy code
cd ../user-service
mvn spring-boot:run
Access the Services:

Eureka Server: http://localhost:8761
API Gateway: http://localhost:8080
User Service: Access through Gateway http://localhost:8080/users
Technologies Used
Spring Boot
Spring Cloud Eureka (for service discovery)
Spring Cloud Gateway (for API Gateway)
Spring Data JPA (for database operations)
MySQL (for persistent storage)
Lombok (to reduce boilerplate code)
Maven (for dependency management)
Folder Structure Explained
Each microservice is contained within its own directory (eureka-server, api-gateway, user-service, etc.).
Every service has its own pom.xml to manage dependencies.
Source code for each microservice is stored under the src/main/java directory, with configuration files like application.yml stored under src/main/resources.
Contributing
To contribute:

Fork the repository.
Create a new branch (git checkout -b feature/new-feature).
Make your changes.
Push to the branch (git push origin feature/new-feature).
Open a pull request.
