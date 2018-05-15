---
title: Visualize spatial data in maps using R and Python
tags:
  - spatial maps
  - R
  - Python
---
For spatial data analysis, visualizing the spatial patterns of the data is necessary. In many cases, a map is used as the background of the figure. This post summarizes several commonly used methods to make maps with R and Python.

<!--more-->
## 1. R
There have been many packages developed in R for plotting different maps. This post introduces the use of packages as follows which should meet the needs of most situations.

* **“maps”**: obtain map data, e.g., world map, country map, state map, etc.
* **“mapdata”**: extra map database that contains higher-resolution map data.
* **“ggplot2”**: a powerful tool for plotting various figures and can be conveniently used for map plotting.
* **“ggmap”**: an integrated package for obtaining map data, e.g., Google Maps, and plotting maps using the layered grammar of graphics implementation of “ggplot2”.

{% highlight r %}
library(maps)
library(mapdata)
library(ggplot2)
library(ggmap)
{% endhighlight %}

### 1.1 Basic maps using "ggplot2"
If people just want to create a map without other information on it, the map can be made easily using ggplot2 package. This post gives three examples showing how the outline-maps are created as follows.
* World Map

{% highlight r %}
world <- map_data("world") #obtain world map data
#plot world map
ggplot()+  
 geom_polygon(data = world, aes(long, lat, group = group), fill = NA, color = "black")+
 coord_quickmap()+
 theme_nothing()
{% endhighlight %}
<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/jay15summer/jay15summer.github.io/master/assets/images/visualize-spatial-map-world-R.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            World map.
        </div>
    </div>
</div>

* USA map
{% highlight r %}
usa_outline <- map_data("usa") #obtain the outlines map of usa
usa_states <- map_data("state") #obtain usa map containing states
#plot the outline usa
ggplot()+
 geom_polygon(data = usa_outline, aes(long, lat, group = group), fill = NA, color = "black")+
 coord_quickmap()+
 theme_nothing()
#plot usa map with states
ggplot()+
 geom_polygon(data = usa_states, aes(long, lat, group = group, fill = region), color = "black")+
 coord_quickmap()+
 theme_nothing()
 {% endhighlight %}
 <div class="card mb-3">
     <img class="card-img-top" src="https://raw.githubusercontent.com/jay15summer/jay15summer.github.io/master/assets/images/visualize-spatial-map-usa.png"/>
     <div class="card-body bg-light">
         <div class="card-text">
             U.S. outline map and states map.
         </div>
     </div>
 </div>

 * Florida Map
{% highlight r %}
states <- map_data("state") #obtain states map of usa
fl_state <- subset(states, region == "florida") #select florida state from all the states
#plot florida state outline map
ggplot()+
 geom_polygon(data = fl_state, aes(long, lat, group = group), fill = NA, color = "black")+
 coord_quickmap()+
 theme_nothing()
#=========================================================
counties <- map_data("county") #obtain counties map of usa
fl_county <- subset(counties, region == "florida") #select florida's counties from all the counties
#plot county map of florida state
ggplot()+
 geom_polygon(data = fl_county, aes(long, lat, group = group, fill = subregion), color = "black")+
 coord_quickmap()+
 theme_nothing()
{% endhighlight %}
<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/jay15summer/jay15summer.github.io/master/assets/images/visualize-spatial-map-fl.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            Florida map and its counties map.
        </div>
    </div>
</div>

**Comments:**

1. `map_data` is a function used for obtaining the outline data of certain maps. The data usually contains: `long`, `lat`, `group`, `order`, `region`, and `subregion` that basically “define” a map.

2. `ggplot` is the function that initiates the map plotting process for the subsequent layers.

3. `geom_polygon` is the main function that plots these outline maps. People can customize the map by changing `fill`, and `color`, etc.

4. `coord_quickmap` is used for projecting the spherical map data onto a 2D plane. It basically controls the aspect ratio of the map. There are also other functions can control the projection, e.g., `coord_map`.

5. `theme_nothing` is used for removing all the background theme (non-data display), e.g., axis, background color, etc. Other themes can be chosen via `theme_xxx`, e.g., `theme_bw`.

### 1.2 Maps with spatial information using "ggplot2": three examples
* point data: load the commonly used "ozone" data, and plot it with its corresponding locations/map:

{% highlight r%}
#==============point data==============
data(ozone)
states <- map_data("state") #obtain states map of usa
ggplot()+
  geom_polygon(data = states, aes(long, lat, group = group), fill = NA, color = "black")+
  geom_point(data = ozone, aes(x = x, y = y, size = median), color = "red")+
  coord_quickmap(xlim = range(ozone[,1]),  ylim = range(ozone[,2]))+ # zoom in on [xlim, ylim]
  theme_void()# empty theme with legend, theme_nothing() will strip legend as well.
{% endhighlight %}
<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/jay15summer/jay15summer.github.io/master/assets/images/visualize-spatial-map-point.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            Ozone point map.
        </div>
    </div>
</div>

* areal data: download and plot the GDP data of all the U.S. states in 2016 from [BEA](https://www.bea.gov/iTable/iTable.cfm?reqid=70&step=10&isuri=1&7003=200&7035=-1&7004=sic&7005=1&7006=xx&7036=-1&7001=1200&7002=1&7090=70&7007=-1&7093=levels#reqid=70&step=10&isuri=1&7003=200&7035=-1&7004=naics&7005=1&7006=xx&7036=-1&7001=1200&7002=1&7090=70&7007=-1&7093=levels)(The Bureau of Economic Analysis of the U.S. Department of Commerce)(the downloaded GDP data "gdp.csv" used in the following code is available [here](https://github.com/jay15summer/jay15summer.github.io/blob/master/assets/data/gdp.csv) with direct downloading link [here](https://drive.google.com/file/d/1at3A5iZZ_zA7TlFMXhwk_AXx48aBQsJR/view?usp=sharing)):

{% highlight r %}
#==============areal data===============
dat <- read.csv("gdp.csv", header = FALSE)
GDP2016 <- data.frame(tolower(as.character(dat$V2[7:65])), as.numeric(dat$V22[7:65]), stringsAsFactors=FALSE)
names(GDP2016) <- c("region","GDP")
GDPMap <- merge(GDP2016, states, by = "region")
ggplot()+
  geom_polygon(data = GDPMap, aes(long, lat, group = group, fill = GDP), color = "white")+
  #coord_quickmap()+
  coord_map("albers", parameters = c(45.5, 29.5))+
  theme_void()+scale_fill_gradientn(colours = cm.colors(7),
                                   breaks = c(20000, 40000, 100000, 500000, 1000000, 1500000),
                                   trans = "log")
{% endhighlight%}
<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/jay15summer/jay15summer.github.io/master/assets/images/visualize-spatial-map-areal.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            U.S. states GDP map.
        </div>
    </div>
</div>

* path data: plot an navigation route from San Francisco to Los Angeles. The route data can be easily obtained from the "ggmap" package using function `trek`:

{% highlight r %}
#========obtain and plot path data using "ggmap"===============
trek_df <- trek("san francisco, california", "los angeles, california", structure = "route")
qmap("california", zoom = 7) +
  geom_path(
    aes(x = lon, y = lat),  colour = "blue",
    size = 1.5, alpha = .5,
    data = trek_df, lineend = "round"
  )

{% endhighlight %}
<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/jay15summer/jay15summer.github.io/master/assets/images/visualize-spatial-map-path.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            Path plot from San Francisco to Los Angeles.
        </div>
    </div>
</div>

**Comments:**
1. `theme_void()` creates an empty theme with the legend on, and `theme_nothing()` will strip the legend as well.
2. "ggmap" is a convenient package for retrieving map data from popular online mapping services, and plotting various types of maps under the "ggplot2" framework. Its GitHub repository is [here](https://github.com/dkahle/ggmap).

## 2. Python
The most commonly used map plotting package in Python is **"Basemap"** from **"Matplotlib"**. Basemap needs to be additionally installed as it is not included in Matplotlib. The installation steps can be found in its [GitHub page](https://github.com/matplotlib/basemap) and [documentation page](https://matplotlib.org/basemap/index.html). If you use "Anaconda", installing Basemap is easy by using Anaconda's Navigator GUI or simply using the command `$ conda install basemap`.

There have been many helpful tutorials about Basemap. Therefore, this post will not describe the use of Basemap in details. Instead, the following two links are two recommended tutorials:
* [Basemap tutorial](http://basemaptutorial.readthedocs.io/en/latest/index.html);

* [Basemap user's guide](https://matplotlib.org/basemap/index.html#).

Lastly, the shapefile of various maps can be freely downloaded from many websites, and then plotted using Basemap. A collection of websites for downloading shapefiles is summarized [here](https://www.statsilk.com/maps/download-free-shapefile-maps). Additionally, an example of plotting a basic map using Basemap is:
{% highlight python %}
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt

map = Basemap()

map.drawcoastlines()

plt.show()
{% endhighlight %}
<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/jay15summer/jay15summer.github.io/master/assets/images/visualize-spatial-map-world-Python.png"/>
    <div class="card-body bg-light">
        <div class="card-text">
            World outline map by Basemap.
        </div>
    </div>
</div>
