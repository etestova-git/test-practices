# API Testing Best Practices

---

## 🔍 What is an API?

**API** stands for **Application Programming Interface**.  
It is a set of rules that allows one software application to interact with another.

- Think of it as a **messenger** that takes a request, tells a system what you want, and returns the response.
- Example: When you use a weather app, it calls a weather API to fetch temperature data.

---

## ⚙️ How Does an API Work?

1. **Request:** A client (like a mobile app) sends a request to a server via an API endpoint  
   Example: `GET /api/users/123`

2. **Processing:** The server processes the request (e.g., queries the database)

3. **Response:** The server returns the data in a structured format (JSON for REST, XML for SOAP)

```json
{
  "id": 123,
  "name": "Alice",
  "email": "alice@example.com"
}
```

**Common HTTP Methods**

- **GET**	- Retrieve data
- **POST** - Submit new data
- **PUT**	- Update existing data
- **DELETE** - Remove data

**What is API Mocking?**
- API Mocking means simulating the behavior of an actual API before it is implemented or available.

**Benefits of API Mocking**
- Frontend and backend teams can work independently
- Enables early testing and development
- Allows simulating edge cases and errors

**How to Mock an API in Postman**


---

## 🔍 POISED Principle for API Testing

---

### ✅ Summary Table

| Letter | Aspect          | Key Focus                                      |
|--------|------------------|------------------------------------------------|
| P      | Performance       | Response time, latency, load handling         |
| O      | Output            | Data correctness, schema, formatting          |
| I      | Interoperability  | Cross-platform support, standards compliance  |
| S      | Security          | Auth, encryption, secure communication        |
| E      | Error Handling    | HTTP codes, error clarity                     |
| D      | Data Integrity    | CRUD validity, consistency, sync              |


---

### 🅿️ P — Performance

- **What to Check:**
  - Response time under normal and high load
  - Latency and throughput
  - Scalability and resource usage

---

### 🅾️ O — Output

- **What to Check:**
  - Accuracy and correctness of response data
  - Schema and data format (e.g., JSON, XML)
  - Content completeness and field validation

---

### 🇮 I — Interoperability

- **What to Check:**
  - Cross-platform compatibility (web, mobile, 3rd party)
  - Standard compliance (RESTful conventions, MIME types)

---

### 🇸 S — Security

- **What to Check:**
  - Authentication (API key, OAuth)
  - Authorization (user roles, permissions)
  - HTTPS usage and data encryption
  - Input validation to prevent injection attacks

---

### 🇪 E — Error Handling

- **What to Check:**
  - Proper use of status codes (e.g., 400, 403, 500)
  - Clear and helpful error messages
  - Graceful degradation and fallback logic

---

### 🇩 D — Data Integrity

- **What to Check:**
  - Correct execution of CRUD operations
  - Data consistency across endpoints
  - Validations on data creation and updates

---

# 🔍 API Testing Plan: GET /api/users/{userId}

This document outlines a comprehensive testing strategy for the `GET /api/users/{userId}` endpoint using **Postman**, covering:

- ✅ Happy Path
- ❌ Negative Testing
- 🔐 Security Testing
- ⚡ Performance Checks

---

## ✅ 1. Happy Path (Successful Retrieval)

**🛠 Action:**  
Send a `GET /api/users/{userId}` request using a valid, existing `userId`.

**✅ Verification:**

- **Status Code:**  
  `200 OK`

- **Response Body - Data Accuracy:**  
  Ensure that:
  - `id` matches the requested `userId`
  - Fields like `email`, `firstName`, `createdAt` match the expected user data from DB

- **Response Body - Schema Validation:**  
  Validate JSON structure:
  ```json
  {
    "id": 123,
    "firstName": "John",
    "email": "john@example.com",
    "createdAt": "2024-01-01T12:00:00Z",
    "isActive": true
  }
  ```
  Use Postman's scripting to check:
  - Required fields exist
  - Data types are correct

- **Headers:**  
  Ensure:
  - `Content-Type: application/json`

---

## ❌ 2. Negative Testing (Expected Errors)

### 🔎 Case 1: Non-existent User

**🛠 Action:**  
`GET /api/users/999999` (user doesn't exist)

**✅ Verification:**
- **Status Code:** `404 Not Found`
- **Response Body:**  
  ```json
  {
    "error": "User not found"
  }
  ```

---

### 🔎 Case 2: Invalid Input Format

**🛠 Action:**  
`GET /api/users/abc` (non-numeric userId)

**✅ Verification:**
- **Status Code:** `400 Bad Request`
- **Response Body:**  
  Well-formed error message indicating invalid input format

---

## 🔐 3. Security Testing (Auth & Permissions)

### 🧾 Authentication Missing or Invalid

**🛠 Action:**  
Send the request without a token or with an invalid token

**✅ Verification:**
- **Status Code:** `401 Unauthorized`
- **Response Body:**  
  ```json
  {
    "error": "Authentication token missing or invalid"
  }
  ```

---

### 🔒 Authorization Violation

**🛠 Action:**  
Authenticated as User A (`ID: 123`), try to access User B (`ID: 456`)

**✅ Verification:**
- **Status Code:** `403 Forbidden`
- **Response Body:**  
  ```json
  {
    "error": "Access to resource is forbidden"
  }
  ```

---

## ⚡ 4. Performance (Edge Case)

**🛠 Action:**  
Observe Postman’s response time metric for a valid user request

**✅ Verification:**
- Acceptable threshold: **< 1000–2000 ms**
- Flag any excessive response time for further analysis (suggest: JMeter, k6)

---
