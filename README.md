# Corporate Headquarters Site Suitability Analysis

**Tools:** ArcGIS Pro · Suitability Modeler · Spatial Analyst
**Study area:** Plattsburgh region, Lake Champlain, New York / Vermont
**Course:** *Spatial Data Science: The New Frontier in Analytics* (Esri Academy)

## Overview

A multi-criteria suitability analysis to find the best location for a corporate headquarters campus with a minimal environmental footprint. The analysis follows the five-stage Esri suitability workflow: **Base criteria → Transform → Weight/Combine → Locate → Evaluate**.

The result is a campus of five buildings (500 hectares in total) placed in the most suitable areas.



[Suitable locations for the five campus buildings]
<img width="5100" height="3300" alt="Headdquarters_siting_Layout" src="https://github.com/user-attachments/assets/4aac033a-75ae-4e10-96e6-71fa00056681" />




## Objective

Stakeholders asked for a headquarters that:

- Is built on gentle terrain, away from wetlands and high-density areas
- Is close to major roads but has low visibility from them
- Supports energy independence (solar potential, access to the electric grid)
- Gives employees access to amenities
- Keeps its environmental impact low

This project focuses on the **Building Site** objective, built as a submodel.

## Methodology

### 1. Base criteria

| Criterion | Input data | Derived layer |
|---|---|---|
| Wetlands and high-density areas are less preferred | Land-use layer | `LandUse` |
| Steep slopes are less preferred | Elevation | `Slope` |
| Closer to major roads is preferred | Major roads | `Dist_MRoads` |
| Visibility from major roads is less preferred | Viewshed | `Views_Zero` |






### 2. Transform

Each criterion was rescaled to a common 1–10 suitability scale with functions suited to its behavior (for example, a decay function for slope, so small values score highest, and category-based preferences for land use).






### 3. Weight and combine

Criteria were weighted with the **multiplier** method, since the criteria could be compared directly with one another, and combined into a single suitability surface (`HQ_Building_Site`, then `HQ_Final_Suitability`).

| Criterion | Weight |
|---|---|
| LandUse | 1.6 |
| Slope | 1.6 |
| Dist_MRoads | 1.25 |
| Views_Zero | 1.25 |






### 4. Locate

The Suitability Modeler **Locate** tool selected the best placement for the five campus buildings from the full-resolution (30 m) suitability surface:

| Parameter | Value |
|---|---|
| Total area | 500 hectares |
| Number of regions (campus buildings) | 5 |
| Region shape | Circle |
| Shape/utility tradeoff | 50% |
| Evaluation method | Highest average value |
| Distance between buildings | 0.5 – 2 km |
| Output | `Suitable_locations` |

### 5. Evaluate

used the **Swipe** tool to compare `Suitable_locations` against the input layers. The building locations sit in areas with limited visibility from major roads and fairly gentle slopes, which confirms they meet the stated requirements.






## Key takeaways

- Built an end-to-end multi-criteria suitability model in ArcGIS Pro.
- Used weighting to reflect stakeholder priorities.
- Placed a multi-building campus within spatial constraints (total area, building shape, and spacing) from a continuous suitability surface.
- Validated results visually with Swipe.

## Acknowledgements

Data and exercise from the Esri Academy course *Spatial Data Science: The New Frontier in Analytics*.

## Author

**Khadijah Assaggaf**
GIS Graduate, King Abdulaziz University
