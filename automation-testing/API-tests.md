**TC-001: GET /users — Successful retrieval**

|  Steps: Send GET `/users`. Validate status code \= 200\. Validate list contains user objects. Validate fields: id, name, email. Expected Result: Status 200 Valid JSON Non-empty list | `import { test, expect } from "@playwright/test"; test("TC001: GET /users returns list", async ({ request }) => {   const res = await request.get("/users");   expect(res.status()).toBe(200);   const body = await res.json();   expect(Array.isArray(body)).toBe(true); });` |
| :---- | :---- |

### **TC-002: GET /users/{id} — User found**

| Steps: Create a user. GET user by ID. Expected: 200 OK Correct user returned | ``test("TC002: GET /users/{id} returns existing user", async ({ request }) => {   const create = await request.post("/users", {     data: { name: "Kate", email: "kate@test.com" },   });   const createdUser = await create.json();   const res = await request.get(`/users/${createdUser.id}`);   expect(res.status()).toBe(200);   const body = await res.json();   expect(body.id).toBe(createdUser.id); });``  |
| :---- | :---- |

### **TC-003: GET /users/{id} — User not found**

| Steps: GET /users/999999 Expected: 404 Not Found Error message: “User not found” | `test("TC003: GET /users/{id} returns 404", async ({ request }) => {   const res = await request.get("/users/99999999");   expect(res.status()).toBe(404); });` |
| :---- | :---- |

### 

### 

### **TC-004: POST /users — Create user successfully**

| Steps: POST JSON body `{name: "Kate", email: "test@test.com"}` Expected: 201 Created New ID returned | `test("TC004: POST /users creates user", async ({ request }) => {   const res = await request.post("/users", {     data: { name: "Kate", email: "kate@test.com" },   });   expect(res.status()).toBe(201);   const body = await res.json();   expect(body.id).toBeTruthy(); });` |
| :---- | :---- |

### **TC-005: POST /users — Missing required fields**

| Steps: POST `{name: ""}` Expected: 400 Bad Request Validation errors | `test("TC005: POST /users returns 400 on invalid payload", async ({ request }) => {   const res = await request.post("/users", {     data: { name: "" },   });   expect(res.status()).toBe(400); });`  |
| :---- | :---- |

### **TC-006: PUT /users/{id} — Update user**

| Expected: 200 OK Updated fields returned | ``test("TC006: PUT /users updates user", async ({ request }) => {   const create = await request.post("/users", {     data: { name: "Old", email: "old@test.com" },   });   const user = await create.json();   const res = await request.put(`/users/${user.id}`, {     data: { name: "Updated" },   });   expect(res.status()).toBe(200);   const body = await res.json();   expect(body.name).toBe("Updated"); });`` |
| :---- | :---- |

### 

### **TC-007: DELETE /users/{id} — Remove user**

| Expected: 204 No Content GET afterwards returns 404 | ``test("TC007: DELETE /users deletes user", async ({ request }) => {   const create = await request.post("/users", {     data: { name: "Delete", email: "del@test.com" },   });   const user = await create.json();   const del = await request.delete(`/users/${user.id}`);   expect(del.status()).toBe(204);   const check = await request.get(`/users/${user.id}`);   expect(check.status()).toBe(404); });`` |
| :---- | :---- |

**TC-008: Validate JSON Schema for /users**

| Expected: Response matches schema All required fields exist No unexpected fields | (Assuming `validateSchema()` helper exists) `import { validateSchema } from "../helpers/schemaValidator"; test("TC008: /users schema matches contract", async ({ request }) => {   const res = await request.get("/users");   await validateSchema(res, "user.schema.json"); });` |
| :---- | :---- |

### **TC-009: Validate data types**

| Expected: `id` is number `email` is string `isActive` is boolean | `test("TC009: Validate data types", async ({ request }) => {   const res = await request.get("/users");   const body = await res.json();   const user = body[0];   expect(typeof user.id).toBe("number");   expect(typeof user.email).toBe("string"); });` |
| :---- | :---- |

### **TC-010: Access without token**

| Steps: GET `/users` without Authorization header Expected: 401 Unauthorized | `test("TC010: Returns 401 without token", async () => {   const { request } = await import("@playwright/test");   const res = await request.newContext().get("https://api.example.com/users");   expect(res.status()).toBe(401); });` |
| :---- | :---- |

### **TC-011: Access with expired token**

| Expected: 401 Unauthorized Message: “Token expired” | `test("TC011: Expired token returns 401", async ({ request }) => {   const res = await request.get("/users", {     headers: { Authorization: "Bearer expired.token.here" },   });   expect(res.status()).toBe(401); });` |
| :---- | :---- |

### **TC-012: User with role "user" accessing admin endpoint**

| Expected: 403 Forbidden | `test("TC012: Forbidden for normal user on admin route", async ({ request }) => {   const res = await request.get("/admin/reports", {     headers: { Authorization: "Bearer user_token" },   });   expect(res.status()).toBe(403); });` |
| :---- | :---- |

### **TC-013: Send invalid JSON**

| Steps: POST invalid JSON payload Expected: 400 Bad Request | `test("TC013: Invalid JSON → 400", async ({ request }) => {   const res = await request.fetch("/users", {     method: "POST",     headers: { "Content-Type": "application/json" },     body: "{invalid-json}",   });   expect(res.status()).toBe(400); });`  |
| :---- | :---- |

### 

### 

### **TC-014: Unsupported HTTP method**

| Steps: PATCH an endpoint that only supports PUT Expected: 405 Method Not Allowed | `test("TC014: Unsupported HTTP method → 405", async ({ request }) => {   const res = await request.patch("/users");   expect(res.status()).toBe(405); });` |
| :---- | :---- |

### **TC-015: Response time \< 300ms**

| Expected: Pass if \< 300ms | `test("TC015: Response < 300ms", async ({ request }) => {   const start = Date.now();   const res = await request.get("/users");   const duration = Date.now() - start;   expect(res.status()).toBe(200);   expect(duration).toBeLessThan(300); });` |
| :---- | :---- |

### **TC-016: Basic concurrency (10 requests)**

| Expected: All responses success No timeouts | `test("TC016: 10 parallel requests", async ({ request }) => {   const promises = Array.from({ length: 10 }, () => request.get("/users"));   const responses = await Promise.all(promises);   for (const res of responses) {     expect(res.status()).toBe(200);   } });` |
| :---- | :---- |

### **TC-017: Verify DB created record after POST**

| Expected: DB contains new user Fields match request | (You need a DB helper; here simplified) `test("TC017: Database contains created user", async ({ request }) => {   const res = await request.post("/users", {     data: { name: "DBcheck", email: "db@test.com" },   });   const user = await res.json();   // pseudo-check:   const dbRecord = await getUserFromDB(user.id);   expect(dbRecord.name).toBe("DBcheck"); });` |
| :---- | :---- |

### **TC-018: Verify DB updated record after PUT**

| Expected: DB row updated correctly | ``test("TC018: Database record updated", async ({ request }) => {   const create = await request.post("/users", {     data: { name: "Initial", email: "init@test.com" },   });   const user = await create.json();   await request.put(`/users/${user.id}`, {     data: { name: "DBupdated" },   });   const dbRecord = await getUserFromDB(user.id);   expect(dbRecord.name).toBe("DBupdated"); });`` |
| :---- | :---- |

### **TC-019: No breaking changes in schema**

| Expected: No removed fieldsNo type changes | `test("TC019: Schema backwards compatibility", async ({ request }) => {   const res = await request.get("/users");   // use schema validator here   await validateSchema(res, "user.schema.json"); });` |
| :---- | :---- |

**TC-020: Required fields must always exist**

| Expected: id, email, name always present | `test("TC020: Required fields exist", async ({ request }) => {   const res = await request.get("/users");   const body = await res.json();   const user = body[0];   expect(user).toHaveProperty("id");   expect(user).toHaveProperty("name");   expect(user).toHaveProperty("email"); });`  |
| :---- | :---- |

