# Topic 50: Algorithmic Cost Models (COCOMO, Putnam-Slim, Watson, Felix)

[< Prev: Cost Estimation Issues and Rayleigh Curve](topic-49.md) | [Index](index.md) | [Next: Software Maintenance Concepts >](topic-51.md)

---

> **Algorithmic cost models** use mathematical formulas and historical data to estimate effort, development time, and cost systematically.

---

## 1. COCOMO Model

The **Constructive Cost Model** by Barry Boehm (1981). Most widely used estimation model.

```
Effort = a x (KLOC)^b
```

Where: Effort = person-months, KLOC = thousands of lines of code, a and b = constants based on project type.

### Project Types in COCOMO

| Type | Description | Example |
|---|---|---|
| **Organic** | Small, simple, familiar technology | Business management app |
| **Semi-Detached** | Medium complexity, mixed experience | Large web application |
| **Embedded** | Highly complex, strict requirements | Aircraft control systems |

---

## 2. Putnam-Slim Model

Based on **Rayleigh distribution** of effort over time.

> Key idea: Compressing schedule **dramatically increases** required effort.

---

## 3. Watson and Felix Models

Developed from **IBM research** using historical project data.

| Model | Based On |
|---|---|
| Watson | IBM project data, program size |
| Felix | Empirical data from large systems |

---

## 4. Advantages

| Advantage |
|---|
| Systematic, repeatable estimation |
| Predict cost and duration |
| Plan resources effectively |
| Reduce reliance on guesswork |

---

## 5. Limitations

| Limitation |
|---|
| Depend on correct input data |
| Requirement changes may invalidate estimates |
| Human factors hard to measure precisely |

> Often combined with **expert judgment**.

---

## 6. Key Insight

> Algorithmic models transform estimation from guesswork into a **structured, data-driven process**. They help organizations estimate cost, time, and resources more accurately.

---

[< Prev: Cost Estimation Issues and Rayleigh Curve](topic-49.md) | [Index](index.md) | [Next: Software Maintenance Concepts >](topic-51.md)