# HTTP Explained from Scratch

Before understanding modern APIs, you need to understand **HTTP** because most APIs communicate using HTTP.

---

# What is HTTP?

**HTTP** stands for:

```text
HyperText Transfer Protocol
```

Don't worry about the full form initially.

The simplest definition is:

> HTTP is a set of rules that defines how a client and server communicate over the web.

---

# Why Do We Need HTTP?

Imagine you call a restaurant and say:

```text
"I want a pizza."
```

The restaurant understands:

- What you want
- How to process the request
- How to respond

There is a common language between you and the restaurant.

HTTP is that common language for computers.

Without HTTP:

```text
Browser ❌ Server
```

The browser wouldn't know how to ask for something, and the server wouldn't know how to respond.

---

# The Two Participants

Every HTTP communication involves two parties:

| Component | Role |
|------------|------|
| Client | Sends requests |
| Server | Sends responses |

---

# The Structures

- 1. Start Line (Request Line for Request, Status line for response)
- 2. Headers
- 3. Blank Line
- 4. Body

## Example: Google Search

```text
Client                      Server
(Browser)                   (Google)

     Request
        ────────►

        ◄────────
          Response
```

You are not directly talking to Google.

Your browser talks to Google on your behalf.

---

# The HTTP Flow

At its core:

```text
Client
   ↓
Request
   ↓
Server
   ↓
Response
   ↓
Client
```

This simple pattern powers:

- Google Search
- YouTube
- Gmail
- Amazon
- REST APIs
- Mobile App APIs

Almost everything on the web.

---

# Google Search Example

Suppose you search:

```text
What is HTTP?
```

### Step 1: Request

Your browser sends:

```text
"Please search for HTTP"
```

to Google.

---

### Step 2: Processing

Google's search program runs.

```text
Browser
    ↓
Google
    ↓
Search Program
```

---

### Step 3: Response

Google returns:

```text
Search results
```

---

### Complete Flow

```text
Browser
   ↓
HTTP Request
   ↓
Google Server
   ↓
Search Program
   ↓
HTTP Response
   ↓
Browser
```

---

# What Does an HTTP Request Contain?

A request is made up of several pieces.

```text
METHOD
URL
HEADERS
BODY (optional)
```

---

## Example Request

```http
GET /search?q=http HTTP/1.1
Host: google.com
```

Don't worry about syntax yet.

Let's break it down.

---

# 1. Method

The method tells the server:

> What do you want me to do?

Common HTTP methods:

| Method | Meaning |
|----------|---------|
| GET | Retrieve data |
| POST | Create data |
| PUT | Replace data |
| PATCH | Update data |
| DELETE | Remove data |

---

## Example

```http
GET /users
```

Meaning:

```text
Give me users.
```

---

## Another Example

```http
DELETE /users/100
```

Meaning:

```text
Delete user 100.
```

---

# 2. URL

The URL identifies what resource you want.

Example:

```http
https://google.com/search
```

Breakdown:

```text
https://       Protocol
google.com    Server
/search       Resource
```

---

# Real Example

```http
https://api.weather.com/weather
```

means:

```text
Contact api.weather.com
and access /weather
```

---

# 3. Headers

Headers provide extra information.

Think of them as metadata.

---

## Example

```http
Content-Type: application/json
```

Meaning:

```text
I am sending JSON data.
```

---

Another example:

```http
Authorization: Bearer XYZ
```

Meaning:

```text
Here is my access token.
```

---

# 4. Body

The body contains actual data.

Usually used with:

- POST
- PUT
- PATCH

---

## Example

```json
{
  "name": "Sushant",
  "city": "Bangalore"
}
```

This data goes inside the request body.

---

# What Does the Server Return?

The server returns an HTTP Response.

A response has:

```text
Status Code
Headers
Body
```

---

# Status Code

The status code tells whether the request succeeded.

---

## Common Status Codes

| Code | Meaning |
|--------|---------|
| 200 | Success |
| 201 | Created Successfully |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## Example

```http
HTTP/1.1 200 OK
```

Means:

```text
Everything worked.
```

---

## Example

```http
HTTP/1.1 404 Not Found
```

Means:

```text
I couldn't find that resource.
```

---

# Response Body

The actual data comes back in the response body.

Example:

```json
{
  "temperature": 28,
  "city": "Bangalore"
}
```

---

# Putting Everything Together

Imagine a weather application.

## Request

```http
GET /weather/bangalore
Host: api.weather.com
```

---

## Server Processing

```text
Receive Request
      ↓
Run Weather Program
      ↓
Fetch Data
```

---

## Response

```http
HTTP/1.1 200 OK
```

```json
{
  "city": "Bangalore",
  "temperature": 28
}
```

---

# How HTTP Fits Into APIs

Remember our API model:

```text
Interface (I)
      ↓
Program (P)
      ↓
Application (A)
```

Now let's add HTTP.

```text
Client
   ↓
HTTP Request
   ↓
API (Interface)
   ↓
Program
   ↓
Application
   ↓
HTTP Response
   ↓
Client
```

---

# Google Search Through HTTP

```text
Browser
   ↓
HTTP Request
   ↓
Google API / Search Endpoint
   ↓
Search Program
   ↓
Google
   ↓
HTTP Response
   ↓
Browser
```

---

# eBay API Example

Without any user interface:

```text
Order System
      ↓
HTTP POST Request
      ↓
eBay API
      ↓
Create Order Program
      ↓
eBay
      ↓
HTTP Response
      ↓
Order System
```

Notice:

```text
HTTP is simply the delivery mechanism.
```

The actual business work is still performed by:

```text
Program (P)
inside
Application (A)
```

---

# API vs HTTP

Many beginners confuse these.

They are not the same.

| Term | Purpose |
|---------|----------|
| API | Defines functionality that can be used |
| HTTP | Defines how the request and response travel |
| Web Service | API exposed over HTTP/Internet |

---

## Analogy

Imagine ordering food.

```text
Restaurant = Application

Cook = Program

Waiter = API

Language used to speak =
HTTP
```

Flow:

```text
Customer
   ↓
HTTP
   ↓
Waiter (API)
   ↓
Cook (Program)
   ↓
Food
   ↓
Waiter
   ↓
HTTP
   ↓
Customer
```

---

# Final Mental Model

```text
                 HTTP

Client  ─────────────────► API
                           │
                           ▼
                       Program
                           │
                           ▼
                       Application
                           │
                           ▼

Client ◄────────────────── Response
```

> **HTTP is the communication protocol that carries requests and responses between a client and a server. APIs often use HTTP as the transport mechanism to invoke programs running inside applications.**