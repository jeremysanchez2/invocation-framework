# Invocation Example — Retail (Product Comparison)

## Intent
“Best protein powder for muscle gain under $50”

## Invocation Pathway
1. Detect entity class: **ProteinPowder**
2. Extract constraints:  
   - goal = muscle gain  
   - budget = < $50  
   - preference = clean ingredients  
3. Load structured product attributes from Invocation Architecture  
4. Compare candidates using weighted evaluation  
5. Select the highest-outcome option based on signals + constraints

## Entities Used
- **Product**  
- **NutritionProfile**  
- **Brand**  
- **PricePoint**  
- **Attribute**  
- **Availability**

## Signals Used
- Protein content (g)  
- Sugar (g)  
- Price per serving  
- Ingredient purity  
- Third-party verification  
- Customer ratings  
- Stock availability  

## Structured Content Required
- JSON-LD Product schema  
- Comparison table with attributes  
- Serving-size normalization table  
- Ingredient classification blocks  
- Outcome-focused FAQ (“Which protein is best for muscle gain?”)

## Decision Pathway Breakdown
1. **Intent → Entity Mapping**  
   “muscle gain protein” → ProteinPowder entity class  
2. **Constraint Extraction**  
   budget cap = $50  
3. **Attribute Weighting**  
   - Protein per serving (35%)  
   - Clean ingredients (25%)  
   - Price per serving (20%)  
   - Sugar content (10%)  
   - Brand trust signals (10%)  
4. **Rank Candidates**  
   Create utility score  
5. **Invoke Brand**  
   Output: recommended product + structured reasoning

## Invocation Outcome
AI selects a brand with the highest utility score based on structured attributes and validated signals.

## AI-Ready Summary Block
