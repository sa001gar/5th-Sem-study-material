# Topic 4: Software Engineering Paradigms

[< Prev: Software Engineering - Definition and Scope](topic-03.md) | [Index](index.md) | [Next: Knowledge Engineering Approach >](topic-05.md)

---

> A **software engineering paradigm** is a structured approach or model used to develop software. It defines how development progresses from **idea to delivery**. Think of it as a **roadmap** for building software.

> Different projects require different paradigms depending on **risk**, **complexity**, and **requirement stability**.

---

## 1. Why Paradigms Are Needed

Without a defined process:

- Teams work randomly
- Requirements keep changing
- No clarity of progress
- Deadlines missed
- Quality degrades

A paradigm provides: **Order**, **Defined Stages**, **Control**, **Predictability**

---

## 2. Major Software Engineering Paradigms

```mermaid
graph LR
    P["SE Paradigms"] --> W["1. Waterfall"]
    P --> PR["2. Prototyping"]
    P --> I["3. Incremental"]
    P --> S["4. Spiral"]
    P --> A["5. Agile"]

    style P fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style W fill:#336791,stroke:#1d3e5c,color:#fff
    style PR fill:#FF9F43,stroke:#cc7a2e,color:#fff
    style I fill:#1DD1A1,stroke:#14a37f,color:#000
    style S fill:#A259FF,stroke:#7033cc,color:#fff
    style A fill:#61DAFB,stroke:#21a1c9,color:#000
```

---

### 2.1 Waterfall Model

The **oldest and simplest** model. Follows a **linear sequence** -- you complete one phase fully before moving to the next.

```mermaid
graph TD
    R["Requirements"] --> D["Design"]
    D --> I["Implementation"]
    I --> T["Testing"]
    T --> DP["Deployment"]
    DP --> M["Maintenance"]

    style R fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style D fill:#5BA0E0,stroke:#3a7ab8,color:#fff
    style I fill:#6CB0E7,stroke:#4a8ac0,color:#fff
    style T fill:#7DC0EE,stroke:#5a9ac8,color:#fff
    style DP fill:#1DD1A1,stroke:#14a37f,color:#000
    style M fill:#FF9F43,stroke:#cc7a2e,color:#fff
```

#### Non-Technical Example

**Building a bridge** -- You finalize design, approve budget, construct, inspect, open. You **cannot** change the design after construction begins.

#### Software Example

**Government payroll system** with fixed rules -- requirements are **stable**, changes are **rare**. Waterfall works well.

| Advantages | Disadvantages |
|---|---|
| Simple to understand | No flexibility |
| Easy to manage | Late discovery of errors |
| Clear documentation | Not suitable for changing requirements |

---

### 2.2 Prototyping Model

First build a small **working model** (prototype). Client sees it, gives feedback, system refined.

```mermaid
graph TD
    R["Gather Requirements"] --> P["Build Prototype"]
    P --> F["Client Feedback"]
    F -->|"Not satisfied"| P
    F -->|"Satisfied"| D["Design Full System"]
    D --> I["Implement"]
    I --> T["Deliver Final Product"]

    style P fill:#FF9F43,stroke:#cc7a2e,color:#fff
    style F fill:#61DAFB,stroke:#21a1c9,color:#000
    style T fill:#1DD1A1,stroke:#14a37f,color:#000
```

#### Non-Technical Example

**Tailor stitching clothes** -- first makes rough trial version, adjusts fitting, then final product.

#### Software Example

**Building a startup app** -- create basic UI demo, show to users, validate idea, then build full system.

| Type | Description |
|---|---|
| **Throwaway** | Discarded after feedback is collected |
| **Evolutionary** | Refined iteratively into the final system |

---

### 2.3 Incremental Model

Software is built in **small parts** (increments). Each increment delivers some **working functionality**.

```mermaid
graph LR
    subgraph "Increment 1"
        R1["Req"] --> D1["Design"] --> I1["Build"] --> T1["Test"]
    end
    subgraph "Increment 2"
        R2["Req"] --> D2["Design"] --> I2["Build"] --> T2["Test"]
    end
    subgraph "Increment 3"
        R3["Req"] --> D3["Design"] --> I3["Build"] --> T3["Test"]
    end

    T1 --> V1["v1.0 - Core Features"]
    T2 --> V2["v2.0 - New Features"]
    T3 --> V3["v3.0 - More Features"]

    style V1 fill:#1DD1A1,stroke:#14a37f,color:#000
    style V2 fill:#1DD1A1,stroke:#14a37f,color:#000
    style V3 fill:#1DD1A1,stroke:#14a37f,color:#000
```

#### Non-Technical Example

**Building a house floor by floor** -- Ground floor complete and usable, first floor added, second floor added.

#### Software Example -- Instagram

| Version | Feature Added |
|---|---|
| v1.0 | Photo upload |
| v2.0 | Stories |
| v3.0 | Reels |
| v4.0 | Messaging |

| Advantages |
|---|
| Early delivery of usable product |
| Reduced risk |
| Flexible to changes |

---

### 2.4 Spiral Model

This model focuses on **risk analysis**. Each cycle involves four phases. It is **iterative** like a spiral.

```mermaid
graph TD
    P["1. Planning"] --> RA["2. Risk Analysis"]
    RA --> E["3. Engineering"]
    E --> EV["4. Evaluation"]
    EV -->|"Next Iteration"| P

    style P fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style RA fill:#FF6B6B,stroke:#c94444,color:#fff
    style E fill:#1DD1A1,stroke:#14a37f,color:#000
    style EV fill:#FF9F43,stroke:#cc7a2e,color:#fff
```

#### When Used?

For **large, complex, high-risk systems**:

| System Type | Why Spiral? |
|---|---|
| Banking Software | Security and financial risk |
| Defense Systems | Mission-critical reliability |
| Air Traffic Control | Safety-critical, zero tolerance |

---

### 2.5 Agile Model

**Modern and widely used.** Key principles:

- Small iterations (**sprints**)
- Continuous customer feedback
- **Working software** over documentation
- **Embrace change**

```mermaid
graph LR
    PB["Product Backlog"] --> S1["Sprint 1 - Login System"]
    S1 --> R1["Review and Feedback"]
    R1 --> S2["Sprint 2 - Dashboard"]
    S2 --> R2["Review and Feedback"]
    R2 --> S3["Sprint 3 - Payments"]
    S3 --> R3["Review and Feedback"]
    R3 --> D["Continuous Delivery"]

    style PB fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style S1 fill:#61DAFB,stroke:#21a1c9,color:#000
    style S2 fill:#61DAFB,stroke:#21a1c9,color:#000
    style S3 fill:#61DAFB,stroke:#21a1c9,color:#000
    style D fill:#1DD1A1,stroke:#14a37f,color:#000
```

#### Non-Technical Example

**Building a startup product** -- instead of planning everything for 1 year: Release MVP in 2 weeks, get feedback, improve, repeat.

---

## 3. Comparison Summary

| Paradigm | Approach | Flexibility | Best For |
|---|---|---|---|
| **Waterfall** | Sequential | Rigid | Stable requirements |
| **Prototyping** | Build, Feedback, Refine | Moderate | Unclear requirements |
| **Incremental** | Feature-based delivery | Flexible | Evolving products |
| **Spiral** | Risk-driven cycles | High | Complex, high-risk systems |
| **Agile** | Iterative sprints | Very High | Customer-driven, fast-moving |

---

## 4. Important Insight

> **Choosing the wrong paradigm leads to project failure.**

| Scenario | Result |
|---|---|
| Using **Waterfall** for a startup with changing requirements | Disaster |
| Using **Agile** for nuclear defense software | Risky |

> **Paradigm must match project nature.**

---

[< Prev: Software Engineering - Definition and Scope](topic-03.md) | [Index](index.md) | [Next: Knowledge Engineering Approach >](topic-05.md)