\# 🧪 How to Mock an API in Postman

---

\### 🔧 Step 1: Create a New Collection

1\. Open \*\*Postman\*\*. 2. Click \*\*"Collections"\*\* in the left
sidebar. 3. Click the \*\*"+ New Collection"\*\* button. 4. Give your
collection a name (e.g., \`User API Mock\`). 5. Click \*\*Save\*\*.

\-\--

\### 📄 Step 2: Add a Request to the Collection

1\. Click on the new collection name. 2. Click \*\*"Add a request"\*\*.
3. Name the request (e.g., \`Get User\`). 4. Set the request method to
\`GET\`. 5. Set the request URL to something like:
https://example.com/api/users/:userId 6. Switch to the
\*\*"Examples"\*\* tab (next to "Body"). 7. Click \*\*"Add Example"\*\*.

\-\--

\### 📝 Step 3: Create a Sample Response

1\. Enter a name for your example (e.g., \`User Found\`). 2. In the
\*\*response body\*\*, add sample JSON: \`\`\`json { \"id\": 123,
\"name\": \"Alice\", \"email\": \"alice@example.com\" } 3. Set Status
Code to 200 OK. 4. Set the Content-Type header to application/json. 5.
Click Save Example.

\-\--

\### 🌐 Step 4: Create a Mock Server 1. Click the "..." (three dots)
next to your collection. 2. Select "Mock Collection". 3. In the popup:
\* Choose "Create a new mock server" \* Name your mock server \* Choose
whether to make it private or public \* Enable Save responses (optional)
\* Click Create Mock Server.

\*\*Postman will now generate a mock URL, e.g\*\*
\*\*https://mock-server.example.com/api/users/:userId\*\*
