---
layout: post
title: "Sidewalks of Mount Vernon Washington"
#tagline: "Mount Vernon;sidewalks;OSM"
description: "Walking in Mount Vernon"
category: articles
tags: [QGIS;postgis,tilemill,JOSM]
image:
  feature: sidewalk.png
  credit: Cindy Zackowitz
---
Walkable City Part 1
---
Just how walkable is Mount Vernon, WA. Anyone that lives in Mount Vernon knows that the city is mostly flat, except for the Southeast corner of the city. So easy to walk, except for some steep climbs in the Southeast and spotty sidewalks. 

Not much can be done with the hills, but routes can be designed to avoid hills, at least as much as possible. Ideally routes that use sidewalks and paths instead of walking in the street. 

The project requires mapping all sidewalk and paths in Mount Vernon. In the next article we will look at extracting the free data from OpenStreetMap (OSM). We will building tiles using TileMill from the OSM data and LIDAR DEM bare-earth for hill shading. Then serving the tiles in a tile server. 

Mapping Sidewalks
---
There are two basic method of mapping sidewalks in OSM. One method is to draw a separate way for each sidewalk. The other is to tag the road with sidewalk=both/right/left/none. The first has the advantage of being easy to create and is very editable. Its biggest disadvantage is the sidewalks are not as easy to create routes. Since sidewalks do not have street names, directions can not be given as turn left on the James Street Sidewalk. The other method, tagging each street with sidewalk=* is easy to create and work well for routing by foot. The disadvantages are first, streets often have to be broken into small segments to match the sidewalk. Second, it is not clear when a path is needed to connect routes. More about this later.

JOSM
--
Visualizing sidewalks is done with the sidewalk mapcss style. Enable it in the preference screen as shown below.

![MAP CSS]({{site_url}}/assets/mapcss.png "JOSM Map CSS Preferences")

Tag each highway with sidewalk=both/left/right/none to have it displayed in the editor. JOSM now shows if a sidewalk exists. The only problem is if there is no sidewalk, nothing is displayed.

![Sidewalks in JOSM]({{site_url}}/assets/josm_sidewalks.png "Sidewalks mapped in JOSM")

 

Complex Sidewalks
--
One of the issues using the tag sidewalk=* is connecting routes. For example, in the image below, streets coverage at a railroad crossing. I decided to use dedicated paths to show the correct pedestrian route.

![Complex Sidewalks in JOSM]({{site_url}}/assets/complex_sidewalk.png "Complex Sidewalks mapped in JOSM")

Tasking Manager
---
Mapping individual sidewalks in a city even as small as Mount Vernon, WA is a big task. I used the [Tasking Manager](http://tasks.openstreetmap.us/job/40) to break the city into 82 squares. The Tasking Manager is perfect for breaking large jobs into small manageable chunks. If you decide to use the Tasking Manager, you'll need to contact the administer for permission to create tasks.

Oops
---
It is easy to miss editing every street. Some are small and hard to spot. Others are lost in areas with streets tagged sidewalk=none. Once the all the tasks in the Tasking Manager are complete, use []Overpass](http://overpass-turbo.eu) and QGIS to find missed roads. 

`
/*
This has been generated by the overpass-turbo wizard.
The original search was:
“highway=residential in "Mount Vernon, Skagit County"”
*/
[out:json][timeout:25];
// fetch area “Mount Vernon, Skagit County” to search in
{{geocodeArea:Mount Vernon, Skagit County}}->.searchArea;
// gather results
(
  // query part for: “highway=residential”

  way["highway"="residential"](area.searchArea);
  way["highway"="primary"](area.searchArea);
  way["highway"="secondary"](area.searchArea);
  way["highway"="road"](area.searchArea);
  way["highway"="tertiary"](area.searchArea);
  way["highway"="tertiary_link"](area.searchArea);

);
// print results
out body;
>;
out skel qt;
`


Export results as a geojson and open in QGIS. Filter the results to eliminate all sidewalks. "sidewalk" **is null**. Use OSM as a bottom layer to easily see the missed roads. 

Next Steps
---
Once all of the streets have been tagged it is time to display the results. We will look at that in Part 2. See you then.




