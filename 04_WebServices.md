# What is a Web Service?

## Definition

Let's break down the term:

| Term | Meaning |
|--------|---------|
| Web | Internet |
| Service | API |
| Web Service | An API that communicates over a network (typically the Internet) |

### Simple Definition

> A **Web Service** is an API that can be accessed over the Internet (or a network).

---

# Relationship Between APIs and Web Services

A common misconception is that APIs and Web Services are the same thing.

They are related, but not identical.

```text
All Web Services are APIs
✅ True

All APIs are Web Services
❌ False
```

---

## Visual Representation

```text
                APIs
      ┌─────────────────────┐
      │                     │
      │   Web Services      │
      │                     │
      └─────────────────────┘
```

A **Web Service** is simply a subset of APIs.

---

# Why Aren't All APIs Web Services?

An API does **not** necessarily need the Internet.

Consider these examples:

| Example | API? | Web Service? |
|----------|------|-------------|
| Python calling a library function | ✅ | ❌ |
| Java application using JDBC to talk to a database | ✅ | ❌ |
| Windows application calling operating system APIs | ✅ | ❌ |
| Application calling Google API over HTTPS | ✅ | ✅ |
| Mobile app calling a weather API over the Internet | ✅ | ✅ |

---

# Examples of Non-Web APIs

## Example 1: Python Library

```python
import math

math.sqrt(25)
```

Here:

- `math` exposes an API.
- No network is involved.
- No Internet is required.

Therefore:

```text
API          ✅
Web Service  ❌
```

---

## Example 2: Operating System APIs

```text
Application
      ↓
Windows API
      ↓
Operating System
```

Applications call operating system functions such as:

- File creation
- Memory allocation
- Process management

These are APIs, but no Internet communication occurs.

---

# Examples of Web Services

## Example 1: Google Search

```text
Browser
    ↓
Internet
    ↓
Google Search Service
    ↓
Response
```

Since the API is being accessed over the Internet:

```text
API          ✅
Web Service  ✅
```

---

## Example 2: Weather API

```text
Mobile App
      ↓
Internet
      ↓
Weather Service
      ↓
Weather Data
```

Again:

```text
API          ✅
Web Service  ✅
```

---

# How Web Services Work

A Web Service follows the same API flow:

```text
Request
   ↓
Program
   ↓
Response
```

The only difference is that the request travels across a network.

```text
Client
   ↓
Internet
   ↓
Web Service
   ↓
Program
   ↓
Response
   ↓
Client
```

---

# Data Formats Used by Web Services

When applications communicate over a network, they need a common language.

The most common formats are:

| Format | Description |
|----------|-------------|
| JSON | Lightweight and most commonly used today |
| XML | Older but still widely used in enterprise systems |

---

## Example JSON Response

```json
{
  "city": "Bangalore",
  "temperature": 27
}
```

---

## Example XML Response

```xml
<weather>
    <city>Bangalore</city>
    <temperature>27</temperature>
</weather>
```

Both formats represent the same information.

---

# Communication Styles Used by Web Services

Web Services need rules that define how requests and responses are exchanged.

Common approaches include:

| Technology | Description |
|------------|-------------|
| REST | Most popular modern approach |
| SOAP | XML-based enterprise standard |
| XML-RPC | Older remote procedure call protocol |

---

## REST Example

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

---

## SOAP Example

```xml
<soap:Envelope>
    ...
</soap:Envelope>
```

SOAP is more structured and commonly found in older enterprise systems.

---

# API vs Web Service

| Feature | API | Web Service |
|----------|------|-------------|
| Exposes functionality | ✅ | ✅ |
| Supports Request/Response | ✅ | ✅ |
| Requires network access | ❌ Not always | ✅ Yes |
| Uses Internet/HTTP | ❌ Optional | ✅ Usually |
| Can exist entirely within one machine | ✅ | ❌ |
| Uses JSON/XML | Sometimes | Usually |

---

# Mental Model

Think of it this way:

```text
API
│
├── Local API
│     ├── Python Library API
│     ├── Windows API
│     └── Database API
│
└── Web Service
      ├── Google API
      ├── Weather API
      ├── eBay API
      └── SAP Web API
```

---

# Key Takeaway

> **An API is any interface that allows one piece of software to interact with another.**

> **A Web Service is a special type of API that is exposed over a network (typically the Internet) and exchanges data using formats such as JSON or XML.**

### Remember

```text
All Web Services are APIs.

But not all APIs are Web Services.
```