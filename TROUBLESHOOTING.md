# Troubleshooting Guide - 500 Error on POST API

## Problem
Tests are failing with: `POST API should return status code 201 expected [201] but found [500]`

## Root Cause
A 500 Internal Server Error means the Spring Boot application encountered an error while processing the request. The most common causes are:

### 1. MySQL Database Not Running ⚠️
**Most Likely Issue:** MySQL server is not running or not accessible.

**Solution:**
- Start MySQL server on your machine
- Windows: Start MySQL service from Services or run `net start MySQL80`
- Verify MySQL is running on port 3306

### 2. Database Connection Issues
**Check application.properties:**
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/demodb?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=root
```

**Verify:**
- MySQL username is `root`
- MySQL password is `root`
- Update credentials if different

### 3. Spring Boot Application Not Running
**The application must be running BEFORE executing tests!**

**Start the application:**
```bash
mvn spring-boot:run
```

Wait for this message in console:
```
Started DemoApplication in X.XXX seconds
```

### 4. Port Already in Use
If port 9001 is already in use, you'll see errors in Spring Boot logs.

**Solution:**
- Check what's using port 9001
- Change port in `application.properties`:
  ```properties
  server.port=9002
  ```
- Update `UserApiTest.java` to match the new port

## Step-by-Step Fix

### Step 1: Start MySQL Server
```bash
# Windows
net start MySQL80

# Or start MySQL from MySQL Workbench or XAMPP
```

### Step 2: Verify MySQL Connection
```bash
mysql -u root -p
# Enter password: root
```

If successful, you should see MySQL prompt:
```
mysql>
```

### Step 3: Start Spring Boot Application
**In a separate terminal:**
```bash
cd C:\Users\arunt\OneDrive\Documents\spring_portal\FullProjects\DemoProject
mvn spring-boot:run
```

**Watch for errors in the console!** If you see database connection errors, fix them before proceeding.

### Step 4: Wait for Application to Start
Look for this log message:
```
Started DemoApplication in X.XXX seconds (process running for X.XXX)
```

### Step 5: Test Manually First
**Before running TestNG tests, verify APIs work:**

```bash
# Test GET endpoint
curl http://localhost:9001/api/users

# Test POST endpoint
curl -X POST http://localhost:9001/api/users ^
  -H "Content-Type: application/json" ^
  -d "{\"name\":\"Test User\",\"email\":\"test@example.com\"}"
```

### Step 6: Run TestNG Tests
**In a NEW terminal** (while Spring Boot is still running):
```bash
mvn test
```

## Common Error Messages and Solutions

### Error: "Communications link failure"
```
Caused by: com.mysql.cj.jdbc.exceptions.CommunicationsException: Communications link failure
```
**Solution:** MySQL server is not running. Start MySQL.

### Error: "Access denied for user 'root'@'localhost'"
```
java.sql.SQLException: Access denied for user 'root'@'localhost' (using password: YES)
```
**Solution:** Wrong MySQL password. Update `application.properties` with correct credentials.

### Error: "Unable to obtain connection from database"
```
HikariPool-1 - Exception during pool initialization
```
**Solution:** MySQL not accessible. Check MySQL is running and credentials are correct.

### Error: "Port 9001 is already in use"
```
Web server failed to start. Port 9001 was already in use.
```
**Solution:** Change port in `application.properties` or stop process using port 9001.

## Verification Checklist

Before running tests, verify:

- [ ] MySQL server is running
- [ ] MySQL credentials in `application.properties` are correct
- [ ] Spring Boot application is running (mvn spring-boot:run)
- [ ] Application started successfully (check console for "Started DemoApplication")
- [ ] Port 9001 is accessible
- [ ] Swagger UI loads: http://localhost:9001/swagger-ui/index.html
- [ ] GET API works manually: http://localhost:9001/api/users

## Quick Test Commands

### Check if MySQL is running:
```bash
# Windows
sc query MySQL80
# Should show STATE: RUNNING

# Test connection
mysql -u root -proot -e "SELECT 1"
```

### Check if Spring Boot is running:
```bash
# Windows PowerShell
Test-NetConnection -ComputerName localhost -Port 9001

# Or use curl
curl http://localhost:9001/api/users
```

### Check application logs:
Look in the Spring Boot console for stack traces or error messages that explain the 500 error.

## Still Having Issues?

1. **Check Spring Boot Console Logs** - The actual error will be printed there
2. **Enable Debug Logging** - Add to `application.properties`:
   ```properties
   logging.level.org.springframework=DEBUG
   logging.level.com.example.demo=DEBUG
   ```
3. **Test with Swagger UI** - Use http://localhost:9001/swagger-ui/index.html to test APIs interactively
4. **Check MySQL Logs** - Look for connection attempts and errors

## Expected Test Flow

```
1. Start MySQL ✓
2. Start Spring Boot Application ✓
3. Application connects to MySQL ✓
4. Tables are created automatically ✓
5. Run TestNG tests ✓
6. Tests hit the running application ✓
7. All tests pass ✓
```

**Remember:** Tests don't start the application - they test an already-running application!

