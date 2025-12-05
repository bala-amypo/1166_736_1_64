# Swagger API Documentation Guide

## Overview

This project uses **Swagger/OpenAPI 3** (via SpringDoc) for interactive API documentation and testing.

## Accessing Swagger UI

### 1. Start the Application

```bash
mvn spring-boot:run
```

### 2. Open Swagger UI

Once the application is running, navigate to:

**Swagger UI:** http://localhost:9001/swagger-ui/index.html

**OpenAPI Docs (JSON):** http://localhost:9001/v3/api-docs

## Using Swagger UI for API Testing

### Features Available:

1. **Interactive API Explorer**
   - View all available endpoints
   - See request/response schemas
   - Try out APIs directly from the browser

2. **Automatic Documentation**
   - API descriptions
   - Parameter details
   - Response codes and examples
   - Data models/schemas

### How to Test APIs Using Swagger UI:

#### Test GET API (Get All Users):

1. Navigate to **User Management** section
2. Click on **GET /api/users**
3. Click **"Try it out"** button
4. Click **"Execute"** button
5. View the response (Status Code: 200)

#### Test POST API (Create User):

1. Navigate to **User Management** section
2. Click on **POST /api/users**
3. Click **"Try it out"** button
4. Modify the request body:
   ```json
   {
     "name": "John Doe",
     "email": "john.doe@example.com"
   }
   ```
5. Click **"Execute"** button
6. View the response (Status Code: 201)

## API Endpoints Documentation

### User Management APIs

| Method | Endpoint | Description | Status Code |
|--------|----------|-------------|-------------|
| GET | `/api/users` | Get all users | 200 OK |
| POST | `/api/users` | Create a new user | 201 CREATED |

### Request/Response Examples

#### POST /api/users - Create User

**Request Body:**
```json
{
  "name": "Jane Smith",
  "email": "jane.smith@example.com"
}
```

**Response (201 CREATED):**
```json
{
  "id": 1,
  "name": "Jane Smith",
  "email": "jane.smith@example.com"
}
```

#### GET /api/users - Get All Users

**Response (200 OK):**
```json
[
  {
    "id": 1,
    "name": "Jane Smith",
    "email": "jane.smith@example.com"
  },
  {
    "id": 2,
    "name": "John Doe",
    "email": "john.doe@example.com"
  }
]
```

## Swagger Configuration

Swagger is **auto-configured** by SpringDoc! No additional configuration file is needed.

SpringDoc automatically:
- Scans your controllers and generates documentation
- Creates the Swagger UI interface
- Provides OpenAPI JSON specification
- Uses default settings (customizable if needed via application.properties)

## Swagger Annotations Used

### Controller Level:
- `@Tag` - Groups related APIs together
- `@Operation` - Describes what an endpoint does
- `@ApiResponses` - Documents possible responses

### Entity Level:
- `@Schema` - Documents model properties
- Includes field descriptions, examples, and requirements

## Benefits of Using Swagger

✅ **Interactive Testing** - Test APIs without external tools like Postman  
✅ **Automatic Documentation** - Always up-to-date with code  
✅ **Clear API Contracts** - See exactly what data is expected  
✅ **Easy Onboarding** - New developers can understand APIs quickly  
✅ **Client Code Generation** - Generate API clients automatically  

## Comparison: Swagger vs TestNG

### Swagger (Interactive UI Testing)
- **Purpose:** Manual API exploration and documentation
- **Use Case:** Development, debugging, and demonstration
- **Execution:** Browser-based, interactive
- **Best For:** Quick testing and API exploration

### TestNG (Automated Testing)
- **Purpose:** Automated regression testing
- **Use Case:** CI/CD pipelines, quality assurance
- **Execution:** Automated, command-line
- **Best For:** Continuous testing and validation

## Tips for Using Swagger

1. **Try Before You Code** - Use Swagger to understand API behavior
2. **Share with Team** - Send Swagger URL to team members
3. **API Documentation** - Use as living documentation
4. **Client Development** - Frontend developers can use it as reference
5. **Quick Debugging** - Test endpoints without writing code

## Troubleshooting

### Swagger UI Not Loading?

1. Ensure application is running on port 9001
2. Check console for any startup errors
3. Verify `springdoc-openapi-starter-webmvc-ui` dependency in pom.xml

### 404 Error on Swagger UI?

Make sure you're using the correct URL:
- ✅ Correct: http://localhost:9001/swagger-ui/index.html
- ❌ Incorrect: http://localhost:9001/swagger-ui.html

## Additional Resources

- [SpringDoc Documentation](https://springdoc.org/)
- [OpenAPI Specification](https://swagger.io/specification/)
- [Swagger UI Guide](https://swagger.io/tools/swagger-ui/)

