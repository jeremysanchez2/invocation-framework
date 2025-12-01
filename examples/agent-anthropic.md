# Anthropic Agent Invocation Example
**Imvara Invocation Framework — Agent Pattern Example**

This example shows how a Claude-compatible agent (Claude 3.5 Sonnet / Opus / Haiku, Tools API, or Messages API) interprets and executes an invocation request using Imvara’s Invocation Architecture, Entity Schema, and Decision Pathway Model.

---

## 1. User Intent

“Find the best air purifier for allergies under $300.”

---

## 2. Agent Workflow (Anthropic)

Claude models follow a **reasoning-first**, **schema-consistent**, **constitutional-explanation** flow.

### Step 1 — Parse Intent (Claude reasoning)
Claude generates a structured interpretation:

```json
{
  "domain": "retail",
  "intent": "product_comparison",
  "constraints": {
    "budget_max": 300,
    "use_case": "allergies"
  }
}
```

### Step 2 — Resolve Entity Classes
Using `invocation-entity-schema.json`:

- **Product**
- **Attribute** → allergen_filter_rating
- **Signal** → CADR_score, filter_lifespan_months, noise_level_dB, rating_score

### Step 3 — Call Tools (if enabled)

Claude tool request:

```json
{
  "tool": "fetch_products",
  "input": {
    "category": "air_purifier",
    "max_price": 300
  }
}
```

Tool returns:

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

## 3. Decision Pathway Execution (Claude Style)

Claude prefers **reasoned scoring** over pure numeric weighting:

```
For allergy-sensitive users:
- CADR_score is primary
- Quiet operation is secondary
- Filter lifespan and ratings confirm reliability
```

Normalizing these signals produces:

- PureAir A100 → **0.88**
- BreezeCo SilentPro → **0.81**

---

## 4. Structured Output (Anthropic Style)

```json
{
  "invocation_result": {
    "top_recommendation": {
      "brand": "PureAir",
      "model": "A100",
      "price": 249,
      "explanation": {
        "summary": "The PureAir A100 provides the strongest combination of CADR performance, quiet operation, and verified user ratings under $300.",
        "signal_breakdown": {
          "CADR_score": "210 (strong airflow)",
          "noise_level_dB": "28 dB (quiet)",
          "filter_lifespan_months": "6 months",
          "rating_score": "4.6"
        }
      }
    },
    "ranked_alternatives": [
      {
        "brand": "BreezeCo",
        "model": "SilentPro",
        "score": 0.81
      }
    ],
    "invocation_meta": {
      "domain": "retail",
      "intent": "product_comparison",
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

- **Reasoning-first execution** → Claude explains each scoring step  
- **Entity schema fidelity** → uses Product, Attribute, Signal classes  
- **Bias-aware** → ensures transparent justification  
- **Constitutional grounding** → aligns recommendation with safety principles  

**This example demonstrates:  
“How Claude becomes invokable through reasoning and schema fidelity.”**
