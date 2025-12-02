# 📚 BookStore API

A RESTful API developed with Spring Boot to manage book loans in online or physical libraries. It allows operations with books, authors, clients, and orders. The project is domain-modularized and includes authentication with JWT, OAuth2 with Google, multiple layers (controller, service, repository, validation, DTO, model...) and documentation with Swagger.

---

## 🚀 Technologies Used
- Java 21
- Spring Boot
  - Spring Web
  - Spring Data JPA
  - Spring Security (JWT and OAuth2 with Google)
- PostgreSQL
- Docker
- Swagger (Springdoc OpenAPI)
- Lombok
- MapStruct

---

## 🏗️ Architecture

The API follows a **layered architecture**, with packages organized by type of responsibility. The domains (`book`, `author`, `client`, `order`) are distributed within these layers, which facilitates maintenance, scalability, and component reuse.

**Package structure:**

- `model` — Entity representations (books, authors, clients, orders)
- `dto` — Data transfer objects for input and output
- `mapper` — Mapping between entities and DTOs with MapStruct
- `controller` — HTTP request handling
- `service` — Centralized business logic
- `repository` — Database access with Spring Data JPA
- `validator` — Auxiliary validations and specific rules
- `security` — Authentication and authorization with JWT and OAuth2
- `exception` — Global error handling with `@ControllerAdvice`
- `config`, `docs`, `util`, `common` — General support and application configurations

This organization ensures each layer has a well-defined role, keeping the code clean, modular, and aligned with clean architecture principles.

---

## 🔐 Security

Authentication is done with JWT (JSON Web Token):

- Public endpoints:
  - `POST /auth/login`
  - `POST /client`
- All other endpoints require the JWT token in the header.

---

## 📌 Available Endpoints

- **Orders**
  - `POST /orders{id}/return` → return a borrowed book
  - `POST /orders` → create a new order
  - `GET /orders` → fetch all orders with filters
  - `GET /orders/{id}` → fetch order by ID
  - `PUT /orders/{id}` → update order by ID
  - `DELETE /orders/{id}` → delete order by ID

- **Authors**
  - `POST /authors` → create a new author
  - `GET /authors` → fetch all authors with filters
  - `GET /authors/{id}` → fetch author by ID
  - `PUT /authors/{id}` → update author by ID
  - `DELETE /authors/{id}` → delete author by ID

- **Books**
  - `POST /books` → create a new book
  - `GET /books` → fetch all books with filters
  - `GET /books/{id}` → fetch book by ID
  - `PUT /books/{id}` → update book by ID
  - `DELETE /books/{id}` → delete book by ID

- **Clients**
  - `POST /clients` → create a new client
  - `GET /client` → fetch all clients with filters
  - `GET /client/{id}` → fetch client by ID
  - `PUT /client/{id}` → update client by ID
  - `DELETE /client/{id}` → delete client by ID

Permissions are managed with `@PreAuthorize` and Spring Security filters.

---

## 🌐 OAuth2 Authentication with Google

The API allows login with Google accounts:

- Endpoint:
  - `/oauth2/authorization/google`
- After authentication, the JWT is automatically generated.
- Configuration via `application.yml`:

```yaml
client-id: ${CLIENT_ID}
client-secret: ${CLIENT_SECRET}
```

---

## 📌 API Documentation
Documentation available after starting the application:

👉 http://localhost:8081/swagger-ui/index.html#/

---

## 📁 Log
Logs are recorded in the `bookstore.log` file, as configured in `application.yml`.

---

## ▶️ How to Run

### ✅ Prerequisites
- Java 21  
- Maven  
- Docker (for PostgreSQL database)  
- Configured Google OAuth2 account  

---

### 📦 Start PostgreSQL with Docker (optional)
```bash
docker run --name postgres-bookstore -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres
```

###🧪 Configure application.yml
```
yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/bookstore
    username: postgres
    password: password
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: ${CLIENT_ID}
            client-secret: ${CLIENT_SECRET}
```

### 1. Clone the repository
git clone https://github.com/CaiquePirs/bookstore.git
2. Configure application.yml (see above)
3. Run the application
bash
```./mvnw spring-boot:run```

### 👨‍💻 Author
BookStore API was developed by Caique Pires. Contributions are welcome!
