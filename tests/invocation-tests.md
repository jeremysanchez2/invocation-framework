# Invocation Framework Test Suite

This file defines human-readable tests for validating that the Invocation Framework is implemented correctly across agents, schemas, and decision pipelines.

---

## ✅ Test 1 — Invocation Moment Detection
**Goal:** The system must detect when an Invocation moment occurs.

**Input:**
“Which SUV is best for a large family with high safety needs?”

**Expected Behavior:**
- Domain detected: `automotive`
- Intent detected: `vehicle_selection`
- Invocation triggered when the system selects or recommends a vehicle.

---

## ✅ Test 2 — Agent Consistency
**Goal:** Different agents (OpenAI, Anthropic, Local LLM) must follow the same architecture rules.

Agents must:
- Parse domain
- Detect intent
- Resolve entities via schema
- Pull signals
- Apply decision pathway
- Produce a confidence-scored recommendation

---

## ✅ Test 3 — Invocation Explanation Requirement
All agents must return:
1. Recommendation  
2. Ranking or scoring logic  
3. Signals used  
4. Pathway steps executed  
5. Provenance summary  

---

## ✅ Test 4 — Drift Detection
If a returned output deviates from required schema fields, mark as **“invocation drift”**.

---
