---
layout: post
title: "Creating a USFS Roads Background Layer for JOSM in Mapbox"
#tagline: "OSM"
description: "This article explores my learning how to create a background layer in Mapbox for use in JOSM."
category: articles
tags: [osm]
image:
  feature: texture-feature-04.jpg
---

## Uploading large geojson to Mapbox
### convert to mbtiles with Tippecanoe
   tippecanoe -o usfs_roads.mbtiles usfs_roads.geojson
### upload using mapbox-cli
 mapbox upload --name USFS_ROADS glassman.tileset ~/ownCloud/OSM/usfs_roads.mbtiles 
## Styling with Mapbox Studio
### Questions
*  how do create a transparent background?
*  how to create casings on ways
*  how to publish the tiles so JOSM can read them

