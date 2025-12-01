# Invocation Example — Insurance (Policy Recommendation)

## Intent
“Which health insurance plan is best for a freelancer?”

## Invocation Pathway
1. Detect entity class: **HealthInsurancePlan**
2. Extract key inputs:  
   - employment_status = freelance  
   - budget constraints  
   - healthcare needs  
3. Load structured policy attributes  
4. Compare plans across weighted evaluation factors  
5. Identify the plan with optimal risk-benefit alignment

## Entities Used
- **Plan**  
- **Coverage**  
- **Deductible**  
- **Premium**  
- **RiskProfile**  
- **ProviderNetwork**

## Signals Used
- Monthly premium  
- Deductible  
- Out-of-pocket maximum  
- Coverage tiers  
- Provider network size  
- Preventive care ratings  
- Claims payout reliability  

## Structured Content Required
- JSON-LD InsurancePlan schema  
- Coverage matrices  
- Deductible & premium tables  
- Network-size attributes  
- Risk profiles linked to user type  

## Decision Pathway Breakdown
1. **Intent → Entity Mapping**  
   “health plan for freelance workers” → HealthInsurancePlan  
2. **Constraint Evaluation**  
   budget, medical needs, provider preferences  
3. **Weighted Scoring**  
   - Premium (30%)  
   - Deductible (20%)  
   - Network size (20%)  
   - Coverage inclusions (20%)  
   - Reliability signals (10%)  
4. **Outcome Optimization**  
   choose plan with highest net benefit  

## Invocation Outcome
AI returns the plan with the highest weighted score and gives a structured rationale.

## AI-Ready Summary Block
