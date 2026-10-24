# HTTP Start Line

Before a client and server exchange data, every HTTP message begins with a **Start Line**.

The Start Line tells the receiver the most important information about the message.

There are two types:

1. **Request Start Line** (sent by the client)
2. **Response Start Line** (sent by the server)

---

# Request vs Response Start Line

| Property | Request Start Line | Response Start Line |
|-----------|-------------------|------------------|
| Also Called | Request Line | Response Line / Status Line |
| Sent By | Client | Server |
| HTTP Version Present? | ✅ Yes | ✅ Yes |
| HTTP Method Present? | ✅ Yes | ❌ No |
| API Endpoint Present? | ✅ Yes | ❌ No |
| Query Parameters Present? | ✅ Yes | ❌ No |
| Status Code Present? | ❌ No | ✅ Yes |
| Purpose | Tell server what action to perform | Tell client the result of the action |

---

# Request Start Line

## Format

```text
METHOD SP PATH?PARAMETERS SP HTTP_VERSION
```

Where:

```text
SP = Single Space
```

General structure:

```text
GET /search?q=tuna HTTP/1.1
```

---

## Components

### 1. Method

Specifies what action should be performed.

Examples:

```text
GET
POST
PUT
PATCH
DELETE
```

Example:

```http
GET /users HTTP/1.1
```

Meaning:

```text
Retrieve users
```

---

### 2. Path (API Endpoint)

Specifies which program or resource should handle the request.

Examples:

```text
/search
/users
/orders
/products
```

Example:

```http
GET /search HTTP/1.1
```

Meaning:

```text
Run the search functionality
```

---

### 3. Query Parameters

Extra information supplied to the endpoint.

Example:

```text
?q=tuna
```

Here:

| Parameter | Value |
|------------|---------|
| q | tuna |

Complete Request Line:

```http
GET /search?q=tuna HTTP/1.1
```

Meaning:

```text
Run Search
Search Term = tuna
```

---

### 4. HTTP Version

Specifies which HTTP standard is being used.

Common values:

```text
HTTP/1.1
HTTP/2
HTTP/3
```

Example:

```http
GET /search?q=tuna HTTP/1.1
```

---

# Request Start Line Breakdown

Example:

```http
GET /search?q=tuna HTTP/1.1
```

Let's break it apart:

```text
GET
 │
 └── Action to perform

/search
 │
 └── Endpoint to execute

?q=tuna
 │
 └── Parameter supplied

HTTP/1.1
 │
 └── HTTP Protocol Version
```

---

# Google Search Example

Suppose you search:

```text
tuna
```

Google's browser request might conceptually look like:

```http
GET /search?q=tuna HTTP/1.1
```

Interpretation:

| Component | Meaning |
|------------|-----------|
| GET | Retrieve data |
| /search | Run Google's search program |
| q=tuna | Search term |
| HTTP/1.1 | Protocol version |

---

# Response Start Line

After processing the request, the server responds.

## Format

```text
HTTP_VERSION SP STATUS_CODE SP STATUS_TEXT
```

Example:

```http
HTTP/1.1 200 OK
```

---

## Components

### 1. HTTP Version

Indicates the protocol version used.

Example:

```text
HTTP/1.1
```

---

### 2. Status Code

A numeric value indicating success or failure.

Examples:

| Code | Meaning |
|---------|---------|
| 200 | Success |
| 201 | Resource Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |
| 500 | Internal Server Error |

---

### 3. Status Text

Human-readable explanation.

Examples:

```text
OK
Created
Not Found
Unauthorized
Internal Server Error
```

---

# Response Start Line Breakdown

Example:

```http
HTTP/1.1 200 OK
```

Breakdown:

```text
HTTP/1.1
    │
    └── Protocol Version

200
 │
 └── Status Code

OK
 │
 └── Status Message
```

---

# Complete Client-Server Conversation

## Request

```http
GET /search?q=tuna HTTP/1.1
```

Meaning:

```text
Run Search Program
Search for "tuna"
```

---

## Server Processing

```text
Request Received
        ↓
Search Program Runs
        ↓
Results Found
```

---

## Response

```http
HTTP/1.1 200 OK
```

Meaning:

```text
Request successfully completed.
```

---

# Visual Flow

```text
CLIENT

GET /search?q=tuna HTTP/1.1
│
│ Request Start Line
▼

SERVER

Run Search Program
│
▼

HTTP/1.1 200 OK
│
│ Response Start Line
▼

CLIENT
```

---

# How the Start Line Fits Into an HTTP Message

A complete HTTP Request looks like:

```http
GET /search?q=tuna HTTP/1.1
Host: google.com
User-Agent: Chrome

<optional body>
```

Notice:

```text
Line 1 = Start Line
Line 2+ = Headers
Blank Line
Body (optional)
```

---

A complete HTTP Response looks like:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
   "results": [
      "Result 1",
      "Result 2"
   ]
}
```

Again:

```text
Line 1 = Start Line
Line 2+ = Headers
Blank Line
Response Body
```

---

# Mental Model

Think of the **Request Start Line** as an instruction:

```text
"What do you want me to do?"
```

Example:

```http
GET /search?q=tuna HTTP/1.1
```

---

Think of the **Response Start Line** as an answer:

```text
"Did it work?"
```

Example:

```http
HTTP/1.1 200 OK
```

---

# Key Takeaway

```text
Request Start Line
=
Method + Endpoint + Parameters + HTTP Version

Response Start Line
=
HTTP Version + Status Code + Status Message
```

Example pair:

```http
GET /search?q=tuna HTTP/1.1
```

```http
HTTP/1.1 200 OK
```

The request start line tells the server **what to do**, while the response start line tells the client **what happened**.