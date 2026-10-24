# How an API Flow Works

## Core Idea

An API allows a **request** to trigger a **program** inside an **application**, which then returns a **response**.

```text
Request
   ↓
Program
   ↓
Response
```

Or using our API model:

```text
Interface (I)
      ↓
Program (P)
      ↓
Application (A)
      ↓
Response
```

---

# Example 1: Google Search

Most people use APIs every day without realizing it.

Suppose you search for:

```text
"What is an API?"
```

in Google.

## Identify A, P, and I

| Component | Value |
|------------|---------|
| I (Interface) | Web browser on your computer or phone |
| P (Program) | Search program |
| A (Application) | Google |

---

## Step-by-Step Flow

### Step 1: User Creates a Request

You type:

```text
What is an API?
```

into Google's search box and press Enter.

```text
You
 ↓
Google Search Box
```

The browser sends a request to Google.

---

### Step 2: The Request Reaches Google

```text
Browser
   ↓
Google
```

Google receives the request and determines which program must run.

In this case:

```text
Run Search Program
```

---

### Step 3: Program Executes

Google's search program:

1. Looks through Google's index.
2. Finds relevant web pages.
3. Ranks the results.
4. Prepares an answer.

```text
Request
   ↓
Search Program
   ↓
Find Results
```

---

### Step 4: Response Is Generated

The search program returns:

```text
- Link 1
- Link 2
- Link 3
- Featured snippets
- Images
```

This becomes the response.

```text
Search Program
      ↓
Response
```

---

### Step 5: Response Returns to User

```text
You
 ↓
Browser
 ↓
Google Search
 ↓
Search Program
 ↓
Results
 ↓
Browser
 ↓
You
```

---

## Complete Flow

```text
User
 ↓
Browser (Interface)
 ↓
Google (Application)
 ↓
Search Program
 ↓
Response
 ↓
Browser
 ↓
User
```

---

## Important Observation

Even though you see a webpage, the browser is really acting as the **Interface (I)** that tells Google's **Search Program (P)** to run inside Google's **Application (A)**.

---

# What Changes in a Real API?

In the Google example:

```text
Human → Browser → Google
```

A human is involved.

In many business systems, there is **no human involved at all**.

Instead:

```text
Application → API → Application
```

One software system talks directly to another software system.

---

# Example 2: eBay Order Creation (API Directly Invoked)

Imagine an online store receives a new order.

The store wants to automatically create the same order in eBay.

No person logs in.

No browser is opened.

Everything happens automatically.

---

## Identify A, P, and I

| Component | Value |
|------------|---------|
| I (Interface) | eBay API |
| P (Program) | Create Order |
| A (Application) | eBay |

Notice that the interface is no longer a browser.

The interface is now the **API itself**.

---

## Step-by-Step Flow

### Step 1: Order Created

An order arrives in another application.

```text
Order System
     ↓
New Order
```

---

### Step 2: API Request Sent

The order system sends a request.

```json
{
  "customer": "John",
  "product": "Laptop",
  "quantity": 1
}
```

```text
Order System
      ↓
eBay API Request
```

---

### Step 3: API Receives Request

The eBay API receives the request.

Think of the API as a special doorway into eBay.

```text
Order System
      ↓
eBay API
```

---

### Step 4: Program Executes

The API tells the Create Order program to run.

```text
Request
   ↓
Create Order Program
```

The program:

- Validates data
- Creates the order
- Stores it in eBay

---

### Step 5: Response Generated

eBay returns:

```json
{
  "orderId": 12345,
  "status": "Created"
}
```

---

### Step 6: Response Returned

```text
eBay
  ↓
Response
  ↓
Order System
```

The order system now knows the order was successfully created.

---

# Complete API Flow

```text
Order System
     ↓
API Request
     ↓
eBay API (Interface)
     ↓
Create Order Program
     ↓
eBay Application
     ↓
Response
     ↓
Order System
```

---

# Comparing the Two Scenarios

| Component | Google Search | eBay API |
|------------|------------|-----------|
| Interface (I) | Browser | API |
| Program (P) | Search | Create Order |
| Application (A) | Google | eBay |
| Triggered By | Human | Another Application |
| Browser Required? | Yes | No |
| Typical Users | Consumers | Software Systems |

---

# The Big Insight

Most beginners think:

```text
API = Request + Response
```

While technically true, a better mental model is:

```text
Request
   ↓
API (Interface)
   ↓
Program
   ↓
Application
   ↓
Response
```

The API itself usually does **not** perform the business work.

Its primary responsibility is to:

1. Receive requests.
2. Validate requests.
3. Call the correct program.
4. Return the response.

The actual work is performed by the **Program (P)** running inside the **Application (A)**.

---

## Final Mental Model

```text
Simple Scenario

Human
  ↓
Browser (I)
  ↓
Program (P)
  ↓
Application (A)
  ↓
Response


Moderate/Complex Scenario

Application
      ↓
API (I)
      ↓
Program (P)
      ↓
Application (A)
      ↓
Response
```

> **An API is simply an Interface (I) that allows a Request to trigger a Program (P) inside an Application (A) and receive a Response back.**