# QGIS Practice: Suitable Swellendam Houses
This is a part of a series of lessons completed by following the tutorials outlined in the [QGIS Training Manual](https://docs.qgis.org/3.34/en/docs/training_manual/index.html), which is a component of the QGIS Documentation. The purpose was to learn and practice QGIS and geospatial skills. The lesson and data used in the practice is not my own, but was provided either by the QGIS Training Manual or Open Street Map.

**Specific Skills:**
- QGIS Environment
- Vector Analysis
- Raster Analysis

## Problem 
A realtor is looking for a house with the following criteria:
1. It is in Swellendam, South Africa
2. It is within reasonable driving distance of a school (1km)
3. It is more than 100m squared in size
4. Closer than 50m to a main road
5. Closer than 500m to a restaurant
6. Is north-facing
7. Has a slope of less than 5 degrees
8. But if the slope is less than 2 degrees, then the aspect doesn’t matter

## Solution
### Sourcing Data
Data for buildings, size of buildings, roads in the town, locations of schools, locations of restaurants was collected from Open Street Map, filtered and converted to WGS 84 / UTM Zone 34S CRS. A Digital Elevation Model (DEM) was provided with the exercise.
### Vector Analysis & Filtering
Vector geometry processing was done to buffer around main roads, restauraunts and schools, with intersections being used to show eligible buildings. Roads were filtered to only main roads, and buildings were filtered to only be above 100m squared in size. This takes care of critieria 1-5.
![](/images/vector_analysis_in_progress.png "In-progress secreenshot of a main road buffer, a school buffer, their intersection, and the buildings that fall in that intersection.")

### Raster Analysis
First the raster processing toolbox was used on the digital elevation model to create a map of the slope values of the terrain (Image 1). Then the raster calculator was used to calculate aspect and create a layer of north facing terrain (Image 2). $$ aspect@1 <= 90  ||  aspect@1 >= 270 $$

Then rasters were calculated of slopes less than or equal to 2 degrees and slopes less than or equal to 5 degrees. These were combined to highlight only areas that are either north facing and less than 5 degrees slope, or less than 2 degrees slope and any aspect (Image 3).

This was vectorized and overlayed onto the vector analysis from above.

![](/images/slope.png "Slope map of Swellendam") ![](/images/aspect.png "Aspect map of Swellendam") ![](/images/all_conditions.png "Slope less than 5 deg and aspect of North, or slope less than 2 deg map") ![](/images/suitable_terrain.png "Suitable terrain overlayed on the vector analysis map")

### Final Result
Intersecting the suitable terrain with the suitable buildings from the vector analysis gives the final answer of houses in Swellendam that suit all 8 criteria. 
![](/images/final.png)