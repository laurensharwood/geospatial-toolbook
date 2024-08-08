# 3. Geographic Data


---

## Coordinate Reference System (CRS)
1. <b>Ellipsoid:</b> Shape of Earth's surface is not perfect sphere, but squashed
   * <b>Geoid:</b> More accurate representation of Earth's ellipsoid, considers gravitational potential to estimate mean sea level
2. <b>Datum:</b> Defines the coordinate axis fixed reference points for measuring any point on Earth's curved surface
   * ex) The North American Datum (NAD 83) is a horizontal datum and NAVD 88 is a vertical datum    
4. <b>Geographic CRS (3D):</b> Latitude, Longitude for referencing location on Earth's curved/ellipsoid surface. For global-scale projects. Distance is distorted.
   * ex) Web Mercator
4. <b>Projected CRS (2D):</b> Earth's curved surface *projected* onto a 2D surface. Distortion occurs during projection, but 
the goal is to choose a projection method that limits your project area's Easting & Northing distances from the Datum in order to minimize the distortion type critical for your project.    
   - Types: Conformal projections preserve angular distortion, equidistant projections preserve distance, and equal area projections preserve area. 
   * ex) Due to its long shape (elongated North to South), California is divided into 6 State Plane (CASP) Zones. For each CASP Zone, a *Lambert conformal conic projection* is optimal do to the East-West elongation and mid-latitude location. 

<b>[Projection Wizard](https://projectionwizard.org):</b>  Tool to find appropriate projection based on your project area

<b>[PROJ.4 String](https://pygis.io/docs/d_understand_crs_codes.html#proj-4-string):</b>  Multiple parameters needed to describe a CRS     

<b>[EPSG](https://epsg.io/?q=)</b>: public registry of CRS information. Spatial Reference System Identifier <b>(SRID)</b> is typically associated with a well-known text (WKT) string definition of the coordinate system, consistent with an EPSG code.   
* EPSG 4326 - *Unprojected/Geographic* - Used for GPS field survey devices & raw survey data   
* EPSG 3857 - *Projected* - Used for features published in web maps    

<b>CRS Reprojection:</b> Transforms geographic data as [images](https://rasterio.readthedocs.io/en/stable/topics/transforms.html) or [vectors](https://www.earthdatascience.org/workshops/gis-open-source-python/reproject-vector-data-in-python/) between different coordinate reference systems.  

---

## Common Data Types & Formats 

### Vectors
Vectors represent objects as features (point, line, or polygon shape) with tabular data containing attributes/fields values for each geometry.   
  * <b>ESRI [feature class](https://pro.arcgis.com/en/pro-app/latest/help/data/feature-classes/feature-classes.htm)</b>: homogenous collection of features (points, lines, or polygons) and can be stored in geodatabases, shapefiles, coverages, or other data formats. For instance, in an ESRI file geodatabase a feature classes can be annotations.    
  * <b>ESRI [shapefile](https://doc.arcgis.com/en/arcgis-online/reference/shapefiles.htm)</b>: A set of files (.shp, .shx, .dbf, & .prj) that contain one feature class   
  * <b>Databases</b>: SQLite, MS Access, PostgreSQL, ESRI file geodatabase   
  * <b>[GeoJSON](https://geojson.org/)</b>: [JSON ```features```](https://courses.spatialthoughts.com/python-foundation.html#understanding-json-and-geojson)  have ```properties``` and ```geometry```
	* [GeoJSON creator](https://geojson.io)   
  * <b>KML/KMZ</b>: for Google Earth Pro   
  * <b>[Geoparquet](https://geoparquet.org/)</b>: Supports <i>columnar</i> data storage making it a faster alternative to .csv files      

#### Networks:   
* Set of connected objects in geographic space to answer questions about connections and flow.   
* Contain objects (as nodes/points and connections/lines). May involve adjacency matrix calculation.  

### Rasters
Rasters are grids of cells, or pixels, with values that represent continuous fields (for example: elevation, temperature, light reflected from Earth's surface)   
  * <b>Tagged Image File Format</b> (.tiff or .tif) - Platform-independent image format   
  * <b>[GeoTIFF](https://ogc.org/standard/geotiff/)</b> - Tiff with metadata for geographic information   
  * <b>Band sequential</b> ([BSQ](https://desktop.arcgis.com/en/arcmap/latest/manage-data/raster-and-images/bil-bip-and-bsq-raster-files.htm)) - Optimal for accessing any part of a single band (spatial). Data is written one band at a time. Must have an associated ASCII file header (.hdr)      
  * <b>Band interleaved by pixel</b> ([BIP](https://desktop.arcgis.com/en/arcmap/latest/manage-data/raster-and-images/bsq-format-example.htm)) - Optimal for accessing multiple bands (spectral). Data for each pixel is written band by band. Must have an associated .hdr     
  * <b>Band interleaved by line</b> ([BIL](https://desktop.arcgis.com/en/arcmap/latest/manage-data/raster-and-images/bil-format-example.htm)) - Compromise allowing for easy access of spectral and spatial information. Pixels are written band by band for each line, or row. Must have an associated .hdr   
  * <b>netCDF</b> - multidimensional rasters, often time-series  
  * <b>Hierarchical Data Format v5</b> ([HDF5](https://www.ogc.org/standard/HDF5/)) - Supports large, heterogeneous data. uses a 'file directory' structure  
  * <b>Cloud Optimized Geotiff</b> ([COG](https://www.cogeo.org/)) - GeoTiff hosted on a HTTP file server  

##### Image Resolution  
<b>Spatial</b> = raster pixel or cell size 
  * Refers to the smallest detectable object, or amount of granularity/precision      
  * Fine resolution = small pixel size    
  * Coarse resolution = large pixel size    

<b>Temporal</b> = data collection frequency    
<b>Spectral</b> = number and width of spectral bands collected by a sensor     
<b>Radiometric</b> = bits / number of possible data values    

 
### Light Detection and Ranging (lidar)
Often used to create 3D digital surface height models (DSM) and digital elevation models (DEM).        

<b>Lidar file formats</b>:  
  * ASCII: raw lidar data   
  * [LAS](https://www.ogc.org/standard/LAS/): 3D point clouds with XYZ (lon-lat-ele) values    
  * LAZ (zipped LAS)   

<b>Tools</b>: 
  * [libLAS](https://liblas.org/): reading & writing LAS   
  * [rapidlasso](https://rapidlasso.de/): LAS processing       
  * [GRASS](https://grasswiki.osgeo.org/wiki/LIDAR): LAS processing with QGIS      

### Computer Automated Design ([CAD](https://pro.arcgis.com/en/pro-app/latest/help/data/cad/what-is-cad-data.htm))    
Files from typical CAD software (AutoCAD & Microstation):   
  * .dxf (drawing exchange format): Platform-independent 2D & 3D vector files        
  * .dwg: AutoCAD 2D & 3D vector files      
  * .dgn: MicroStation 2D & 3D vector files    

---

## Data Transformation

Refers to transferring / converting geospatial data between formats -- Python objects, ESRI [geodatabases](https://pro.arcgis.com/en/pro-app/latest/help/data/geodatabases/overview/the-architecture-of-a-geodatabase.htm#GUID-739D940C-FD50-4F6F-8600-EBE39B00189A
), and other RDBMS such as [SQL Server](https://pro.arcgis.com/en/pro-app/latest/help/data/geodatabases/manage-sql-server/overview-geodatabases-sqlserver.htm). 


#### Data Converter: 
https://www.gisconvert.com/   

#### OSGEO GDAL
<b>Available [vector](https://gdal.org/drivers/vector/index.html) and [raster](https://gdal.org/drivers/raster/index.html) drivers</b>      
  
```ogr2ogr``` from OSGeo4W Shell:  

shp → gpkg: 
> ogr2ogr -f "ESRI Shapefile" "input.shp" "output.gpkg" "layer"

Postgres → gpkg:
> ogr2ogr -f PostgreSQL "PG:user=your_username password=your_pwd dbname=your_dbname" out_filename.gpkg

gpx → gpkg (for all gpx files in current directory):  
> for /R %f in (*.gpx) do ogr2ogr -f "GPKG" out_filename.gpkg "%f"



#### CAD ↔ SHP:  
  * DXF to shp [QGIS Plugin](https://docs.qgis.org/2.18/en/docs/user_manual/plugins/plugins_dxf2shape_converter.html)   
  * [DWG to shp](https://gisgeography.com/dwg-to-shp/)  



#### PostgreSQL ↔ Python (geopandas):  
Cursors are database objects that work with tables (for instance: reading or writing) one row at a time   
~~~
import pandas as pd
import psycopg2

def df_to_postgres(df, table_name, db, usr, pwd, localhost="localhost", port="5432"):
    try:
        conn = psycopg2.connect(database = db, user = usr, password = pwd, host = localhost, port = port)
        cur = conn.cursor()
        col_names = df.columns.to_list()
        for i in range(0 ,len(df)):
            values = tuple(df[col][i] for col in col_names)
            cur.execute("INSERT INTO {} ({}) VALUES({})".format(table_name, ", ".join(col_names), ", ".join(["%s"] * len(col_names))))
        conn.commit()

    except (Exception, psycopg2.Error) as error:
        print("Error while fetching data from PostgreSQL", error)
    
    finally:
        if conn:
            cur.close()
            conn.close()
            print("PostgreSQL connection is closed")

def postgres_to_df(SQL_query, db, user="postgres", pwd="", host="localhost", port=5432):
    try:
        conn = psycopg2.connect(database=db, user="postgres", password=pwd, host=host, port=port)
        cur = conn.cursor()
        cur.execute(SQL_query)
        items = cur.fetchall()
        hits=[]
        for row in items:
            hits.append(row)
        col_names = [desc[0] for desc in cur.description] 
        hits_df=pd.DataFrame(hits, columns=col_names)
        if ("lat" in col_names and "lon" in col_names):
            hits_gdf = gpd.GeoDataFrame(hits_df, geometry=gpd.points_from_xy(hits_df.loc[:,'lon'],hits_df.loc[:,'lat'], crs="EPSG:4326"))
            return hits_gdf
        else:
            return hits_df

    except (Exception, psycopg2.Error) as error:
        print("Error while fetching data from PostgreSQL", error)
    
    finally:
        if conn:
            cur.close()
            conn.close()
            print("PostgreSQL connection is closed")
~~~


---

## GIS Data Standards  
Improve geographic information's utility & value by increasing its interoperability, reusability, reliability, and access.   
* Example of [City of Fremont CAD standards](https://storymaps.arcgis.com/stories/9767345c01fc4fd5a6b90e970b249dbd)  

International Organization for Standardization (ISO) standards must be purchased. The American National Standards Institute (ANSI) serves as the US member agency to ISO and provides easier access to the standards and, generally, at a lower cost.   

<u> Open Geospatial Consortium (OGC)</u> is a diverse array of international groups (govt, academia, private, etc.) using geospatial data, settling on standards for sharing & integrating data.   
OGC publishes the following documents: 1) implementation standards, 2) abstract specifications, 3) best practices, 4) engineering reports, 5) discussion papers, and 6) change requests.  

Standards:  
* Data Encoding:  
    - [Geography Markup Language (GML)](http://opengeospatial.github.io/e-learning/gml/text/main.html)   
    - [Geopackage (.gpkg)](http://opengeospatial.github.io/e-learning/geopackage/text/introduction.html)   
* Data Access:  
    - [Web Feature Service (WFS)](http://opengeospatial.github.io/e-learning/wfs/text/basic-main.html)   
    - [Web Coverage Service (WCS)](http://opengeospatial.github.io/e-learning/wcs/text/basic-main.html#introduction)   
* Processing:
    - [Web Processing Standards (WPS)](http://opengeospatial.github.io/e-learning/wps/text/basic-main.html)  
* Visualization:  
    - [Web Map Service (WMS)](http://opengeospatial.github.io/e-learning/wms/text/basic-main.html)   
    - [Web Map Tile Service (WMTS)](http://opengeospatial.github.io/e-learning/wmts/text/main.html#introduction)   
* [Metadata and Catalogue Service](http://opengeospatial.github.io/e-learning/metadata/text/specifications.html)
</br>  

<u>Federal Geographic Data Committee (FGDC)</u> is a U.S. interagency group with the same mission 

* FGDC [standards list](https://www.fgdc.gov/standards/list) includes standards from FGDC, along with OGC and ISO

#### GIS metadata standards:  
- ISO 19115: Geographic information — Metadata  
- ISO 19139: Geographic information — Metadata — XML schema  
- [FGDC Content Standard for Digital Geospatial Metadata (CSDGM)](https://www.fgdc.gov/metadata/csdgm-standard) to Create System-level Metadata Records  

#### [Metadata creation best practices](https://www.usgs.gov/data-management/metadata-creation):   
* Gather all information together & reuse information that is already developed, e.g. abstract, purpose, date from grant or funding proposals
* Choose a descriptive title for your data that incorporates who, what, where, when, and scale.
* Choose keywords wisely -- consider all possible interpretations of your word choices.
* Include as many details as you can in the metadata record for future users of the data.
* Update the metadata date (date stamp) so that metadata repositories will know which version of the record is most recent.
* DOI should go in the primary <onlink> in the Citation Information section and should be a URL. 

#### Metadata validation:  
* Compares the metadata standard to the XML metadata record to ensure it conforms to the structure of the standard, such that all of the required elements are filled in.
* USGS best practices for [Checking Metadata with Data](https://d9-wret.s3.us-west-2.amazonaws.com/assets/palladium/production/s3fs-public/atoms/files/CheckingMetadataWithData_508-compliant.pdf) with FGDC-CSDGM metadata
* [USGS Metadata Parser (MP)](https://geology.usgs.gov/tools/metadata/tools/doc/mp.html) 
* [Metadata Wizard tool](https://code.usgs.gov/usgs/fort-pymdwizard)


---

## Publicly available data:  

* [Google Earth Engine](https://developers.google.com/earth-engine/datasets/catalog) + https://gee-community-catalog.org
* [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/catalog)
* [Planet Labs Basemaps](https://developers.planet.com/docs/basemaps/) 
* [USAID Spatial Data Repository](https://spatialdata.dhsprogram.com/home/)
* [US Govt](https://catalog.data.gov/)
* [USGS](https://data.usgs.gov/datacatalog/search)
* [USFS](https://data-usfs.hub.arcgis.com)
* [California](https://gis.data.ca.gov/) & [CA vegetation](https://wildlife.ca.gov/Data/GIS/Vegetation-Data)

### Google Earth Engine: Data Catalog & Cloud Computing   

#### Data:  
##### ee.FeatureCollection   

| category         |ee.FeatureCollection|
|------------------|---|
| Google buildings |"GOOGLE/Research/open-buildings/v3/polygons"| 

##### ee.Image

| category  |ee.Image| 
|-----------|---| 
| elevation |ee.Image("NASA/NASADEM_HGT/001").select(['elevation'])| 
| elevation |ee.Image("USGS/SRTMGL1_003").select(['elevation'])| 
| landcover |"projects/mapbiomas-public/assets/paraguay/collection1/mapbiomas_paraguay_collection1_integration_v1" | 
| soil      | "ISDASOIL/Africa/v1/fcc" | 
| soil      | "ISDASOIL/Africa/v1/cation_exchange_capacity" | 
| soil      | "ISDASOIL/Africa/v1/cation_exchange_capacity" | 
| soil      | "ISDASOIL/Africa/v1/clay_content" | 
| soil      | "ISDASOIL/Africa/v1/carbon_organic" | 
| soil      | "ISDASOIL/Africa/v1/bedrock_depth" |  

##### ee.ImageCollection

| name                                      |ee.ImageCollection|
|-------------------------------------------|---|
| US NLCD |  ee.ImageCollection("USGS/NLCD_RELEASES/2021_REL/NLCD").select("landcover") | 
| precip                                    |"UCSB-CHG/CHIRPS/DAILY"| 
| Sentinel-1                                |"COPERNICUS/S1_GRD"| 
| Sentinel-2 harmonized surface reflectance |"COPERNICUS/S2_SR_HARMONIZED"| 
| Sentinel-2 cloud probability              |"COPERNICUS/S2_CLOUD_PROBABILITY"| 
| MODIS LST                                 |ee.ImageCollection('MODIS/006/MOD11A1').select(['LST_Day_1km', 'LST_Night_1km', 'QC_Day', 'QC_Night']) | 
| Planet monthly basemaps                   |"projects/planet-nicfi/assets/basemaps/americas"| 
| Planet monthly basemaps                   |"projects/planet-nicfi/assets/basemaps/africa"| 
| Planet monthly basemaps                   |"projects/planet-nicfi/assets/basemaps/asia"| 
