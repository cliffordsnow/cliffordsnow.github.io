---
layout: post
title: "JOSM Background Layer"
#tagline: "Tilestream;JOSM"
description: "Easy way to server tiles locally"
category: articles
tags: [QGIS;github;drone]
image:
  feature: texture-feature-04.jpg
---

Now that we can find missing roads with the plan developed in [Finding Errors]({{site_url}}/articles/Finding-Errors) it is time to move on to aligning the roads.

Up until now, the easiest way was to convert the roads shapefile into an .osm layer for JOSM. As the image below shows, aligning roads using Bing Imagery and the .osm layer works just fine. Until you want to check road name. The .osm layer doesn't display the name or any other attribute for that matter.

![JOSM with OSM Background]({{site_url}}/assets/josm_osm_background.png)

Using a tile background solves that problem. Looking at the image below, the road name is displayed along side for easy comparison to OSM data.

![JOSM using Tiles in the Background]({{site_url}}/assets/josm_tilestream_background.png)

Here is what is needed to create your own backgrounds for JOSM.

* [TileMill](https://www.mapbox.com/tilemill/) for creating tiles
* [TileStream ](https://github.com/mapbox/tilestream)for serving up the tiles
* POSTGIS connection to road data

Check out TileMill [documentation](https://www.mapbox.com/tilemill/docs/manual/) for help installing and creating tiles. 

<!-- language: lang-js -->
	#skagitroads {
  		line-width:5;
  		line-color:#00ff00;
  		line-cap: round;
 	*/
  

 	::labels[zoom > 13]{
  		text-name: [fullname];
  		text-face-name: 'Helvetica Bold';
  		text-fill: #fff;
  		text-placement: line;
  		text-dy: 12;
   		text-size:14;
		}
  	}
  	
Tilestream was easy to install. My only hangup was to update Homebrew before starting. 

TileMill's default is to save the tiles in my ~/Documents/MapBox/export folder. Move the tiles.mbtiles file to ~/Documents/MapBox/tiles. You could create a symbolic link but I just moved the files.

Start Tilestream
	./index.js

Open localhost:8888 in your browser to verify that everything is working. Select your new tiles. Once open, click on Info to get the tile URL to paste into JOSM.

![Tilestream URL]({{site_url}}/assets/tilestream_url.png)

In this case the url is 
	http://localhost:8888/v2/SkagitCountyRoads/{z}/{x}/{y}.png

Finally, enter the tile url into JOSM. Select the ![TMS]({{site_url}}/assets/josm_tms.png) icon to add your new tiles to JOSM.

![JOSM add TMS]({{site_url}}/assets/josm_add_tms.png)


















