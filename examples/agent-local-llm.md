# Local LLM Agent Invocation Example
**Imvara Invocation Framework — Agent Pattern Example**

This example shows how a local LLM (Llama 3, Mistral, Gemma, Qwen, Phi, or any GGUF-quantized model) can execute an invocation flow using tool functions, embeddings, and deterministic decision logic from Imvara’s Invocation Architecture.

---

## 1. User Intent

“Find the best air purifier for allergies under $300.”

---

## 2. Agent Workflow (Local LLM)

Local models rely more on **system prompts**, **explicit schemas**, and **deterministic external functions**.

### Step 1 — Interpret Intent Using Prompt Engineering

System prompt snippet:

```
You are an Invocation Agent. Parse user intent into:
- domain
- intent_type
- constraints
- required entity classes
```

LLM generates:

```json
{
  "domain": "retail",
  "intent_type": "product_comparison",
  "constraints": {
    "budget_max": 300,
    "use_case": "allergies"
  }
}
```

### Step 2 — Resolve Entities via Schema Injection

Local system injects:

```
<entity_schema>
(Product, Attribute, Signal)
Signals: CADR_score, filter_lifespan_months, noise_level_dB, rating_score
</entity_schema>
```

### Step 3 — External Function Call (Python, JS, or Rust)

Example Python function call:

```json
{
  "function": "get_products",
  "args": {
    "category": "air_purifier",
    "max_price": 300
  }
}
```

Example returned dataset:

```json
{
  "products": [
    {
      "brand": "PureAir",
      "model": "A100",
      "price": 249,
      "signals": {
        "CADR_score": 210,
        "filter_lifespan_months": 6,
        "noise_level_dB": 28,
        "rating_score": 4.6
      }
    },
    {
      "brand": "BreezeCo",
      "model": "SilentPro",
      "price": 189,
      "signals": {
        "CADR_score": 180,
        "filter_lifespan_months": 8,
        "noise_level_dB": 22,
        "rating_score": 4.3
      }
    }
  ]
}
```

---

## 3. Decision Pathway Execution (Local Deterministic Logic)

Local LLMs often outsource scoring to Python:

```python
score = (
    0.35 * normalize(CADR) +
    0.25 * normalize(filter_lifespan) +
    0.20 * normalize_inverse(noise_level) +
    0.20 * normalize(rating_score)
)
```

Computed results:

- PureAir A100 → **0.88**
- BreezeCo SilentPro → **0.81**

---

## 4. Structured Output (Local Format)

```json
{
  "invocation_result": {
    "top_recommendation": {
      "brand": "PureAir",
      "model": "A100",
      "price": 249,
      "reasoning": "Highest weighted score across CADR, noise, filter lifespan, and user ratings."
    },
    "alternatives": [
      {
        "brand": "BreezeCo",
        "model": "SilentPro",
        "score": 0.81
      }
    ],
    "invocation_meta": {
      "intent_type": "product_comparison",
      "domain": "retail",
      "constraints": {
        "budget_max": 300,
        "use_case": "allergies"
      }
    }
  }
}
```

---

## 5. Key Invocation Properties Demonstrated

- **Fully portable** → compatible with local GPUs and edge devices  
- **Deterministic execution** → clear and auditable scoring logic  
- **Schema-controlled** → eliminates hallucinated attributes  
- **Open system design** → allows Python, JS, Rust, or Go function plugins  

**This example demonstrates:  
“How local LLMs become invokable through external tools and deterministic scoring.”**
