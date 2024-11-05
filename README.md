# Unified Backend for Calculator Microservices

This repository contains the unified backend for a microservices system that provides user authentication, mathematical operations, and gateway routing for external requests. All components are integrated here to form a complete backend for the system.

## Overview

The unified backend consists of three main microservices:

1. **Authentication API**: Manages user authentication and user status.
2. **Operations API**: Performs mathematical operations and validates user balance.
3. **Gateway API**: Handles routing for requests, serving as the entry point for all external communications.

All requests to the system pass through the Gateway API, which determines the appropriate microservice to handle each request.

## Architecture

The architecture follows a microservices approach with centralized routing managed by the Gateway API, running on **port 8080**.

- **Gateway API (port 8080)**: Routes external requests to the appropriate microservice.
- **Authentication API (port 8081)**: Manages user login, registration, and status validation.
- **Operations API (port 8082)**: Handles mathematical operations (addition, subtraction, multiplication, division, square root, and more).

### Request Flow

1. **Authentication Requests**: User login and registration requests are routed to the Authentication API via the Gateway.
2. **Operations Requests**: Requests for mathematical operations are validated for user balance and then processed by the Operations API.
3. **Central Routing**: The Gateway API, on **port 8080**, serves as the single entry point for all external requests and directs them to the correct service.

## Technologies Used

- **Spring Boot**: Framework for creating REST APIs.
- **Spring Cloud Gateway**: For centralized routing and load balancing.
- **Maven**: Build automation and dependency management.
- **Docker**: For containerization.
- **MySQL**: Database for storing user and transaction data.

## Setup and Running Instructions

Follow these steps to set up and run the unified backend.

### Prerequisites

- **Java 17** or higher installed.
- **Maven** for building the project.
- **Docker** (optional) for containerized deployment.
- **MySQL** for database setup.

### Running Locally

1. **Clone the Repository**:
   ```bash
   git clone <repository_url>
   cd unified-backend
   ```

2. **Configure MySQL Database**:
   - Update database configuration in `application.properties` files for each microservice.

3. **Build the Project**:
   ```bash
   ./mvnw clean install
   ```

4. **Run Each Microservice**:
   - **Authentication API**:
     ```bash
     ./mvnw spring-boot:run -pl authentication
     ```
   - **Operations API**:
     ```bash
     ./mvnw spring-boot:run -pl operations
     ```
   - **Gateway API**:
     ```bash
     ./mvnw spring-boot:run -pl gateway
     ```

5. **Access the Application**:
   - The **Gateway API** runs on `http://localhost:8080`, and routes requests to the appropriate services.

### Running with Docker

1. **Build Docker Images**:
   ```bash
   docker-compose build
   ```

2. **Start All Services**:
   ```bash
   docker-compose up
   ```

3. **Access the Gateway**:
   - Visit `http://localhost:8080` to interact with the APIs.

## API Endpoints

### Authentication API

- **POST /api/auth/register**: Register a new user.
- **POST /api/auth/login**: Login and receive an authentication token.

### Operations API

- **POST /api/operations/add**: Perform addition.
- **POST /api/operations/subtract**: Perform subtraction.
- **POST /api/operations/multiply**: Perform multiplication.
- **POST /api/operations/divide**: Perform division.

## Error Handling

- Division by zero requests will return an error with appropriate status codes.
- Operations that require a balance greater than the user’s available funds will return an error indicating insufficient balance.

## Unit Tests

Unit tests are included for both backend services and API endpoints. Run the tests using:

```bash
./mvnw test
```



## License

This project is licensed under the MIT License. See the LICENSE file for more details.

## Contact

For questions or support, please contact [mdq767@gmail.com].

