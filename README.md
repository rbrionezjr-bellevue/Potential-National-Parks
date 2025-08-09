# Identifying the Next U.S. National Park

This project uses geospatial and ecological data to score and rank federally managed lands in the United States for their potential designation as National Parks.  
The model combines biodiversity, protection status, and visitation potential into a **Park Potential Score**, producing a ranked list of candidate sites.

## Project Overview
The goal is to identify public lands with high ecological, recreational, and conservation value that are not currently designated as National Parks.  
The scoring model provides a data-driven starting point for agencies, policymakers, and conservation groups to guide future designation efforts.

## Data Sources
- **PAD-US v4.1** – U.S. Geological Survey: Protected Areas Database of the United States  
  <https://doi.org/10.5066/P9Q9LQ4B>
- **NPS Visitation Data** – National Park Service: Annual Visitation Summary Report  
  <https://irma.nps.gov/Stats/Reports/National>
- **NatureServe Explorer** – Biodiversity species occurrence and distribution data  
  <https://explorer.natureserve.org>

## Methods Summary
1. **Data Preparation**
   - Loaded PAD-US dataset using GeoPandas
   - Filtered out existing National Parks
   - Removed non-U.S. biodiversity records (ON, QC, BC, SU)
   - Removed parcels unlikely to be viable parks (`Unknown Park`, `Ennis National Fish Hatchery`, `Fullerton Sports Complex`)
   - Deduplicated parcels by `Unit_Nm`

2. **Scoring**
   - **Biodiversity**: 40% weight – state-level species counts normalized 0–1
   - **Protection**: 30% weight – GAP status codes from PAD-US
   - **Visitation Potential**: 30% weight – benchmark from NPS visitation data
   - Tie-breaks handled with `GIS_Acres` (larger areas rank higher)

3. **Ranking**
   - Combined weighted scores into **Park Potential Score**
   - Ranked all parcels from highest to lowest

4. **Visualization & EDA**
   - State-level potential score distribution
   - Ownership breakdown
   - Top 20 states by species count
   - Top 10 potential National Parks (final scorecard)

## Repository Structure
