# Topic 40: Coding Standards

[< Prev: Re-engineering Legacy Systems](topic-39.md) | [Index](index.md) | [Next: Software Quality Assurance >](topic-41.md)

---

> When multiple developers work on the same system, code must follow a **consistent structure and style**. Coding standards define rules and guidelines for writing readable, maintainable, and consistent code.

---

## 1. Why Coding Standards are Important

| Without Standards | With Standards |
|---|---|
| Each developer writes differently | Consistent code style |
| Confusion and miscommunication | Easy to read and understand |
| Hard to maintain | Simpler maintenance |

---

## 2. Common Coding Standard Guidelines

### Naming Conventions

| Bad | Good |
|---|---|
| `x` | `totalPrice` |
| `fn1` | `calculateDiscount` |

### Code Formatting

```
if (userLoggedIn) {
    displayDashboard();
}
```

> Proper indentation, consistent spacing, clear structure.

### Comments and Documentation

```python
# Calculate total price including tax
total_price = price + (price * tax_rate)
```

### Error Handling

Instead of ignoring errors, use proper exception handling mechanisms.

### Code Modularity

Instead of one large function with hundreds of lines, create **multiple smaller functions** for specific tasks.

---

## 3. Real Industry Example

| Company/Standard | Language |
|---|---|
| PEP 8 | Python |
| Google Java Style | Java |
| Airbnb Style Guide | JavaScript |

> These standards ensure thousands of developers can work on the **same codebase** efficiently.

---

## 4. Benefits of Coding Standards

| Benefit |
|---|
| Improve code readability |
| Reduce programming errors |
| Easier onboarding for new developers |
| Simplify maintenance and debugging |

---

## 5. Key Insight

> Software is rarely written once and forgotten. It **evolves continuously**. Coding standards ensure software remains understandable and maintainable even as teams change and systems grow.

---

[< Prev: Re-engineering Legacy Systems](topic-39.md) | [Index](index.md) | [Next: Software Quality Assurance >](topic-41.md)