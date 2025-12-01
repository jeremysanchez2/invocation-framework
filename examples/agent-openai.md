# OpenAI Agent Invocation Example
**Imvara Invocation Framework — Agent Pattern Example**

This example shows how an OpenAI-compatible agent (GPT-4.1, GPT-5, o-series, or Assistants API) should interpret and execute an invocation request using Imvara’s Invocation Architecture, Entity Schema, and Decision Pathway Model.

---

## 1. User Intent

“Find the best air purifier for allergies under $300.”

---

## 2. Agent Workflow (OpenAI)

OpenAI models follow a **function-first**, **schema-guided**, **reasoning-optional** flow.

### Step 1 — Parse Intent
- Detect domain: *retail*
- Detect intent: *product_comparison*
- Detect constraints:
  - budget_max = 300
  - use_case = allergies

### Step 2 — Resolve Entity Classes
Based on `invocation-entity-schema.json`:

- **Product**
- **Attribute** → allergen_filter_rating
- **Signal** → CADR_score, filter_lifespan_months, noise_level_dB, rating_score

### Step 3 — Fetch Structured Inputs
(OpenAI agents typically call tools, APIs, or embeddings depending on setup.)

Example tool call:

```json
{
  "tool": "fetch_products",
  "arguments": {
    "category": "air_purifier",
    "max_price": 300
  }
}
```

Example response:

```json
{
  "products": [
    {
      "id": "p1",
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
      "id": "p2",
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

## 3. Decision Pathway Execution

Using `invocation-decision-pathway-schema.json`:

### Weighted Scoring Strategy
```
score = (0.35 * CADR_score_normalized)
      + (0.25 * filter_lifespan_normalized)
      + (0.20 * noise_level_inverse_normalized)
      + (0.20 * rating_score_normalized)
```

Example computed outcome:

- PureAir A100 → **0.88**
- BreezeCo SilentPro → **0.81**

**Winner: PureAir A100**

---

## 4. Structured Output (OpenAI Style)

```json
{
  "invocation_result": {
    "top_recommendation": {
      "brand": "PureAir",
      "model": "A100",
      "price": 249,
      "reasoning": {
        "signals": {
          "CADR_score": "High (210)",
          "filter_lifespan_months": "Moderate (6 months)",
          "noise_level_dB": "Quiet (28 dB)",
          "rating_score": "Strong (4.6)"
        },
        "explanation": "Selected due to highest weighted score for allergy-focused purification under $300."
      }
    },
    "alternatives_ranked": [
      {
        "brand": "BreezeCo",
        "model": "SilentPro",
        "score": 0.81
      }
    ],
    "invocation_meta": {
      "intent": "product_comparison",
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
- **Outcome-driven** → produces a definitive ranked recommendation  
- **Entity-governed** → uses Product, Attribute, and Signal schemas  
- **Signal-mediated** → normalizes and weights measurable factors  
- **Transparent** → includes output reasoning and pathway metadata  

**This example demonstrates:  
“How an OpenAI agent becomes structurally capable of Invocation.”**
