# HTTP Body

## What is an HTTP Body?

The **HTTP Body** is the part of an HTTP message that contains the **actual data being sent** between the client and server.

Think of it as the main content or payload of the request/response.

---

# HTTP Message Structure

An HTTP message consists of:

```text
Start Line
Headers
Blank Line
Body
```

Visualized:

```text
┌──────────────────────────┐
│ Start Line              │
├──────────────────────────┤
│ Headers                 │
├──────────────────────────┤
│ Blank Line              │
├──────────────────────────┤
│ Body (Actual Data)      │
└──────────────────────────┘
```

---

# Mental Model

Suppose you are sending a courier package.

```text
Shipping Label     → Start Line
Special Instructions → Headers
Package Contents    → Body
```

The body is the actual thing you care about.

---

# Why Do We Need a Body?

Imagine creating a new user.

The Start Line can tell the server:

```http
POST /users HTTP/1.1
```

This means:

```text
Create a user.
```

But it doesn't answer:

```text
Which user?
What is the name?
What is the email?
What is the city?
```

The body carries this information.

---

# Example Request Body

Request:

```http
POST /users HTTP/1.1
Content-Type: application/json
```

Body:

```json
{
  "name": "Sushant",
  "email": "sushant@example.com",
  "city": "Bangalore"
}
```

The body contains the data needed to create the user.

---

# HTTP Body in the Request

## Client Sends Data

Common examples:

- Create a user
- Create an order
- Update a profile
- Upload a file

Example:

```http
POST /orders HTTP/1.1
Content-Type: application/json
```

```json
{
  "product": "Laptop",
  "quantity": 1
}
```

The JSON object is the body.

---

# HTTP Body in the Response

The server can also send data back.

Example:

```http
HTTP/1.1 200 OK
Content-Type: application/json
```

```json
{
  "orderId": 12345,
  "status": "Created"
}
```

The JSON response is the response body.

---

# Complete Example

## Request

```http
POST /users HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "name": "Sushant"
}
```

---

## Server Processing

```text
Receive Request
       ↓
Extract Body
       ↓
Create User
       ↓
Generate Response
```

---

## Response

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 101,
  "name": "Sushant"
}
```

---

# Which HTTP Methods Usually Have a Body?

| Method | Request Body Usually Present? |
|----------|----------|
| GET | ❌ No |
| POST | ✅ Yes |
| PUT | ✅ Yes |
| PATCH | ✅ Yes |
| DELETE | Usually No |

---

# Why GET Usually Doesn't Have a Body

GET is intended to retrieve data.

Information is typically supplied through:

```http
GET /search?q=tuna
```

Instead of:

```http
GET /search
```

```json
{
  "term": "tuna"
}
```

Most APIs therefore avoid request bodies for GET requests.

---

# POST Body Example

Creating an order:

```http
POST /orders
```

Body:

```json
{
  "product": "Laptop",
  "quantity": 1
}
```

Each field describes the resource to create.

---

# PUT Body Example

Replacing a user:

```http
PUT /users/101
```

Body:

```json
{
  "name": "Sushant",
  "city": "Bangalore"
}
```

The body contains the complete updated version.

---

# PATCH Body Example

Updating only one field:

```http
PATCH /users/101
```

Body:

```json
{
  "city": "Mumbai"
}
```

Only the specified field changes.

---

# Common Body Formats

The body can contain data in many formats.

---

## JSON (Most Common)

```json
{
  "name": "Sushant",
  "city": "Bangalore"
}
```

Used by most modern REST APIs.

---

## XML

```xml
<user>
  <name>Sushant</name>
  <city>Bangalore</city>
</user>
```

Common in SOAP services and older enterprise systems.

---

## Plain Text

```text
Hello World
```

---

## File Uploads

```text
image.png
document.pdf
resume.docx
```

The body contains the file itself.

---

# How Does the Server Know the Body Format?

Using the **Content-Type** header.

Example:

```http
Content-Type: application/json
```

Meaning:

```text
The body contains JSON.
```

---

Another example:

```http
Content-Type: application/xml
```

Meaning:

```text
The body contains XML.
```

---

# Relationship Between Headers and Body

Headers describe the body.

Body contains the actual data.

Example:

```http
Content-Type: application/json
Content-Length: 75
```

Headers tell us:

```text
Format = JSON
Size = 75 bytes
```

Body:

```json
{
  "name": "Sushant"
}
```

Actual payload.

---

# Visual API Flow

```text
Client
   │
   │ Body:
   │ {
   │   "name":"Sushant"
   │ }
   ▼

API
   ▼

Program
   ▼

Database
   ▼

Response Body:
{
  "id":101,
  "name":"Sushant"
}
```

---

# Start Line vs Headers vs Body

| Component | Purpose | Example |
|------------|----------|----------|
| Start Line | What action should be performed? | `POST /users HTTP/1.1` |
| Headers | Additional instructions and metadata | `Content-Type: application/json` |
| Body | Actual data | `{ "name": "Sushant" }` |

---

# Putting It All Together

```http
POST /users HTTP/1.1
Host: api.example.com
Authorization: Bearer token123
Content-Type: application/json

{
  "name": "Sushant",
  "city": "Bangalore"
}
```

Breakdown:

```text
POST /users HTTP/1.1
↑
Start Line

Host
Authorization
Content-Type
↑
Headers

{
  "name": "Sushant",
  "city": "Bangalore"
}
↑
Body
```

---

# Final Mental Model

Think of an HTTP request as filling out a form:

```text
What do you want to do?
        ↓
Start Line

Additional Instructions
        ↓
Headers

Actual Information
        ↓
Body
```

Or even more simply:

```text
Start Line = Action

Headers = Metadata

Body = Data
```

> The **HTTP Body** is where the actual business information lives. If you are creating, updating, uploading, or returning meaningful data, that data is usually carried inside the body.