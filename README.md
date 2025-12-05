# Demo Spring Boot Project

A simple Spring Boot application with MySQL connectivity, REST APIs, and TestNG test cases.

## Project Structure
```
DemoProject/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── example/
│   │   │           └── demo/
│   │   │               ├── DemoApplication.java
│   │   │               ├── controller/
│   │   │               │   └── UserController.java
│   │   │               ├── entity/
│   │   │               │   └── User.java
│   │   │               ├── repository/
│   │   │               │   └── UserRepository.java
│   │   │               └── service/
│   │   │                   └── UserService.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/
│           └── com/
│               └── example/
│                   └── demo/
│                       └── UserApiTest.java
└── pom.xml
```

## Features

- **Spring Boot 3.1.5** with Java 17
- **MySQL Database** connectivity
- **REST APIs**:
  - `POST /api/users` - Create a new user
  - `GET /api/users` - Get all users
- **Swagger/OpenAPI 3** - Interactive API documentation and testing
- **TestNG Test Cases** - 5 test cases for API validation

## Prerequisites

1. Java 17 or higher
2. Maven 3.6 or higher
3. MySQL 8.0 or higher

## Database Setup

1. Install and start MySQL server
2. Create a database named `demodb`:
   ```sql
   CREATE DATABASE demodb;
   ```
3. Update credentials in `src/main/resources/application.properties` if needed:
   ```properties
   spring.datasource.username=root
   spring.datasource.password=root
   ```

## Running the Application

1. Build the project:
   ```bash
   mvn clean install
   ```

2. Run the application:
   ```bash
   mvn spring-boot:run
   ```

The application will start on `http://localhost:9001`

## Swagger API Documentation

Once the application is running, you can access the Swagger UI for interactive API testing:

**Swagger UI:** `http://localhost:9001/swagger-ui/index.html`

**OpenAPI JSON:** `http://localhost:9001/v3/api-docs`

Swagger provides:
- Interactive API testing interface
- Complete API documentation
- Request/response examples
- Schema definitions
- Try-it-out functionality for all endpoints

## API Endpoints

### 1. Create User (POST)
**Endpoint:** `POST /api/users`

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

**Response:** Status Code `201 CREATED`
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

### 2. Get All Users (GET)
**Endpoint:** `GET /api/users`

**Response:** Status Code `200 OK`
```json
[
  {
    "id": 1,
    "name": "John Doe",
    "email": "john.doe@example.com"
  }
]
```

## Running Tests

The project includes 5 TestNG test cases that validate:
1. GET API endpoint name and status code (200)
2. POST API endpoint name and status code (201)
3. GET API returns valid JSON response
4. POST API with valid data creates user
5. GET API verification after creating users

### Run Tests:
```bash
mvn test
```

**Note:** Make sure the application is running before executing the tests.

## Test Cases Overview

| Test Case | Description | Expected Status Code |
|-----------|-------------|---------------------|
| testGetAllUsersEndpoint | Validates GET API endpoint and status | 200 OK |
| testCreateUserEndpoint | Validates POST API endpoint and status | 201 CREATED |
| testGetAllUsersReturnsJson | Validates GET API returns JSON | 200 OK |
| testPostApiWithValidData | Validates POST API creates user | 201 CREATED |
| testGetAllUsersAfterCreation | Validates GET API after user creation | 200 OK |

## Technologies Used

- Spring Boot 3.1.5
- Spring Data JPA
- MySQL Connector
- Swagger/OpenAPI 3 (SpringDoc 2.2.0)
- TestNG 7.8.0
- Rest Assured 5.3.2
- Maven

## Author

Demo Project for Spring Boot MySQL Integration

