# Invocation Framework — Quick Start Guide  
Version: 0.1  
Maintainer: Imvara  
Last Updated: 2025-12-01  

Welcome to the **Invocation Framework Quick Start**.  
This guide gives you a fast, clear, implementation-ready understanding of how Invocation works and how to begin building Invocation-compliant systems.

If you read only one document before diving deeper, it should be this one.

---

# 1. What Is Invocation?

Invocation is the structured, deterministic process of transforming natural-language queries into **validated, explainable, machine-actionable decisions**.

Invocation replaces stochastic LLM reasoning with a governed pipeline:

```text
Intent
  → Entities
  → Signals
  → Decision Pathway
  → Validated Output (Invocation Protocol v0.1)
```

Invocation ensures:

- Determinism  
- Transparency  
- Safety  
- Interoperability  
- Reproducibility  

Same inputs → same outputs → same explanations.

---

# 2. Invocation Architecture (Quick Overview)

Invocation systems follow a **five-stage pipeline**:

1. **Intent Interpreter**  
   Extracts domain, intent, constraints, and referenced entities.

2. **Entity Binder**  
   Maps detected entities to canonical schemas.

3. **Signal Resolver**  
   Fetches all signals needed to evaluate entities.

4. **Decision Pathway Engine**  
   Executes deterministic decision logic (weighted scoring, elimination, utility models).

5. **Output Validator**  
   Ensures the result conforms to the Invocation Protocol v0.1.

The full pipeline is defined in `spec-architecture.md`.

---

# 3. Example: Quick Invocation Flow

Example user query:

> “Best protein powder for muscle gain under $50?”

Behind the scenes, an Invocation-compliant system would produce:

### **Step 1 — Intent Interpretation**

```json
{
  "domain": "retail",
  "intent_type": "product_comparison",
  "constraints": { "budget_max": 50 },
  "detected_entities": ["Product"]
}
```

### **Step 2 — Entity Binding**

```json
{
  "entity_class": "Product",
  "candidate_entities": ["protein_powder_1", "protein_powder_2"]
}
```

### **Step 3 — Signal Resolution**

```json
{
  "protein_per_serving": 24,
  "rating_score": 4.7,
  "price_per_serving": 1.10,
  "ingredient_purity": 0.92
}
```

### **Step 4 — Decision Pathway Execution**

Uses a weighted scoring model defined in the schema registry.

### **Step 5 — Validated Output**

```json
{
  "decision_pathway_used": "retail.product_comparison.v1",
  "entities_evaluated": ["protein_powder_1", "protein_powder_2"],
  "signals_used": ["protein_per_serving", "rating_score", "price_per_serving"],
  "ranked_results": [
    { "id": "protein_powder_1", "score": 0.91 }
  ],
  "explanation_available": true,
  "version": "0.1"
}
```

This is the Invocation Protocol v0.1 output.

---

# 4. What You Need to Implement Invocation

To implement Invocation, your system must:

### **1. Understand Schemas**
Schemas define:

- Entities  
- Signals  
- Products  
- Services  
- Decision pathways  

See: `/specs/schemas/`.

### **2. Implement the Invocation Architecture**
Defined in: `spec-architecture.md`.

### **3. Use Pathways for Decisions**
Pathways define deterministic logic models.

See: `spec-pathways.md`.

### **4. Validate Outputs**
All Invocation outputs must pass:

- Schema validation  
- Signal validation  
- Pathway validation  
- Safety validation  
- Output protocol checks  

See: `spec-validation.md`.

### **5. Follow Governance Rules**
Versioning, proposals, deprecations, and release cadence.

See: `spec-governance.md`.

---

# 5. Minimal Example Implementation (Pseudocode)

### **Step 1 — Parse Intent**

```python
intent = interpret_intent(user_query)
```

### **Step 2 — Bind Entities**

```python
entities = bind_entities(intent)
```

### **Step 3 — Resolve Signals**

```python
signals = resolve_signals(entities)
```

### **Step 4 — Execute Pathway**

```python
result = execute_pathway(intent, entities, signals)
```

### **Step 5 — Validate Output**

```python
validated = validate_output(result)
```

If validation passes:  
→ Return the Invocation Protocol output.  
If not:  
→ Return a structured error.

---

# 6. Directory Map (Where Everything Lives)

```
docs/
  quickstart.md          ← you are here
  spec-index.md
  spec-architecture.md
  spec-pathways.md
  spec-validation.md
  spec-governance.md

specs/
  schemas/
  definitions/
  examples/
  diagnostics/
  invocation-protocol/
  invocation-os/
```

---

# 7. Suggested Next Steps

### **If you want to learn the architecture:**  
Read `spec-architecture.md`.

### **If you want to implement a pathway:**  
Read `spec-pathways.md` and the examples in `/specs/examples/`.

### **If you want to claim compliance:**  
Read `spec-validation.md`.

### **If you want to propose changes:**  
Open an IGP via `/CONTRIBUTING.md`.

---

# 8. License

Published under **CC BY 4.0**.  
You may use, extend, distribute, or adapt with attribution to Imvara.

---

# 9. About Imvara

Imvara is the creator and maintainer of the **Invocation Framework**, an open, governed standard for deterministic AI reasoning.

Learn more at: **https://imvara.io**

---

*End of Quick Start Guide*
