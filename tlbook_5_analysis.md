# Geospatial Analysis

---

## 1st 'Law' of Geography 
"everything is related to everything else, but near things are more related than distant things." - Walder Tobler
* *not a scientific law, more of a starting point for thinking about why things are happening where*

## Spatial Autocorrelation
- Moran's I - measure of spatial autocorrelation 

## Topological Relations
- disjoint  / intersects 
- is equal to
- contains / within 
- overlap with 
![toporelations](img/toporelations.png)

## Set Operations
![setoperations](img/setoperations.png)
## Point Pattern Analysis
- Avg Nearest Neighbor   
- Convex hull/envelope from common points    
- Ripley's K - test for significant clustering 
- Getis Ord D - hot/cold spot   

## Buffer 
- points, lines, or polygon vectors. Add or subtract buffer distance area 

## Interpolation 
Estimate a value at a location based on surrounding locations (time or space) 
*  nearest neighbor, bilinear, cubic resampling methods for reprojecting rasters (NN basic/fastest -> cubic most intensive)  
* IDW - further away, less weight given   
* Kriging - first derivative describes the rate that values change over a distance, or the effect of distance on the attribute  

## Global statistics
- Band (```b```) algebra: ```b1 + b2```
- Threshold/mask

## Focal / Neighborhood statistics
Require user-input kernel size/radius/distance for the moving window calculation   
- Low-pass filter - smooths surface
- High-pass filter - edge-enhancement / sharpening 
- Spatial Lags

## Descriptive Analytics



## Predictive Analytics
Predicts future or past based value based on historical (often time-series) data
- OLS
- GWR
- Clustering - DBSCAN, K-means, PCA
- RF, SVM - image classification 
- NN - image segmentation

## Perscriptive Analytics
Suggests decision options for how to take advantage of a future opportunity or mitigate a future risk, and shows the implication of each decision option. 
- site suitability analysis (SSA)
- vehicle routing:
  - https://developers.arcgis.com/python/guide/part1-introduction-to-network-analysis/
  - service area - travel times to customer. ex-to decide where to put fire station. regular buffer, cost over surface (elevation/slope), network (street travel time)
  - find closest facility for incidents 
  - An [origin-destination (OD) cost matrix](https://developers.arcgis.com/python/guide/part5-generate-od-cost-matrix/) from multiple origins to multiple destinations, is a table that contains the cost, such as the travel time or travel distance, from each origin to each destination
  - location allocation - be far from competition but near customers 
  - [vehicle routing problem](https://developers.arcgis.com/python/guide/part7-vehicle-routing-problem/) goal is to best service the orders and minimize the overall operating cost for the fleet of vehicles   
      - starts with OD cost matrix, iterates adds real-world heuristics 

