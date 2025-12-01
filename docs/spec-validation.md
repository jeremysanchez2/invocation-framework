# Invocation Framework — Validation Specification  
Version: 0.1  
Status: Draft (Public Technical Preview)  
Maintainer: Imvara  
Last Updated: 2025-12-01  

This specification defines the **Validation Layer** for Invocation-compliant systems.  
Validation guarantees that every Invocation completes with **deterministic**, **safe**, **schema-aligned**, and **explainable** outputs.

The Validation Layer is the “contract enforcer” of the Invocation Framework.  
All systems MUST implement the rules in this document to claim Invocation compliance.

---

## 1. Purpose of the Validation Layer

Invocation validation ensures that:

- Inputs are well-formed  
- Entities and signals conform to canonical schemas  
- Pathway execution is deterministic  
- Outputs follow the Invocation Protocol  
- Explanations are complete and reproducible  
- Drift, errors, and unsafe outputs are prevented  

No Invocation result may be returned to the user **until it fully passes validation**.

---

## 2. Validation Pipeline

All systems MUST implement the complete validation sequence:

```text
1. Input Validation
2. Schema Validation
3. Signal Validation
4. Pathway Validation
5. Output Validation (Invocation Protocol v0.1)
6. Safety Validation
```

Validation MUST be executed **after** computation but **before** any output is returned.

---

## 3. Input Validation

The system MUST confirm:

1. **Intent structure validity**  
   - Domain MUST be known  
   - Intent type MUST be registered  
   - Constraints MUST be typed correctly  
   - Detected entities MUST be semantically valid  

2. **Malformed inputs MUST be rejected**  
   Examples:  
   - Missing fields  
   - Invalid JSON  
   - Contradictory constraints (e.g., “budget_max = -10”)  

3. **Input provenance logging is required**  
   Systems MUST record:  
   - Timestamp  
   - Model version  
   - Intent interpreter version  

**Input Validation Output Example:**

```json
{
  "input_valid": true,
  "errors": []
}
```

---

## 4. Schema Validation

All required schemas MUST be validated before any pathway executes.

### Systems MUST verify:

- Entities match the canonical definitions in `/specs/schemas/`  
- Signals correspond to required types  
- Field names and shapes match schema definitions  
- Deprecated fields trigger warnings but MUST NOT break validation  
- Units and data types are correct (e.g., price as number, not string)  

### Schema Validation Failure MUST block execution.

**Example Failure:**

```json
{
  "schema_valid": false,
  "errors": [
    "missing_required_signal: protein_per_serving"
  ]
}
```

---

## 5. Signal Validation

Signal validation ensures that all required signals for the decision pathway are:

- Present  
- Within allowed ranges  
- Fresh (if freshness requirements exist)  
- Normalized to canonical units  
- Correctly typed  
- Non-null unless explicitly allowed  

### Missing Signals Handling

If a required signal is missing:

- The Invocation MUST NOT proceed  
- The missing signal MUST be listed in the output explanation  
- The model MUST NOT infer or hallucinate a replacement  

### Example Signal Validation Output

```json
{
  "signal_valid": true,
  "missing_signals": []
}
```

---

## 6. Pathway Validation

The decision pathway MUST pass validation checks for:

### **6.1 Conformance to the pathway schema**

- Required entities present  
- Required signals present  
- Valid weights or rule structures  
- No undefined branches or steps  

### **6.2 Determinism**

The system MUST guarantee:

- No stochastic operations  
- No dependence on model sampling randomness  
- No reliance on temperature-based heuristics  

### **6.3 Execution Logging**

Pathway evaluation MUST log:

- Signals used  
- Entities eliminated and why  
- Scoring computations  
- Constraint applications  

### Example:

```json
{
  "pathway_valid": true,
  "execution_log_recorded": true
}
```

---

## 7. Output Validation — Invocation Protocol v0.1

All Invocation results MUST be validated against the Invocation Protocol.

### Required Output Fields:

A conformant output MUST include:

1. `decision_pathway_used`  
2. `entities_evaluated`  
3. `signals_used`  
4. `constraints_applied`  
5. `ranked_results` or `recommendation`  
6. `explanation_available`  
7. `version`  

### Additional Rules:

- No undefined fields  
- No empty required results  
- No unlogged eliminations  
- No missing pathway version  

### Example Validated Output:

```json
{
  "output_valid": true,
  "errors": []
}
```

---

## 8. Safety Validation

Before returning any recommendation, the system MUST pass:

### **8.1 Safety Class Checks**
Signals or entities classified as “Sensitive” MUST follow stricter rules.

### **8.2 Hallucination Prevention**
The system MUST verify:

- No invented brands  
- No invented products  
- No fabricated statistics  
- No unverified claims  

### **8.3 Constraint Safety**
Risk-related constraints MUST be validated, such as:

- Medical  
- Financial  
- Legal  
- Insurance  

### **8.4 Explanation Completeness**
Explanations MUST include:

- Why the entity was selected  
- How signals contributed  
- How constraints shaped the result  
- Pathway version  

No explanation ⇒ NO output.

---

## 9. Validation Error Model

All validation failures MUST follow the canonical error schema:

```json
{
  "error": {
    "type": "ValidationError",
    "stage": "signal_validation",
    "message": "Missing required signal: protein_per_serving",
    "metadata": {
      "pathway": "retail.product_comparison.v1",
      "entity": "product_123"
    }
  }
}
```

No Invocation-compliant system may expose internal stack traces.

---

## 10. Validation Logging Requirements

Every Invocation execution MUST log:

- Input validation results  
- Schema validation results  
- Signal validation details  
- Pathway execution logs  
- Timestamp  
- Model version  
- Invocation OS version  
- Pathway version  

This ensures:

- Reproducibility  
- Auditability  
- LLM hallucination detection  

---

## 11. Compliance Testing

Validation compliance is tested through:

- `/tests/validation/` — unit tests  
- `/tests/pathways/` — deterministic evaluation tests  
- `/tests/schemas/` — schema conformance  
- `/tests/protocol/` — full Invocation Protocol conformity  

A system MAY claim compliance **only if all tests pass**.

---

## 12. Conformance Claim Requirements

A system MAY declare:

> **“Invocation Validation v0.1 Compliant”**

ONLY if:

- It implements the full validation pipeline  
- All required logs are produced  
- All schemas validate successfully  
- All pathways pass deterministic evaluation  
- All outputs pass Invocation Protocol validation  

Partial compliance claims are prohibited.

---

## 13. License

Released under **CC BY 4.0**.

---

*End of Validation Specification*
