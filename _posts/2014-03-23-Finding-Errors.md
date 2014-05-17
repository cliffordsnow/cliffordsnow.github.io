---
layout: post
title: "Finding Differences in Roads"
#tagline: "QGIS;PostGIS;Overpass"
description: "Using Open Source Tools to Find Differences in Road Data"
category: articles
tags: [QGIS;PostGIS;Overpass]
image:
  feature: missing.png
  credit: OpenStreetMap Contributors and Clifford Snow
---

Finding differences between OpenStreetMap and county road data is hard if done manually. Fortunately, Open Source Software tools eases the process.
This tutorial will provide you with one means of finding differences. The following software is needed:

*	[QGIS](http://www.qgis.org)
*	[PostGIS](http://)
*	[PGAdmin3](http://www.pgadmin.org/)
*	pgShapeLoader
*	[org2osm.py](https://github.com/pnorman/ogr2osm)

QGIS, PostGIS, PGAdmin3 and pgShapeLoader installation is beyond the scope of this tutorial. [Boundless](http://www.boundlessgeo.com) Open Geo Suite is the perfect solution to install PostGIS and related tools. 

I'm comparing Skagit County road center line shapefile data with OSM road ways. Fortunately, Skagit County's road names are spelled out instead of abrevated as most road data is presented. Skagit County's GIS data is open and freely available. Since most road data comes abrevated, you'll need to expand the road names to compare with OSM data. Postgresql funtions to expand road names can be found in my [github repository.](https://github.com/clifford/sql) Most likely you will need to modify the function for your data.


Download OSM Data
----
[Overpass-Turbo](http://overpass-turbo.eu) has an easy method to obtain current data. Modify and run the fullowing script:

```
     <osm-script output="json" timeout="900" 
element-limit="1073741824">
    <id-query {{nominatimArea:"Skagit County"}}             into="area"/>
    <!-- gather results -->
    <union>
     	<query type="node">
      		<has-kv k="highway"/>
      		<area-query from="area"/>
        </query>
        <query type="way">
            <has-kv k="highway" />
            <area-query from="area"/>
        </query>
    	<query type="relation">
      		<has-kv k="highway"/>
      		<area-query from="area"/>
    	</query>      
    </union>
    <!-- print results -->
    <print mode="body"/>
    <recurse type="down"/>
    <print mode="skeleton" order="quadtile"/>
    </osm-script>
```

Remember, change the nominatim search area from "Skagit County" to your county.

Once the query is complete, select Export from the menu. Select GeoJSON for the data type. It will take a few minutes before the download starts. Once complete move the file export.geojson to the data directory of your counties data. 

QGIS
---
Open the geojson vector file ![vector icon]({{site_url}}/assets/vector_icon.png) in QGIS. Select the LineString feature. 

![image]({{site_url}}/assets/qgis_geojson_import.png)

Select the OpenStreetMap in OpenLayers plugins menu item. Once open, drag the export to the top position, otherwise the OSM layer will obscure the geojson data. 

![QGIS Layers]({{site_url}}/assets/qgis_layers.png)

The last step with QGIS is to select the county roads using the Select Features by Rectangle tool. ![Rectangle Selection]({{site_url}}/assets/rectangle_selection_icon.png)  and save the layer as a vector file, in the Vector menu. 

![Save Vector Layer]({{site_url}}/assets/qgis_save_vector.png)

![Vector File]({{site_url}}/assets/qgis_save_vector_file.png)

Import into PostGIS
---
Use pgShapeFile to import the saved shapefiles into PostGIS. 


 
---


![HTTPS]({{site_url}}/assets/josm_https.png "HTTPS in JOSM")



