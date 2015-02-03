---
layout: post
title: "Prompt for OSM User ID in JOSM:Using a Mac"
#tagline: "JOSM Vernon;applescript;OSM"
description: "Applescript Code for a JOSM prompt"
category: articles
tags: [applescript,JOSM]
image:
  feature: applescript.png
  credit: Brandon Titus
---
Mac OSC Prompt for My User ID in JOSM
---
I'm doing an import of Kirkland Buildings and Addresses into OSM. I wanted an easy way to remember to use the right id

~~~ applescript
set pList to (choose from list {"UserID", "UserID_Import"} with title "Which UserId?" with prompt "Select User ID")if pList is false then	display dialog "Canceled" with icon stopelse if pList contains "UserID" then	do shell script "cp /Users/cliffordsnow/Development/Info.plist.normal /Applications/JOSM.app/contents/Info.plist"	tell application "JOSM" to activateelse if pList contains "UserID_Import" then	do shell script "cp /Users/userid/Development/Info.plist.import /Applications/JOSM.app/contents/Info.plist"	tell application "JOSM" to activateend if
~~~
<br>

Create Info.plist
---
Create a Info.plist for each id you want to use. The easiest way is to run JOSM using the desired id. Close JOSM and copy the file /Applications/JOSM.app/Contents/Info.plist to your desired location. I picked my Developement folder. 

Compile the applescript into a new application. Using the Applescript Editor, export the script as an Application. I called my new JOSM script, MyJOSM.

![Applescript]({{site_url}}/assets/applescript.png "Create Script Application")

  








