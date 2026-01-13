# Safe Routes to School

## Purpose

Safe Routes to School is a program designed to help parents encourage their children to walk and bike to school safely, while promoting healthy engagement. In some locations, walking or biking to school is a child's only means of getting to school. The OpenStreetMap (OSM) goal is to help parents find the best routes to school and to assist them in working with local governments to improve safety.

## What is needed

* Pedestrian and bike maps
* Routing engines* Walking and biking Isochrones
* Instructions on how to map for pedestrians and cyclists
* Help for SRTS groups on how to use OSM to improve infrastructure in their local communities

## Pedestrian and bike maps

Bike maps already exist. Not only does OSM offer two different map layers for cyclists, but there are several apps available. Pedestrian maps are a different story. While there are some pedestrian maps, such as the University of Washington's Taskar Center for Accessible Technology's [AccessMap.app](http://AccessMap.app), they are limited. What is needed is a tool that parents can use to find a good walking route to school, as well as a tool that can help improve pedestrian mapping, much like OpenStreetMap US's [OpenTrailMap.us](http://OpenTrailMap.us). The rendering should show pedestrian ways, crossings, accessibility features like tactile pads and kerb ramps,

## Routing Engines

OSM has some great routing engines. The user interface will likely need to be improved so that features can be added to avoid. For example, railways may be dangerous for children to cross. By allowing the addition of features to be avoid, it's possible to provide a safe route.

## Walking and biking Isochrones

Good open-source isochrone maps are available. One of my favorites is Valhalla. Below is an example of an isochrone map of a local elementary school created using Valhalla in QGIS. It shows 5, 10, and 15 walk areas. However, there are two major problems with the isochrone. First, it uses streets with no sidewalks. It also crosses the Division Street Bridge, which the school district doesn't feel is safe for children to cross. If we add an isochrones feature to our pedestrian and bike map, it needs to be able to restrict the isochrones to only safe walking and biking routes.

![Walkshed](https://mycloud.snowandsnow.us/index.php/s/JR2LiJTRQkofDCw)

## Instructions on how to map for pedestrians and cyclists

Four main features need to be mapped: schools, pedestrian ways, cycleways, and traffic calming features. A how-to page, along with video tutorials are needed to help new mappers get started.

Schools’ buildings, parking, bus drop off areas, main entrance, and bike rakes need to be mapped. Emphasis needs to be placed on adding accessibility features for kids with disabilities. See <https://wiki.openstreetmap.org/wiki/Disabilities>

The OSM US Pedestrian Working Group has developed a
schema for mapping pedestrian ways. Footways, curb ramps, tactile pads, crossings, surface, width, and other features need to be mapped. I should note that the schema focuses on mapping sidewalks as separate ways, which is not universally accepted. My experience is that mapping sidewalks as a separate way produces better routing.

Bike mapping is well established in OSM. For SRTS, intersection details, like traffic signal mapping is important for the safety of the children.

Traffic calming features, such as speed bumps, traffic islands, choker points, etc, are used to slow vehicle speeds, making walking and biking safer. Additionally, highway classifications and speed limits on roads are needed to help pick safer streets for children to walk or bike to school.

## Final thought

Not only is mapping for SRTS important in helping parents get their kids to school safely, but it also helps document areas that need safety improvements. While local governments typically have a detailed inventory of sidewalks, curbs, and roads, they may not have put it together in one source like we do in OSM.

### Links:

Safe Routes: National Center for Safe Routes to School <https://www.saferoutesinfo.org/>

Federal Highway Administration's Guidance for the Safe Routes to
School Program website:
<https://www.fhwa.dot.gov/environment/safe_routes_to_school/guidance/#toc123542171>

Safe Routes Partnership website: <https://saferoutespartnership.org/>

Washington State Department of Transportation website:
<https://wsdot.wa.gov/business-wsdot/support-local-programs/funding-programs/safe-routes-school-program>

Seattle PDF:
<https://www.seattle.gov/documents/Departments/SDOT/SRTS/SeattleSafeRoutestoSchoolEngineeringToolkit.pdf>

Washington Safe Routes to School Network website:
<https://www.washingtonsaferoutes.org/>