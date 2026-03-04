# Topic 49: Issues in Software Cost Estimation and the Rayleigh Curve

[< Prev: Function Point Analysis](topic-48.md) | [Index](index.md) | [Next: Algorithmic Cost Models >](topic-50.md)

---

> Estimating cost and time for software projects is one of the **most difficult tasks** in SE. The **Rayleigh Curve** models how effort is distributed over the project lifecycle.

---

## 1. Issues in Cost Estimation

| Issue | Description |
|---|---|
| **Changing Requirements** | New features increase complexity and cost |
| **Unclear Requirements** | Incomplete info leads to redesign |
| **System Complexity** | Multiple modules, algorithms, integrations |
| **Human Factors** | Developer skill variations |
| **Technology Uncertainty** | New frameworks need learning time |

---

## 2. The Rayleigh Curve

Shows how **effort changes over time** during a project.

```mermaid
graph LR
    S["Start: Low effort"] --> M["Mid: Peak effort"]
    M --> E["End: Declining effort"]

    style S fill:#61DAFB,stroke:#21a1c9,color:#000
    style M fill:#FF6B6B,stroke:#c94444,color:#fff
    style E fill:#1DD1A1,stroke:#14a37f,color:#000
```

| Phase | Effort Level | Activity |
|---|---|---|
| **Beginning** | Low | Planning, requirement analysis |
| **Middle** | Peak | Active coding, testing |
| **End** | Declining | Maintenance, final adjustments |

---

## 3. Importance of the Rayleigh Curve

| Purpose |
|---|
| Understand how effort changes during development |
| Allocate resources effectively |
| Predict the peak development phase |
| Plan project schedules more accurately |

---

## 4. Key Insight

> Development effort does **not remain constant**. It increases, peaks, then decreases. Understanding this pattern helps managers make better **resource allocation** and scheduling decisions.

---

[< Prev: Function Point Analysis](topic-48.md) | [Index](index.md) | [Next: Algorithmic Cost Models >](topic-50.md)