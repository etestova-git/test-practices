# API Testing Best Practices

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

## 📌 Notes

- All tests should be included in Postman collections with preconditions & assertions
- Use **Pre-request Script** and **Test** tabs in Postman for validation
- Store expected values in environment or collection variables for reuse
