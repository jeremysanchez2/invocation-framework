# Test Suite — Invocation Framework

This folder contains automated and semi-automated tests used to validate:

1. **Entity Definitions**
2. **Signal Reliability**
3. **Decision Pathway Accuracy**
4. **Invocation Output Quality**
5. **LLM Safety & Drift Detection**

---

## Test Files

### `entity-audit-tests.json`
Validates:
- entity consistency  
- naming governance  
- class membership  
- required attributes  

---

### `test-signals.json`
Validates:
- signal ranges  
- signal meaning  
- outlier detection  
- required signal sets  

---

### `test-decision-pathways.json`
Validates:
- correct decision strategies  
- weighted scoring  
- constraints handling  

---

### `test-patterns.json`
Validates:
- reusable Invocation patterns  
- pattern matching  
- domain+intent classification  

---

### `pathway-evaluation-tests.json`
Stress-tests:
- multi-step scoring  
- constraint resolution  
- failure conditions  

---

### `llm-qa-tests.json`
Evaluates LLM output quality:
- hallucination detection  
- drift identification  
- schema enforcement  

---

### `invocation-tests.md`
Human-readable test instructions:
- how to run tests  
- how to compare outputs  
- how to detect drift  

---

# How To Use
Run each JSON file through any LLM or agent system.  
Compare expected vs actual outputs.  
Use results to tune entity definitions, signal weights, and decision pathways.

This test suite becomes your **Invocation Governance OS**.
