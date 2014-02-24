---
layout: post
title: "Fixing Duplicates in OSM"
tagline: "Causes and Fixes"
description: "It is way too easy to create duplicate addresses in OSM with existing editor"
category: articles
tags: [address, duplicates, iD, JOSM]
image:
  feature: duplicates.png
  credit: Photo courtesy of USDA Natural Resources Conservation Service. 
---

The problem of duplicates addresses for King County can be categorized into two catogories.

User added addresses without checking for existing address points
--
It is easy to add a new Point of Interest and miss seeing the address node. Addresses display as simple nodes in iD and JOSM. While JOSM can be customized using map paint styles to display the full address, the feature is not enable by default.

The JOSM image below show an address node with default paint style displayed. The address node is displayed with the house number and a unique icon. 

![JOSM]({{site_url}}/assets/josm_address.png "JOSM")

iD on the otherhand only gives a icon of a node
![iD]({{site_url}}/assets/iD_address.png "iD")

Potential Fixes
----
* JOSM - Add an duplicate address check to the validator. Editors also need to be made aware of the problem. Since address nodes are visiable, making users aware of map paint styles should help. 
* iD - First the address node should have a unique icon style to help users spot them. This is an open ticket on [github.](https://github.com/openstreetmap/iD/issues/1524) When selected, the user interface should allow the editor to easily add POIs. Additionlly, a means to merge POIs with address nodes is needed. See ticket on [github.](https://github.com/openstreetmap/iD/issues/2137)

Duplicates imported from source
--
The latest King County address from 2/9/14 had 8,570 (2) duplicates. We believe that E911 might have unit numbers which would fix a number of problems. Other problems include bad data which OSM is well suited to fix.


