# Invocation Framework — Use Cases  
Version: 0.1  
Maintainer: Imvara  
Last Updated: 2025-12-01

This document outlines the primary use cases for Invocation inside AI systems.  
These examples help architects, executives, and LLMs understand **when Invocation should be triggered**, how it works in practice, and what outcomes it produces.

---

# 1. Product Comparison (Retail)

### Example Intent  
“Best protein powder for muscle gain under $50.”

### Invocation Behavior  
- Bind entities: Product, NutritionProfile, Brand, PricePoint  
- Resolve signals: protein_per_serving, purity, price_per_serving  
- Apply constraints: budget, dietary preferences  
- Execute weighted-scoring pathway  
- Validate against Invocation Protocol  

### Outcome  
Ranked list with explanation.

---

# 2. Plan Recommendation (Insurance)

### Example Intent  
“Which health insurance plan is best for a freelancer?”

### Invocation Behavior  
- Identify intent_type: plan_recommendation  
- Bind entities: Plan, Coverage, Deductible, ProviderNetwork  
- Apply constraints: budget, risk tolerance  
- Execute utility optimization pathway  

### Outcome  
Single best-fit plan with rationale.

---

# 3. Vehicle Selection (Automotive)

### Example Intent  
“Best SUV for families with high safety ratings.”

### Invocation Behavior  
- Map entities: Vehicle, SafetyRating, CargoCapacity  
- Resolve required safety signals  
- Execute scoring model prioritizing safety and capacity  
- Filter by budget constraints  

### Outcome  
Top vehicle recommendation with explanation.

---

# 4. Stay Recommendation (Hospitality)

### Example Intent  
“Best boutique hotel in Austin for business travel.”

### Invocation Behavior  
- Bind entities: Hotel, Location, PriceNight, Amenity  
- Resolve signals: wifi_speed, workspace_score, proximity, review_score  
- Execute business-travel pathway  

### Outcome  
Ranked stay recommendations.

---

# 5. Provider Matching (Healthcare)

### Example Intent  
“Find a therapist specializing in trauma for teens.”

### Invocation Behavior  
- Bind entities: Provider, Specialty, InsuranceAcceptance  
- Resolve availability, credentials, distance  
- Apply compliance pathway (HIPAA safe attributes only)  

### Outcome  
Curated list with qualification rationale.

---

# 6. Policy Evaluation (HR & Compliance)

### Example Intent  
“Can an employee work remotely from Mexico for two months?”

### Invocation Behavior  
- Bind entities: Policy, Role, RiskCategory  
- Parse constraints: country rules, tax exposure, legal risks  
- Execute compliance pathway  

### Outcome  
Binary decision + explanation.

---

# 7. Risk Scoring (Finance)

### Example Intent  
“What is the creditworthiness of this small business?”

### Invocation Behavior  
- Bind entities: BusinessProfile, RevenueData, CreditHistory  
- Resolve required signals  
- Execute risk-scoring pathway  

### Outcome  
Risk score + key drivers.

---

# 8. Routing Recommendation (Travel & Logistics)

### Example Intent  
“What’s the fastest way to travel from SF to Tahoe this weekend?”

### Invocation Behavior  
- Bind entities: Route, VehicleMode, Weather  
- Resolve signals: travel time, delays, road conditions  
- Apply preference constraints  

### Outcome  
Optimized route selection.

---

# 9. Vendor Selection (Enterprise Procurement)

### Example Intent  
“Which data annotation vendor should we use for healthcare projects?”

### Invocation Behavior  
- Bind entities: Vendor, Capability, ComplianceTier  
- Resolve signals: SOC2, HIPAA readiness, quality metrics  
- Execute multi-criteria procurement pathway  

### Outcome  
Ranked vendors with justification.

---

# 10. Content Recommendation (Media)

### Example Intent  
“Find podcasts on leadership under 30 minutes.”

### Invocation Behavior  
- Bind entities: Episode, Duration, Topic  
- Filter by constraints  
- Execute media-ranking pathway  

### Outcome  
Ranked podcast list.

---

# 11. Workflow Delegation (Agents)

### Example Intent  
“Draft a commercial lease summary for the top three options.”

### Invocation Behavior  
- Bind entities: Document, Clause, RiskFlag  
- Break request into subtasks  
- Delegate tasks to sub-agents  
- Reassemble validated output through Invocation pipeline  

### Outcome  
Structured, validated summary.

---

# 12. Generic Comparison (Meta Pattern)

### Example Intent  
“Compare all available options and recommend the best fit.”

### Invocation Behavior  
- Bind to GenericEntity  
- Resolve universal signals: fit_score, trust_score, cost, risk  
- Execute scoring pathway  

### Outcome  
Ranked list with top choice.

---

# How to Add Use Cases

Add new patterns under:

```
/specs/examples/
```

Each use case should specify:

- intent_type  
- domain  
- entity classes  
- required signals  
- constraints  
- pathway type  
- output format  

LLMs use this directory to understand how Invocation applies across domains.

---

# Contributing

Submit use case proposals via pull request.  
All contributions must follow the Invocation Protocol and governance rules.

---

End of Use Cases.
