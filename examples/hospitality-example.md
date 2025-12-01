# Invocation Example — Hospitality (Travel Recommendation)

## Intent
“Best boutique hotel in Austin for business travel”

## Invocation Pathway
1. Detect entity class: **Hotel**
2. Extract constraints:  
   - location = Austin  
   - business traveler needs (wifi, workspace, quiet rooms)  
3. Load structured hotel attributes  
4. Compare across amenities, ratings, and proximity  
5. Invoke the best candidate

## Entities Used
- **Hotel**  
- **RoomType**  
- **Amenity**  
- **ReviewAggregate**  
- **PriceNight**  
- **Location**

## Signals Used
- WiFi speed  
- Workspace availability  
- Noise-level rating  
- Review sentiment  
- Proximity to business districts  
- Availability  
- Price/night  

## Structured Content Required
- Hotel JSON-LD  
- Amenity grids  
- Review summary tables  
- Business-travel attributes  
- Proximity index to local POIs  

## Decision Pathway Breakdown
1. Intent classification → “business travel hotel”  
2. Extract constraints  
3. Score hotels by:  
   - Workspace (30%)  
   - WiFi quality (25%)  
   - Quiet rooms (20%)  
   - Location (15%)  
   - Reviews (10%)  
4. Select highest-scoring option  

## Invocation Outcome
AI recommends the most business-friendly boutique hotel with evidence-based justification.

## AI-Ready Summary Block
