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

# HTTP Methods: Idempotence

## What is Idempotence?

A request is **idempotent** if making the same request multiple times produces the **same final state** on the server.

### Simple Definition

> An operation is **idempotent** when repeating it does not change the outcome beyond the initial execution.

Or put another way:

```text
Safe to repeat
```

---

# Why Does Idempotence Matter?

In distributed systems, things go wrong:

- Network timeouts
- Lost responses
- Retries
- Temporary connectivity issues

A client may not know whether the server successfully processed a request.

So it may send the same request again.

```text
Request
   ↓
Timeout Occurs
   ↓
Client Unsure
   ↓
Retry Request
```

If the operation is idempotent, retrying is safe.

---

# HTTP Methods and Idempotence

| Method | Idempotent? | Safe to Repeat? |
|----------|------------|----------------|
| GET | ✅ Yes | Yes |
| POST | ❌ No | No |
| PUT | ✅ Yes | Yes |
| DELETE | ✅ Yes | Yes |

---

# GET is Idempotent

A GET request only retrieves information.

Example:

```http
GET /users/101
```

Response:

```json
{
  "id": 101,
  "name": "Sushant"
}
```

You can execute the request:

```text
1 time
10 times
100 times
```

The final state of the server never changes.

```text
No modification
No new records
No updates
No deletion
```

Therefore:

```text
GET = Idempotent
```

---

# PUT is Idempotent

PUT replaces a resource with the supplied representation.

Suppose user 101 currently has:

```json
{
  "name": "John"
}
```

Request:

```http
PUT /users/101
```

```json
{
  "name": "Sushant"
}
```

---

## First Execution

Server state becomes:

```json
{
  "name": "Sushant"
}
```

---

## Second Execution

Exactly the same request:

```http
PUT /users/101
```

```json
{
  "name": "Sushant"
}
```

Server state remains:

```json
{
  "name": "Sushant"
}
```

Nothing changes.

---

## Third Execution

Same result.

```text
Final state remains unchanged
```

Therefore:

```text
PUT = Idempotent
```

---

# DELETE is Idempotent

Imagine:

```http
DELETE /users/101
```

---

## First Execution

User is removed.

```text
User exists → Deleted
```

---

## Second Execution

User already does not exist.

```text
Still deleted
```

---

## Third Execution

Nothing changes.

The server may return:

```http
404 Not Found
```

but the important point is:

```text
The final state remains the same.
```

There is still no user.

Therefore:

```text
DELETE = Idempotent
```

---

# POST is NOT Idempotent

POST usually creates new resources.

Example:

```http
POST /orders
```

```json
{
  "product": "Laptop"
}
```

---

## First Execution

Creates:

```text
Order #1001
```

---

## Second Execution

Creates:

```text
Order #1002
```

---

## Third Execution

Creates:

```text
Order #1003
```

---

Result:

```text
More executions
=
More resources
=
Different server state
```

Therefore:

```text
POST = Not Idempotent
```

---

# Visual Comparison

## GET

```text
GET User
     ↓
User Data Returned

GET User
     ↓
User Data Returned

GET User
     ↓
User Data Returned
```

Server state:

```text
Unchanged
```

✅ Idempotent

---

## PUT

```text
Set Name = Sushant
     ↓
Updated

Set Name = Sushant
     ↓
No Additional Change

Set Name = Sushant
     ↓
No Additional Change
```

Server state:

```text
Same
```

✅ Idempotent

---

## DELETE

```text
Delete User
     ↓
Deleted

Delete User
     ↓
Already Deleted

Delete User
     ↓
Still Deleted
```

Server state:

```text
No User Exists
```

✅ Idempotent

---

## POST

```text
Create Order
     ↓
Order #1

Create Order
     ↓
Order #2

Create Order
     ↓
Order #3
```

Server state:

```text
Keeps changing
```

❌ Not Idempotent

---

# Common Interview Question

## Does Idempotent Mean the Response Must Be Identical?

**No.**

A very common misconception is:

```text
Same Request
=
Same Response
```

This is NOT the definition of idempotence.

The real definition is:

```text
Same Request
=
Same Final Server State
```

### Example

```http
DELETE /users/101
```

First response:

```http
200 OK
```

Second response:

```http
404 Not Found
```

Responses differ.

But the server state is still:

```text
User does not exist
```

Therefore the operation remains idempotent.

---

# Idempotence vs Safe Methods

These concepts are related but different.

| Concept | Meaning |
|----------|----------|
| Safe | Does not modify server state |
| Idempotent | Can be repeated without changing the final state |

---

## Safe Methods

```text
GET
HEAD
OPTIONS
```

These should not modify data.

---

## Idempotent Methods

```text
GET
PUT
DELETE
```

These may modify data, but repeating them leads to the same final state.

Example:

```text
PUT changes data
```

Yet it is still idempotent.

---

# Mental Model

Think of a light switch.

### Idempotent

```text
Set Light = ON
```

Execute once:

```text
Light ON
```

Execute ten times:

```text
Light ON
```

Final state never changes.

✅ Idempotent

---

### Non-Idempotent

```text
Increase Counter by 1
```

Execute once:

```text
Counter = 1
```

Execute again:

```text
Counter = 2
```

Execute again:

```text
Counter = 3
```

State keeps changing.

❌ Not Idempotent

---

# Key Takeaway

> **Idempotence means that repeating the same request produces the same final state on the server.**

| Method | Idempotent? | Reason |
|----------|-------------|---------|
| GET | ✅ | Reads data only |
| PUT | ✅ | Replaces resource with same value each time |
| DELETE | ✅ | Resource remains deleted |
| POST | ❌ | Usually creates additional resources |

### Remember

```text
Idempotent ≠ Same Response

Idempotent = Same Final Server State
```