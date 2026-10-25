# HTTP Headers

## What are HTTP Headers?

HTTP Headers are additional pieces of information sent along with an HTTP request or response.

Think of them as **metadata about the message**.

They don't usually contain the actual business data.

Instead, they describe:

- Who is sending the request
- What format the data is in
- Whether the sender is authenticated
- What response formats are acceptable
- Caching instructions
- Browser information

---

# Mental Model

Imagine ordering food over the phone.

Actual request:

```text
I want a pizza.
```

Additional information:

```text
My address is XYZ.
Pay using credit card.
Please deliver within 30 minutes.
```

The pizza order itself is the main request.

The additional information is similar to HTTP headers.

---

# Anatomy of an HTTP Request

```http
GET /users/101 HTTP/1.1
Host: api.example.com
Accept: application/json
Authorization: Bearer abc123

<Body (optional)>
```

Let's identify the parts:

```text
GET /users/101 HTTP/1.1
↑
Start Line

Host: api.example.com
Accept: application/json
Authorization: Bearer abc123
↑
Headers

<Body>
↑
Data
```

---

# Why Do Headers Exist?

Without headers, a server wouldn't know:

```text
Who are you?
What data format do you want?
What application sent this request?
Are you authenticated?
Can the response be cached?
```

Headers solve these problems.

---

# Header Structure

Every header follows the same format:

```text
Header-Name: Value
```

Example:

```http
Content-Type: application/json
```

Header Name:

```text
Content-Type
```

Value:

```text
application/json
```

---

# Request Headers vs Response Headers

## Request Headers

Sent by the client to the server.

```text
Client
   ↓
Request Headers
   ↓
Server
```

Examples:

```http
Accept: application/json
Authorization: Bearer xyz
Host: api.google.com
```

---

## Response Headers

Sent by the server back to the client.

```text
Server
   ↓
Response Headers
   ↓
Client
```

Examples:

```http
Content-Type: application/json
Content-Length: 150
Server: nginx
```

---

# Most Important Request Headers

---

## Host

Specifies which server you want.

Example:

```http
Host: www.google.com
```

Without this:

```text
Server may not know which site to serve.
```

---

## Accept

Tells the server which response formats are acceptable.

Example:

```http
Accept: application/json
```

Meaning:

```text
Please respond with JSON.
```

Another example:

```http
Accept: application/xml
```

Meaning:

```text
Please respond with XML.
```

---

## Authorization

Used for authentication and security.

Example:

```http
Authorization: Bearer eyJ123...
```

Meaning:

```text
Here is my access token.
```

The server verifies the token before processing the request.

---

## User-Agent

Identifies the client making the request.

Example:

```http
User-Agent: Chrome
```

or

```http
User-Agent: PostmanRuntime
```

or

```http
User-Agent: Python-requests
```

The server can tailor responses based on the client.

---

## Content-Type

Indicates the format of the request body.

Example:

```http
Content-Type: application/json
```

Meaning:

```text
The body contains JSON.
```

---

### Example

Request:

```http
POST /users HTTP/1.1
Content-Type: application/json
```

Body:

```json
{
  "name": "Sushant"
}
```

The server now knows how to parse the body.

---

# Most Important Response Headers

---

## Content-Type

Indicates the format of the response body.

Example:

```http
Content-Type: application/json
```

Response body:

```json
{
  "name": "Sushant"
}
```

The client now knows the response contains JSON.

---

## Content-Length

Indicates the size of the response.

Example:

```http
Content-Length: 250
```

Meaning:

```text
Response body contains 250 bytes.
```

---

## Date

Shows when the response was generated.

Example:

```http
Date: Tue, 21 Oct 2026 09:00:00 GMT
```

---

## Server

Identifies the web server software.

Example:

```http
Server: nginx
```

or

```http
Server: Apache
```

---

# Real API Example

Suppose your application creates an order.

## Request

```http
POST /orders HTTP/1.1
Host: api.ebay.com
Authorization: Bearer abc123
Content-Type: application/json
Accept: application/json

{
  "product": "Laptop",
  "quantity": 1
}
```

---

## What Each Header Does

| Header | Purpose |
|----------|----------|
| Host | Identify server |
| Authorization | Prove who you are |
| Content-Type | Describe request body |
| Accept | Describe desired response format |

---

## Response

```http
HTTP/1.1 201 Created
Content-Type: application/json
Content-Length: 60

{
  "orderId": 12345,
  "status": "Created"
}
```

---

# Where Headers Fit in the HTTP Message

Request:

```http
GET /users/101 HTTP/1.1
Host: api.example.com
Authorization: Bearer token123
Accept: application/json

```

Response:

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 120

{
  "id": 101,
  "name": "Sushant"
}
```

Visualizing:

```text
┌──────────────────────────┐
│ Start Line              │
├──────────────────────────┤
│ Headers                 │
├──────────────────────────┤
│ Blank Line              │
├──────────────────────────┤
│ Body                    │
└──────────────────────────┘
```

---

# Headers in API Interviews

You should be comfortable explaining:

| Header | Common Usage |
|----------|-------------|
| Authorization | Authentication |
| Content-Type | Request/Response format |
| Accept | Desired response format |
| Host | Target server |
| User-Agent | Client identification |
| Content-Length | Message size |

---

# Easy Way to Remember

Think of HTTP as sending a package.

```text
Package
│
├── Address Label
├── Delivery Instructions
├── Sender Information
├── Security Verification
└── Actual Item
```

Equivalent HTTP message:

```text
HTTP Message
│
├── Start Line
├── Headers
├── Blank Line
└── Body
```

---

# Key Takeaway

Headers are **metadata about the HTTP message**.

They help the client and server understand:

- Who is communicating
- What format is being used
- Whether authentication is required
- How to process the message

```text
HTTP Request

Start Line
    +
Headers
    +
Body


HTTP Response

Start Line
    +
Headers
    +
Body
```

> The Start Line tells **what is happening**, the Headers provide **additional instructions and context**, and the Body contains the **actual business data**.