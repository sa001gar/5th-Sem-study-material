# Topic 15: Specification Tools

[< Prev: Formal Specification Methods](topic-14.md) | [Index](index.md) | [Next: Flow-Based Analysis (DFD) >](topic-16.md)

---

> After understanding formal specification methods, now we look at **practical tools** used to describe and model system requirements. Specification tools help represent system requirements clearly using **diagrams and structured representations** instead of only text.

---

## 1. What Are Specification Tools?

Specification tools are techniques or modeling tools used to describe:

- System functionality
- Data flow
- Data structure
- Object interactions
- System behavior

> They make requirements **visual** and **structured**.

---

## 2. Why Specification Tools Are Important

Plain text requirements can:

| Problem |
|---|
| Be misunderstood |
| Miss relationships |
| Hide logical gaps |

Diagrams make structure **visible**. They show:
- How data moves
- Which module depends on which
- What triggers what

> This clarity **prevents design mistakes**.

---

## 3. Major Specification Tools

```mermaid
graph TD
    ST["Specification Tools"] --> DFD["Data Flow Diagrams"]
    ST --> ERD["ER Diagrams"]
    ST --> DT["Decision Tables"]
    ST --> DTR["Decision Trees"]
    ST --> SE["Structured English"]
    ST --> UCD["Use Case Diagrams"]

    style ST fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style DFD fill:#61DAFB,stroke:#21a1c9,color:#000
    style ERD fill:#FF9F43,stroke:#cc7a2e,color:#fff
    style DT fill:#1DD1A1,stroke:#14a37f,color:#000
    style DTR fill:#A259FF,stroke:#7033cc,color:#fff
    style SE fill:#FF6B6B,stroke:#c94444,color:#fff
    style UCD fill:#F7DF1E,stroke:#c4b018,color:#000
```

---

## 4. Data Flow Diagram (DFD)

Shows how **data moves** through the system.

**Components:** Process, Data Store, External Entity, Data Flow

**Example (Online Exam System):**

```mermaid
graph LR
    S["Student"] --> LP["Login Process"]
    LP --> DB["Database"]
    DB --> RD["Result Display"]
    RD --> S

    style S fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style DB fill:#A259FF,stroke:#7033cc,color:#fff
    style RD fill:#1DD1A1,stroke:#14a37f,color:#000
```

> DFD focuses on **data movement**, not control logic.

---

## 5. Entity-Relationship (ER) Diagram

Shows how **data entities** relate to each other.

```mermaid
erDiagram
    STUDENT ||--o{ ENROLLMENT : "enrolls in"
    COURSE ||--o{ ENROLLMENT : "has"
    TEACHER ||--o{ COURSE : "teaches"
```

> Used to design **database structure**.

---

## 6. Decision Tables

Used when system behavior depends on **multiple conditions**.

**Example:**

| User is Admin | Payment Successful | Account Active | Action |
|---|---|---|---|
| Yes | Yes | Yes | **Grant Access** |
| Yes | Yes | No | Deny Access |
| No | Yes | Yes | Limited Access |
| No | No | Yes | Deny Access |

> Decision table organizes **all combinations** clearly.

---

## 7. Decision Trees

Graphical representation of **conditional logic**.

```mermaid
graph TD
    Q1{"Is user logged in?"}
    Q1 -->|"Yes"| Q2{"Check subscription"}
    Q1 -->|"No"| A1["Redirect to login"]
    Q2 -->|"Active"| A2["Grant full access"]
    Q2 -->|"Expired"| A3["Show renewal prompt"]

    style Q1 fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style A2 fill:#1DD1A1,stroke:#14a37f,color:#000
    style A1 fill:#FF6B6B,stroke:#c94444,color:#fff
    style A3 fill:#FF9F43,stroke:#cc7a2e,color:#fff
```

> Useful for modeling **business rules**.

---

## 8. Structured English

Uses controlled English language to specify logic clearly.

```
IF attendance < 75%
    THEN mark student as "Short Attendance"
    ELSE allow exam registration
```

> More structured than plain English.

---

## 9. Use Case Diagrams

Used in **Object-Oriented Analysis**. Shows:

- **Actors** (users)
- **Use cases** (system functions)

**Example:**

| Actor | Use Cases |
|---|---|
| Student | Login, View Results, Pay Fees |
| Teacher | Upload Marks, View Attendance |
| Admin | Manage Users, Generate Reports |

> Focuses on **user interaction**.

---

## 10. Real Industry Example

When building a large ERP:

| Tool | Purpose |
|---|---|
| DFD | Show data movement |
| ER Diagram | Database design |
| Use Case Diagram | User interaction |
| Decision Tables | Complex business logic |

> Each tool provides a **different projection** of the system.

---

## 11. Important Insight

Specification tools:

| Benefit |
|---|
| Reduce ambiguity |
| Improve communication |
| Detect missing logic |
| Support structured thinking |

> They **bridge the gap** between system analysis and system design.

---

[< Prev: Formal Specification Methods](topic-14.md) | [Index](index.md) | [Next: Flow-Based Analysis (DFD) >](topic-16.md)