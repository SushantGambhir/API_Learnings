# What is an API? Exercise 1

## Exercise

For each API example, determine:

- **A (Application)** → What software is running the program?
- **P (Program)** → What task is being performed?
- **I (Interface)** → From where are you telling the program to run?

### API Definition

> An API exists when you tell an **Interface (I)** to run a **Program (P)** inside an **Application (A)**.

---

## Reference Questions

### Interface (I)
**From where are you telling the program to run?**

### Program (P)
**What task is being performed? What does the program do?**

### Application (A)
**Which software/application contains the program being run?**

---

## Examples

| Difficulty | Example | Interface (I) | Program (P) | Application (A) |
|------------|----------|---------------|-------------|-----------------|
| Simple | Send a Whatsapp message using a cell phone | Android / iPhone | Messaging | Whatsapp |
| Simple | Perform a Google search using a computer | Windows / Mac / Linux Distro | Search | Google |
| Moderate / Complex | Create orders in Amazon automatically when orders are received (no browser involved) | Amazon API | Create Order | Amazon |
| Moderate / Complex | Create orders in SAP automatically when orders are received (no browser involved) | SAP API | Create Order | SAP |

---

## Key Observation

### Simple Examples

In these examples, a **human** interacts with the application through a device:

```text
Person → Device → Application → Program
```

Examples:

- Cell Phone → Viber → Messaging
- Computer → Google → Search

### Moderate / Complex Examples

In these examples, one **software system talks directly to another software system**:

```text
Application → API → Program → Application
```

Examples:

- Order System → Amazon API → Create Order → Amazon
- Order System → SAP API → Create Order → SAP

---

## Important

> When people talk about **APIs** in software engineering, they are usually referring to the **Moderate / Complex** scenarios where one application communicates directly with another application without a human using a browser or user interface.

### Mental Model

```text
Interface (I)
      ↓
Program (P)
      ↓
Application (A)
```

Or simply:

```text
Tell (I) a Program (P) to run in an Application (A)
```