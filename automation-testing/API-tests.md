# Playwright API Tests

| TC#  | Steps / Expected Result |
|------|------------------------|
| TC001 | GET `/users`. Validate status 200. List contains user objects with id, name, email. |
| TC002 | GET `/users/{id}` for existing user. Status 200, returned user matches created user. |
| TC003 | GET `/users/{id}` for non-existing user. Status 404. |
| TC004 | POST `/users` with valid payload. Status 201, returns new ID. |
| TC005 | POST `/users` with missing fields. Status 400. |
| TC006 | PUT `/users/{id}` updates user. Status 200, updated fields returned. |
| TC007 | DELETE `/users/{id}`. Status 204, GET afterwards returns 404. |
| TC008 | GET `/users` schema validation. Matches JSON schema. |
| TC009 | GET `/users`, validate data types (id:number, email:string). |
| TC010 | GET `/users` without token. Status 401. |
| TC011 | GET `/users` with expired token. Status 401. |
| TC012 | GET `/admin/reports` with normal user. Status 403. |
| TC013 | POST `/users` with invalid JSON. Status 400. |
| TC014 | PATCH `/users` unsupported method. Status 405. |
| TC015 | GET `/users`, measure response time <300ms. Status 200. |
| TC016 | Send 10 parallel GET `/users`. All responses 200. |
| TC017 | POST `/users` and check DB record exists. |
| TC018 | PUT `/users/{id}` and check DB updated. |
| TC019 | GET `/users` schema backwards compatibility. |
| TC020 | GET `/users` required fields exist: id, name, email. |

---

## TC001 — GET `/users` — Successful retrieval
```ts
import { test, expect } from "@playwright/test";

test("TC001: GET /users returns list", async ({ request }) => {
  const res = await request.get("/users");
  expect(res.status()).toBe(200);

  const body = await res.json();
  expect(Array.isArray(body)).toBe(true);
});
```
## TC003 — GET /users/{id} — Not found
```ts
test("TC003: GET /users/{id} returns 404", async ({ request }) => {
  const res = await request.get("/users/99999999");
  expect(res.status()).toBe(404);
});
```
## TC004 — POST /users — Create user
```ts
test("TC004: POST /users creates user", async ({ request }) => {
  const res = await request.post("/users", { data: { name: "Kate", email: "kate@test.com" } });
  expect(res.status()).toBe(201);

  const body = await res.json();
  expect(body.id).toBeTruthy();
});
```
## TC005 — POST /users — Missing fields
```ts
test("TC005: POST /users returns 400 on invalid payload", async ({ request }) => {
  const res = await request.post("/users", { data: { name: "" } });
  expect(res.status()).toBe(400);
});
```
## TC006 — PUT /users/{id} — Update
```ts
test("TC006: PUT /users updates user", async ({ request }) => {
  const create = await request.post("/users", { data: { name: "Old", email: "old@test.com" } });
  const user = await create.json();

  const res = await request.put(`/users/${user.id}`, { data: { name: "Updated" } });
  expect(res.status()).toBe(200);

  const body = await res.json();
  expect(body.name).toBe("Updated");
});
```
## TC007 — DELETE /users/{id}
```ts
test("TC007: DELETE /users deletes user", async ({ request }) => {
  const create = await request.post("/users", { data: { name: "Delete", email: "del@test.com" } });
  const user = await create.json();

  const del = await request.delete(`/users/${user.id}`);
  expect(del.status()).toBe(204);

  const check = await request.get(`/users/${user.id}`);
  expect(check.status()).toBe(404);
});
```
## TC008 — Schema validation
```ts
import { validateSchema } from "../helpers/schemaValidator";

test("TC008: /users schema matches contract", async ({ request }) => {
  const res = await request.get("/users");
  await validateSchema(res, "user.schema.json");
});
```
## TC009 — Data type validation
```ts
test("TC009: Validate data types", async ({ request }) => {
  const res = await request.get("/users");
  const body = await res.json();
  const user = body[0];

  expect(typeof user.id).toBe("number");
  expect(typeof user.email).toBe("string");
});
```
## TC010 — No token
```ts
test("TC010: Returns 401 without token", async () => {
  const { request } = await import("@playwright/test");
  const res = await request.newContext().get("https://api.example.com/users");
  expect(res.status()).toBe(401);
});
```
## TC011 — Expired token
```ts
test("TC011: Expired token returns 401", async ({ request }) => {
  const res = await request.get("/users", { headers: { Authorization: "Bearer expired.token.here" } });
  expect(res.status()).toBe(401);
});
```
## TC012 — Forbidden access
```ts
test("TC012: Forbidden for normal user on admin route", async ({ request }) => {
  const res = await request.get("/admin/reports", { headers: { Authorization: "Bearer user_token" } });
  expect(res.status()).toBe(403);
});
```
## TC013 — Invalid JSON
```ts
test("TC013: Invalid JSON → 400", async ({ request }) => {
  const res = await request.fetch("/users", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: "{invalid-json}",
  });
  expect(res.status()).toBe(400);
});
```
## TC014 — Unsupported method
```ts
test("TC014: Unsupported HTTP method → 405", async ({ request }) => {
  const res = await request.patch("/users");
  expect(res.status()).toBe(405);
});
```
## TC015 — Response time
```ts
test("TC015: Response < 300ms", async ({ request }) => {
  const start = Date.now();
  const res = await request.get("/users");
  const duration = Date.now() - start;

  expect(res.status()).toBe(200);
  expect(duration).toBeLessThan(300);
});
```
## TC016 — Basic concurrency (10 requests)
```ts
test("TC016: 10 parallel requests", async ({ request }) => {
  const promises = Array.from({ length: 10 }, () => request.get("/users"));
  const responses = await Promise.all(promises);

  for (const res of responses) {
    expect(res.status()).toBe(200);
  }
});
```
## TC017 — DB record exists after POST
```ts
test("TC017: Database contains created user", async ({ request }) => {
  const res = await request.post("/users", { data: { name: "DBcheck", email: "db@test.com" } });
  const user = await res.json();

  // pseudo-check
  const dbRecord = await getUserFromDB(user.id);
  expect(dbRecord.name).toBe("DBcheck");
});
```
## TC018 — DB updated after PUT
```ts
test("TC018: Database record updated", async ({ request }) => {
  const create = await request.post("/users", { data: { name: "Initial", email: "init@test.com" } });
  const user = await create.json();

  await request.put(`/users/${user.id}`, { data: { name: "DBupdated" } });

  const dbRecord = await getUserFromDB(user.id);
  expect(dbRecord.name).toBe("DBupdated");
});
```
## TC019 — No breaking changes in schema
```ts
test("TC019: Schema backwards compatibility", async ({ request }) => {
  const res = await request.get("/users");
  await validateSchema(res, "user.schema.json");
});
```
## TC020 — Required fields must exist
```ts
test("TC020: Required fields exist", async ({ request }) => {
  const res = await request.get("/users");
  const body = await res.json();
  const user = body[0];

  expect(user).toHaveProperty("id");
  expect(user).toHaveProperty("name");
  expect(user).toHaveProperty("email");
});
```
