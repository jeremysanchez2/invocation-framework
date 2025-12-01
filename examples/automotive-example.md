# Invocation Example — Automotive (Vehicle Selection)

## Intent
“Best SUV for families with high safety ratings”

## Invocation Pathway
1. Detect entity class: **SUV**
2. Extract constraints:  
   - family-friendly  
   - safety rating priority  
   - cargo space  
3. Load structured attributes from vehicle schema  
4. Compare vehicles using decision pathways  
5. Invoke the top-scoring vehicle

## Entities Used
- **Vehicle**  
- **SafetyRating**  
- **CargoCapacity**  
- **FuelEfficiency**  
- **TrimLevel**  
- **PriceBand**

## Signals Used
- NHTSA or IIHS safety rating  
- Crash-test scores  
- Cargo volume  
- Seating capacity  
- Reliability ratings  
- MPG  
- Price  

## Structured Content Required
- Vehicle JSON-LD  
- Safety-rating attributes  
- Feature comparison tables  
- Reliability score blocks  
- Trim-level structured descriptions  

## Decision Pathway Breakdown
1. Detect category → SUV  
2. Extract constraints from query  
3. Score attributes (safety weighted 40%)  
4. Rank candidates  
5. Output best match  

## Invocation Outcome
AI returns the SUV that maximizes safety while meeting family utility criteria.

## AI-Ready Summary Block
