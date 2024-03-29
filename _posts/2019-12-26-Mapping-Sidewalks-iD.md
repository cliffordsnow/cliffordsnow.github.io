---
layout: post
title: "Mapping Sidewalks with iD a HowTo"
#tagline: "iD;footways;OSM"
description: "Detailed instructions on how to map sidewalks, curbs, crosswalks, etc. in iD for pedestrian routing"
category: articles
tags: [footways,iD]
image:
  feature: sidewalks_pic.png
  
---
How to Manually Map Sidewalks as Separate Ways
---
This guide will help you map your cities sidewalks as separate ways using the iD editor. My previous post was mapping sidewalks using JOSM. 

The goal is to build a network of routable sidewalks, especially for people with limited mobility. [AccessMap.io](https://accessmap.io) show the power of OSM to help people navigate their city on foot or in a wheelchair.

While I have you here, I want to give a shoutout to the University of Washington's [Taskar Center for Accessible Technology](https://tcat.cs.washington.edu/) . The director, Anat Caspi and project lead, Nick Bolton, were the ones that convinced me that we need to change how we map pedestrian ways. They developed the [OpenSidewalk Project](https://opensidewalks.com) and [AccessMap.io](https://accessmap.io). They are the inspiration behind mapping sidewalks in OSM. 

### Tools you'll need 

1. iD - personnally I like JOSM for editing but iD is well suited to mapping sidewalks.
2. [Tasking Manager](https://tasks.openstreetmap.us) to help break the area into manageable chunks.
3. Good satellite imagery
4. Street level imagery which can be Bing StreetSide, OpenStreetCam or Mapillary. The last two allow you to capture the street level imagery from your car, bike and even walking.
5. Tasking Manager to break the collections into small chunks
6. See my previous article on how to evaluate the sidewalk network.

### Sidewalk terms

1. **footway**. What we call sidewalks in the US is called a [footway](https://wiki.openstreetmap.org/wiki/Tag:highway%3Dfootway) in England where OSM got it start. A footway is a pedestrian path between any two points. `highway=footway`
2. **sidewalks**. A [sidewalk](https://wiki.openstreetmap.org/wiki/Tag:footway%3Dsidewalk) is a footway that run parallel to a street. `highway=footway + footway=sidewalk`
3. **crossing**. A street [crossing](https://wiki.openstreetmap.org/wiki/Key:crossing) is either a marked or unmarked crossing of a street. `highway=footway + footway=crossing + crossing=marked|unmarked` 
4. **Marked/Unmarked** Any crossing that is marked on the street should be tagged as `crossing=marked`. The marking can be just two parallel lines, stripping, or even intricate patterns. This interpretation differs from the wiki which is confusing.
5. **crossing islands**. Crossing island are small places usually between two lanes of traffic. Tag the short way as `crossing:island=yes`<br>![Traffic Island]({{site_url}}/assets/traffic_island.png "Traffic Island")
6. **curbs**. In British English its [kerb](https://wiki.openstreetmap.org/wiki/Key:kerb). There are many flavors of kerbs. Here are some of the common ones you'll likely see:

*  **Lowered**   	 A lowered curb cut should be wide enough for a wheelchair to use. There should be no more than a 1 inch difference between the street and the curb. also referred to as a sloped curb or curb ramp.  	 `kerb=raised`  	 ![lowered curb]({{site_url}}/assets/Lowered_curb.png "Example of a lowered curb") 
*  **Incline** An attempt to create a lowered curb. Using JOSM to measure the length and estimate the height of the curb to determine [incline](https://wiki.openstreetmap.org/wiki/Key:incline). Most curbs are 6" high but not all. Split the way at the end of the regular sidewalk. Draw the way to indicate movement upward. `highway=footway` + `footway=sidewalk` + `incline=8%` ![asphalt lowered curb]({{site_url}}/assets/Asphalt_lowered_curb.png "Example of a ashpalt lowered curb")  
*  **Flushed**   	  A flush curb is level with the pavement  	  `kerb=flush`  	 ![flush curb]({{site_url}}/assets/Flush_curb.png "Example of a flush curb") 	 
*  **None**  	  If there is no curb, tagging the end of the footway with   	 `kerb=no` 
*  **Raised** A curb with more than a 1 inch difference with the street. `kerb=raised` ![raised curb]({{site_url}}/assets/Raised_curb.png "Example of a raised curb")  
*  **Rolled** Rolled curbs still provide a gutter for water while being traversable by large wheeled vehicles, such as cars and bicycles, but not wheelchairs  `kerb=rolled` No image available



Mapping
-----
##### Sidewalks
A good place to start is to map sidewalks in city blocks around one intersection before adding the crossings. If the imagery is sufficiently sharp you should be able to easily add the sidewalks. Occasionally you'll need to consult street level imagery to see below tree and other blocked views. 

![Add Sidewalks]({{site_url}}/assets/add_sidewalk.png "Just sidewalks mapped")

The next logical step would be to add curbs. This is where street side imagery is needed. iD has integrated the three street side packages into the editor.
 
##### Curbs
Determine if a curb ramp exists and if so, what type and is there a tactile pad. Adding the tactile pad is important for people with vision impairments. Adding a short footway between the curb with a ramp and the sidewalk would be a good idea. I don't, basically because marking a curb ramp in the footway doesn't impact routing for people with limited mobility and since most curb ramps extend into the way, it's a good signal to someone with vision impairments that they reached a curb ramp.

![Add Curb]({{site_url}}/assets/curb_ramp.png "Curb ramp")
![Raised Curb with Step]({{site_url}}/assets/raised_curb_steps.png "Raised curb - this one with steps")

![Tactile Pad]({{site_url}}/assets/tactile_pad.png "Tactile Pad")

##### Crosswalk
Next add the crosswalks. Use `highway=footway` + `footway=crossing` + `crossing=marked` when the intersection is marked for pedestrians or `crossing=unmarked` when the crossing isn't marked. Include a pedestrian crossing node where the street intersects with the crosswalk. It's purpose is to notify vehicles of the crosswalk. While you are there, check for stop signs and traffic lights to add to OSM.

![Add Crosswalk]({{site_url}}/assets/add_crosswalk.png "Completed crosswalk mapping")
![Raised Curb]({{site_url}}/assets/raised_curbs.png "How to map raised curbs")
#### Traffic Island
If there is a island between lanes of traffic, add a way, ```crossing:island=yes```![Traffic Island]({{site_url}}/assets/mapped_traffic_island.png "Traffic island mapping")

##### Wheelchair Ramps
This is a special case where there is a wheelchair ramp, usually to a business. It should be mapped as `highway=footway` + `incline=x%`. Use JOSM to measure the length of the way and estimate the height to calculate the percent incline.
![Wheelchair_ramp.jpg]({{site_url}}/assets/Wheelchair_ramp.jpg "By Lionel Allorge - Own work, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=27859568")


Mapping Tips
----

* Mark sidewalks that end without access to the street as ```kerb=no```
* Mark sidewalks that end in the yard with ```kerb=no```
* If the sidewalk has a raised curb, add an extension to the sidewalk otherwise the router will thing their is a raised curb preventing wheelchair routing. ![Improper Raised Curb]({{site_url}}/assets/improper_raised_curb.png "Don't do this")
* Remove any existing footway that connects directly to the road without a crossing. Remember, we are trying to keep pedestrians on the sidewalk.
* Include steps and ramps
* Indicate obstruction areas that block wheelchair access with ```wheelchair=no``` ![Obstructions]({{site_url}}/assets/Obstruction.png "Obstruction in footway")
* Add surface=* especially if the surface is gravel or other material that would impair or prohibit wheelchair access.
* If working from Tasking Manager, pick a strategy, such as working blocks from south to north and east to west. This will help you not miss intersections. 
