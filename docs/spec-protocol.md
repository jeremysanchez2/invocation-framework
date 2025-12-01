# Invocation Protocol — Specification v0.1  
Version: 0.1  
Status: Draft (Public Technical Preview)  
Maintainer: Imvara  
Updated: 2025-12-01  

The Invocation Protocol defines the required output contract for all Invocation-compliant AI systems. It ensures that every model, vendor, or agent produces deterministic, explainable, enterprise-safe reasoning artifacts.

---

## 1. Purpose

The Invocation Protocol standardizes how AI systems report:

- what entities were evaluated  
- what signals contributed to the decision  
- what constraints shaped the reasoning  
- what steps the model took internally  
- how results were ranked  
- what safety checks were executed  
- whether a human-readable explanation is available  

This protocol acts as the execution ledger for the Invocation OS.

---

## 2. Required Output Contract (Normative)

Invocation-compliant systems **must** return a JSON-LD object matching the machine-readable schema defined in:

`/invocation-protocol/invocation-protocol-v0.1.jsonld`

---

## Required Fields

| Field | Type | Description |
|-------|-------|-------------|
| `decision_pathway_used` | string | Identifier of the executed Decision Pathway |
| `entities_evaluated` | array<string> | Structured entity identifiers analyzed |
| `signals_used` | array<string> | Signals contributing to reasoning |
| `constraints_applied` | array<string> | Hard and soft constraints applied |
| `pathway_steps` | array<object> | Ordered execution trace |
| `ranked_results` | array<object> | Final structured and ranked outputs |
| `explanation_available` | boolean | Whether an explanation exists |
| `explanation_reference` | string (optional) | URI for explanation resource |
| `confidence_score` | number (optional) | Model-level confidence |
| `safety_checks` | object | Structured safety validation results |

All fields marked **required** must appear in every Invocation-compliant output.

---

## 3. Validation Rules

Invocation-compliant responses are validated against the following:

### 3.1 Presence Validation  
All required fields must be present and non-null.

### 3.2 Type Validation  
All fields must match their type definitions.

### 3.3 Entity & Signal Integrity  
All referenced entities and signals must map to governed schemas.

### 3.4 Deterministic Pathway  
Given identical inputs and constraints, the same pathway must be invoked.

### 3.5 Ranked Result Ordering  
Results must be sorted in descending relevance.

### 3.6 Explanation Rule  
If `explanation_available = true`, an `explanation_reference` must be included.

### 3.7 Safety Validation Structure  
`safety_checks` must define:

- `disallowed_entities_filtered`  
- `incomplete_signals_detected`  
- `fallback_pathway_triggered`

---

## 4. Example Invocation Output (Compliant)

```json
{
  "decision_pathway_used": "retail.product_comparison",
  "entities_evaluated": ["product:123", "product:456"],
  "signals_used": ["price", "rating_score", "cadence_score"],
  "constraints_applied": ["budget_max <= 40"],
  "pathway_steps": [
    { "stage": "intent_parse", "duration_ms": 2 },
    { "stage": "entity_bind", "duration_ms": 1 }
  ],
  "ranked_results": [
    { "id": "product:123", "score": 0.91 },
    { "id": "product:456", "score": 0.83 }
  ],
  "explanation_available": true,
  "explanation_reference": "urn:explanations:invocation:abc123",
  "confidence_score": 0.78,
  "safety_checks": {
    "disallowed_entities_filtered": [],
    "incomplete_signals_detected": [],
    "fallback_pathway_triggered": false
  }
}
```

---

## 5. Compliance Testing

Automated tests are provided in:  
`/tests/test-invocation-protocol.json`

The test suite validates:

- required field presence  
- type correctness  
- explanation logic  
- safety structure integrity  
- deterministic execution  
- schema violation behavior  

---

## 6. Versioning & Governance

The Invocation Protocol follows the Imvara Invocation Framework rules for governance:

- formal versioning  
- public changelogs  
- vendor review cycles  
- backward-compatible schema evolution  

---

## 7. References

- Invocation OS Specification  
- Entity Schema Registry  
- Signal Schema  
- Decision Pathway Schema  
- Imvara Invocation Framework (Core)
