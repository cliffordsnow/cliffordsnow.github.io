---
layout: post
title: Duplicate addresses in Seattle
category: articles
tags: osm
---

It was pointed out that Seattle has a number of duplicate addresses in OSM. Running a query in overpass convinced me that there were more than anticipated. 

The overpass query run on overpass-turbo.eu

{% highlight XML linenos %}
{% raw %}
    <osm-script output="json" timeout="900" element-limit="1073741824">
      <id-query {{nominatimArea:Seattle}} into="area"/>
      <!-- gather results -->
      <union>
        <query type="node">
          <has-kv k="addr:housenumber" />
          <has-kv k="addr:city" v="Seattle" />
          <!-- <has-kv k="source" v="King County GIS" /> -->
          <area-query from="area"/>
        </query>
      </union>
      <!-- print results -->
      <print mode="body"/>
      <recurse type="down"/>
      <print mode="skeleton" order="quadtile"/>
    </osm-script>
{% endraw %}
{% endhighlight %}

Some duplicates can easily be fixed by removing the duplicate. However, King County lables many buildings with the same address, such as mobile home parks. These need a add:unit tag added. 


 