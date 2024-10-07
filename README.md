
# Placement Service Application

This is a Spring Boot application that provides a RESTful API for managing placement information.  It uses PostgreSQL as the database and can be integrated with a frontend framework like AngularJS.


## Features

* **CRUD Operations:** Create, Read, Update, and Delete placement records.
* **RESTful API:**  Easy to integrate with frontend applications.
* **PostgreSQL Database:** Stores placement data persistently.
* **Spring Boot:**  Provides a robust and easy-to-use framework.


## Prerequisites

* Java 21
* Maven
* PostgreSQL (installed and running)
* Postman (for API testing)


## Getting Started

1. **Clone the repository:**

   ```bash
   git clone <repository_url>
   ```

2. **Configure Database:**
   - Create a PostgreSQL database (e.g., `placementdb`).
   - Create a user with appropriate permissions (e.g., `your_username` with password `your_password`).  Make sure the user has permissions to create tables, either by granting permissions on the `public` schema or by creating the `placement` table manually.  See the "Database Permissions" section below for details.
   - Update the `src/main/resources/application.properties` file with your database credentials:

     ```properties
     spring.datasource.url=jdbc:postgresql://localhost:5432/your_database_name
     spring.datasource.username=your_username
     spring.datasource.password=your_password
     spring.datasource.driver-class-name=org.postgresql.Driver
     spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
     server.port=8080  # Or any other available port
     spring.jpa.hibernate.ddl-auto=update  
     ```

3. **Build and Run:**
   - Open the project in your IDE (like Eclipse or IntelliJ IDEA).
   - Build the project using Maven:

     ```bash
     mvn clean install
     ```

   - Run the application as a Spring Boot app.

4. **Test with Postman:**
   - Open Postman.
   - Create new requests to test the API endpoints (e.g., `GET http://localhost:8080/placement`).  Refer to the examples in the "API Endpoints" section.


## Database Permissions

The PostgreSQL user you specify in `application.properties` must have the necessary privileges to create tables in the database schema you are using (usually `public`). You can grant these permissions using the following SQL commands (replace placeholders with your actual values):

```sql
-- Grant all privileges on the public schema (less secure, but convenient):
GRANT ALL ON SCHEMA public TO your_username;


-- Grant only the necessary create and usage permissions for the public schema:
GRANT CREATE ON SCHEMA public TO your_username;
GRANT USAGE ON SCHEMA public TO your_username;

-- Grant privileges for a specific schema (if not using public):
GRANT ALL ON SCHEMA your_schema_name TO your_username;


--or
CREATE TABLE placement (
       id BIGSERIAL PRIMARY KEY,          -- Use BIGSERIAL for auto-incrementing ID
       company_name VARCHAR(255),
       drive_date VARCHAR(255),
       location VARCHAR(255),
       position VARCHAR(255),
       salary_package VARCHAR(255)
   );
```

## API Endpoints

| Method | URL                       | Description                        |
| ------ | -------------------------- | ---------------------------------- |
| GET    | `/placement`               | Get all placements                 |
| GET    | `/placement/{id}`          | Get placement by ID               |
| POST   | `/placement`               | Create a new placement            |
| PUT    | `/placement/{id}`          | Update an existing placement       |
| DELETE | `/placement/{id}`          | Delete a placement                 |


## Example Postman Requests


**GET (all placements):**

* URL: `http://localhost:8080/placement`
* Method: `GET`

**POST (create placement):**

* URL: `http://localhost:8080/placement`
* Method: `POST`
* Headers: `Content-Type: application/json`
* Body (JSON):
  ```json
  {
    "companyName": "Example Corp",
    "position": "Java Developer",
    "location": "Bangalore",
    "salaryPackage": "800000",
    "driveDate": "2024-12-20"
  }
  ```

(And so on for PUT and DELETE, remembering to use the correct `id`.)




 Remember to replace the placeholder values with your actual database and user credentials.

