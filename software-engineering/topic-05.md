# Topic 5: Knowledge Engineering Approach

[< Prev: Software Engineering Paradigms](topic-04.md) | [Index](index.md) | [Next: End User Development >](topic-06.md)

---

> Now we move slightly into **AI-related thinking**. Knowledge Engineering is about building systems that **simulate human expertise**.

---

## 1. What is Knowledge Engineering?

Knowledge Engineering is the process of:

1. **Collecting** knowledge from domain experts
2. **Structuring** that knowledge
3. **Encoding** it into a computer system
4. **Creating** a system that can make decisions like an expert

> It is mainly used in **Expert Systems** and **AI-based systems**.

---

## 2. How It Is Different from Normal Software

| Aspect | Normal Software | Knowledge-Based Software |
|---|---|---|
| **Logic** | Fixed, algorithmic | Rule-based |
| **Data** | Static data | Facts + Rules |
| **Processing** | Sequential execution | **Inference** (reasoning) |
| **Behavior** | Deterministic | Simulates **expert reasoning** |

---

## 3. Simple Real-Life Example (Non-Technical)

**Doctor diagnosing a disease:**

| Symptoms | Diagnosis |
|---|---|
| Fever + Cough + Chest Pain | Possible **Pneumonia** |
| High Sugar Level | **Diabetes** risk |

A knowledge engineering system **captures such rules**:

```
IF fever AND cough AND chest_pain
THEN pneumonia_probability = HIGH
```

> Now the software can behave like a **medical advisor**.

---

## 4. Technical Example

### Fraud Detection System

| Approach | Method |
|---|---|
| **Traditional** | Write fixed logic rules manually |
| **Knowledge Engineering** | Collect expert banking fraud patterns and encode them |

#### Encoded Rule Example:

```
IF transaction_amount > 50,000
AND location != usual_location
AND time = midnight
THEN fraud_risk = HIGH
```

```mermaid
graph LR
    TX["New Transaction"] --> IE["Inference Engine"]
    KB["Knowledge Base -- Rules and Facts"] --> IE
    IE --> D{"Decision"}
    D -->|"fraud_risk = HIGH"| A["Alert and Block"]
    D -->|"fraud_risk = LOW"| P["Approve"]

    style TX fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style KB fill:#A259FF,stroke:#7033cc,color:#fff
    style IE fill:#FF9F43,stroke:#cc7a2e,color:#fff
    style A fill:#FF6B6B,stroke:#c94444,color:#fff
    style P fill:#1DD1A1,stroke:#14a37f,color:#000
```

---

## 5. Components of a Knowledge Engineering System

```mermaid
graph TD
    KES["Knowledge Engineering System"] --> KB["Knowledge Base"]
    KES --> IE["Inference Engine"]
    KES --> UI["User Interface"]
    KES --> EF["Explanation Facility"]

    style KES fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style KB fill:#A259FF,stroke:#7033cc,color:#fff
    style IE fill:#FF9F43,stroke:#cc7a2e,color:#fff
    style UI fill:#61DAFB,stroke:#21a1c9,color:#000
    style EF fill:#1DD1A1,stroke:#14a37f,color:#000
```

| Component | Role |
|---|---|
| **Knowledge Base** | Stores rules and facts |
| **Inference Engine** | Applies rules to facts to derive conclusions |
| **User Interface** | Allows user interaction |
| **Explanation Facility** | Explains *why* a particular conclusion was reached |

---

## 6. Process of Knowledge Engineering

```mermaid
graph TD
    A["1. Knowledge Acquisition -- Interview experts"] --> B["2. Knowledge Representation -- Convert into formal structures"]
    B --> C["3. Implementation -- Build system using rule engines"]
    C --> D["4. Testing and Validation -- Compare with expert decisions"]

    style A fill:#4A90D9,stroke:#2C5F8A,color:#fff
    style B fill:#A259FF,stroke:#7033cc,color:#fff
    style C fill:#FF9F43,stroke:#cc7a2e,color:#fff
    style D fill:#1DD1A1,stroke:#14a37f,color:#000
```

### Knowledge Representation Methods

| Method | Description |
|---|---|
| **IF-THEN Rules** | `IF condition THEN action` |
| **Semantic Networks** | Graph of related concepts |
| **Frames** | Structured data templates |
| **Logic Expressions** | Formal logical statements |

---

## 7. Where It Is Used

| Domain | Example |
|---|---|
| Medical | Diagnosis systems |
| Legal | Legal advisory systems |
| Customer Service | Chatbots |
| Finance | Financial risk assessment |
| Configuration | PC builder suggestions |

---

## 8. Real Industry Examples

| Era | System | Description |
|---|---|---|
| **Early (1970s)** | MYCIN | Medical expert system for bacterial infections |
| **Modern** | AI Credit Scoring | Automated loan approval decisions |
| **Modern** | Support Bots | Automated customer support using knowledge rules |

---

## 9. Why It Matters in Software Engineering

Knowledge engineering is used when:

- The problem requires **expert decision-making**
- The domain is **rule-based**
- Expertise must be **preserved digitally**

> Instead of hardcoding everything, we **separate knowledge from processing logic**.

---

## 10. Difference from Traditional Software

```mermaid
graph LR
    subgraph "Traditional Software"
        C1["Code with logic embedded inside"]
    end

    subgraph "Knowledge Engineering"
        KB2["Knowledge Base -- Rules and Facts"] --- IE2["Inference Engine -- Reasoning Logic"]
    end

    style C1 fill:#FF6B6B,stroke:#c94444,color:#fff
    style KB2 fill:#A259FF,stroke:#7033cc,color:#fff
    style IE2 fill:#1DD1A1,stroke:#14a37f,color:#000
```

| Aspect | Traditional | Knowledge Engineering |
|---|---|---|
| **Logic Location** | Embedded in code | Stored separately in knowledge base |
| **Updating** | Rewrite code | Change rule -- no program rewrite |
| **Flexibility** | Low | High |

> Separating knowledge from logic makes **updating rules much easier** -- just change the rule, no need to rewrite the entire program.

---

[< Prev: Software Engineering Paradigms](topic-04.md) | [Index](index.md) | [Next: End User Development >](topic-06.md)