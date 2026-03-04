# Topic 11: Systems Specification

[< Prev: Projection](topic-10.md) | [Index](index.md) | [Next: Software Requirements Specification >](topic-12.md)

---

> After analyzing a system using abstraction, partitioning, and projection, we must **formally describe** what the system is supposed to do. That formal description is called **System Specification**.

---

## 1. What is Systems Specification?

System Specification is a detailed, structured description of:

- **What** the system should do
- **What constraints** it must follow
- **What performance level** is expected
- **How it interacts** with users and other systems

It defines the system clearly **before** design and coding begin.

> It answers: **"What exactly are we building?"**

---

## 2. Simple Real-Life Example (Non-Technical)

### School Bus Tracking System

| Approach | Actions |
|---|---|
| **Without specification** | You just build a tracking app |
| **With specification** | You define precise requirements |

**Specification details:**

| Requirement | Description |
|---|---|
| Parents can see live bus location | Real-time GPS tracking |
| Admin can assign buses to routes | Route management |
| Drivers must log in before starting trip | Authentication |
| System updates location every 10 seconds | Update frequency |
| Alerts sent if bus deviates from route | Deviation notification |
| Data stored for 30 days | Data retention |

> Now expectations are **clear**.

---

## 3. Technical Example (CS Perspective)

### Online Exam System

```mermaid
graph TD
    SPEC["System Specification"] --> FR["Functional Requirements"]
    SPEC --> NFR["Non-Functional Requirements"]
    SPEC --> CON["Constraints"]

    FR --> F1["Students can log in"]
    FR --> F2["Timer auto-submits exam"]
    FR --> F3["Auto-evaluation for MCQs"]
    FR --> F4["Results generated instantly"]

    NFR --> N1["Support 5,000 concurrent users"]
    NFR --> N2["Response time less than 2 seconds"]
    NFR --> N3["Data encrypted"]
    NFR --> N4["99.9% uptime"]

    CON --> C1["Must run on college server"]
    CON --> C2["Must use MySQL"]

    style SPEC fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style FR fill:#1DD1A1,stroke:#14a37f,color:#000
    style NFR fill:#FF9F43,stroke:#cc7a2e,color:#fff
    style CON fill:#FF6B6B,stroke:#c94444,color:#fff
```

> Now the development team has **clear boundaries**.

---

## 4. What Does System Specification Contain?

| Section | Description |
|---|---|
| **Functional Requirements** | What system must do |
| **Non-Functional Requirements** | Performance, security, scalability |
| **Constraints** | Budget, platform, technology limitations |
| **Interfaces** | User interface, External system interfaces, APIs |
| **Data Requirements** | What data must be stored and processed |

---

## 5. Why Systems Specification is Important

Without it:

| Problem | Impact |
|---|---|
| Client-developer miscommunication | Wrong system built |
| Scope keeps changing | Feature creep |
| Features added without control | Budget increases |
| No clear agreement | Deadlines break |

> Specification creates **agreement** between client and developer. It acts like a **contract**.

---

## 6. Difference Between System Analysis and System Specification

| Aspect | System Analysis | System Specification |
|---|---|---|
| **Purpose** | Understand the problem | Write formal description of solution |
| **Activity** | Study existing system, identify needs | Document requirements precisely |
| **Nature** | Thinking | Documenting |

```mermaid
graph LR
    SA["System Analysis -- Thinking"] --> SS["System Specification -- Documenting"]
    SS --> DD["Design and Development"]

    style SA fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style SS fill:#FF9F43,stroke:#cc7a2e,color:#fff
    style DD fill:#1DD1A1,stroke:#14a37f,color:#000
```

---

## 7. Real Industry Example

Large companies like banking institutions do **not** start coding immediately. They prepare:

| Document | Purpose |
|---|---|
| Requirement documents | Define what to build |
| Architecture documents | Define how to build |
| Compliance specifications | Meet regulatory standards |
| Security specifications | Protect data and systems |

> Only after approval does development begin.

---

## 8. Important Insight

> If system specification is weak, even the **best programmers** will **build the wrong system correctly**.

Good specification reduces:

| Factor |
|---|
| Risk |
| Rework |
| Conflict |
| Cost |

---

[< Prev: Projection](topic-10.md) | [Index](index.md) | [Next: Software Requirements Specification >](topic-12.md)