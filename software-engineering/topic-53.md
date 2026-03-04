# Topic 53: Work Breakdown Structure (WBS)

[< Prev: Planning Software Projects](topic-52.md) | [Index](index.md) | [Next: Integrating Design and Planning >](topic-54.md)

---

> Large projects are divided into **smaller, manageable parts**. This structured decomposition is called a **Work Breakdown Structure (WBS)**.

---

## 1. WBS Hierarchy

```
Large Project --> Phases --> Tasks --> Subtasks
```

```mermaid
graph TD
    P["Online Learning Platform"] --> RA["Requirement Analysis"]
    P --> SD["System Design"]
    P --> DEV["Development"]
    P --> TEST["Testing"]
    P --> DEP["Deployment"]

    RA --> RA1["Gather requirements"]
    RA --> RA2["Define specifications"]

    SD --> SD1["System architecture"]
    SD --> SD2["Database design"]
    SD --> SD3["UI design"]

    DEV --> DEV1["Backend"]
    DEV --> DEV2["Frontend"]
    DEV --> DEV3["API integration"]

    TEST --> TEST1["Unit testing"]
    TEST --> TEST2["Integration testing"]
    TEST --> TEST3["System testing"]

    DEP --> DEP1["Server setup"]
    DEP --> DEP2["App deployment"]
    DEP --> DEP3["User training"]

    style P fill:#4A90D9,stroke:#2C5F8A,color:#fff
```

---

## 2. Purpose of WBS

| Purpose |
|---|
| Organize project tasks clearly |
| Estimate effort more accurately |
| Assign responsibilities to team members |
| Track progress and manage deadlines |
| Control project scope |

---

## 3. Benefits

| Benefit |
|---|
| Simplifies project management |
| Improves task assignment and accountability |
| Better cost and time estimation |
| Reduces risk of missing tasks |

---

## 4. Tools for WBS

| Tool |
|---|
| Jira |
| Microsoft Project |
| Asana |

---

## 5. Key Insight

> Complex projects become manageable when broken into **smaller, well-defined tasks**. WBS provides a systematic way to organize and control all aspects of a project.

---

[< Prev: Planning Software Projects](topic-52.md) | [Index](index.md) | [Next: Integrating Design and Planning >](topic-54.md)