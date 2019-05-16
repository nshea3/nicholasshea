---
title: "Mapping in Python"
date: 2019-05-03T17:43:28-07:00
---

Every day I use more and more spatial data in my projects. I have a few different Python mapping packages to handle spatial visualization and I figured I would summarize my experience with them. 

[Link to git repository](https://github.com/nshea3/athabasca-data)

### The dataset

This dataset is drillhole collar coordinates for exploration holes in the Athabasca oil sands in northern Alberta. The coordinates can be found [here](https://gist.github.com/JustinGOSSES/61fbdedec03f936a58daedf5d010cf5a). The government of Alberta released the coordinates along with well log data I will likely analyze in another post. 

### First up: Folium

[Folium](https://github.com/python-visualization/folium) is a Python package that uses Leaflet.js to provide interactive visualizations of data in Python. It has a number of neat features, including inline, interactive map rendering in Jupyter notebooks, and save-to-HTML functionality. The syntax is surprisingly succinct; the example below creates a basemap and plots 2193 drillhole collars in the Athabasca oil sands.

~~~
well_center_coord = [55.736558, -112.615421]

map_wells = folium.Map(location=well_center_coord, zoom_start=7,tiles='cartodbpositron', width = 640, height=480)

for index, row in well_locations.iterrows():
  folium.CircleMarker(location=[row['lat'], row['lng']], radius=1).add_to(map_wells)

map_wells
~~~

The interactive plot means you are free to zoom in on interesting areas and then look at the global distribution without generating a whole new figure. 

<iframe width="640" height="480" src="https://www.nicholasshea.com/posts/plot_data.html" frameborder="0" allowfullscreen></iframe>

My only complaints so far are how it deals with huge amounts of points (the HTML file is huge and slow to render), and the fact that you can't save a static image of the map. This also limits how the map is displayed when the notebook is hosted, since if it isn't interactive the map will not render. I resorted to screenshotting the interactive map for display in the notebook, which obviously isn't the best solution. The convenience of having an interactive map  is hard to beat though, and you can add even more interaction features with tooltips and data selection/interrogation in the interactive map, using `Map.add_child(folium.LatLngPopup())` and related methods. And you can also choose among a variety of basemaps with the `tiles` argument to `folium.Map`:

<iframe width="640" height="480" src="https://www.nicholasshea.com/posts/plot_data_2.html" frameborder="0" allowfullscreen></iframe>

Unfortunately I have not had any luck using popups, I think that would be really useful for my work but I just can't get it to work. I understand there are some issues with special characters and possibly version problems as well so I will keep an eye out for that feature.

### Bokeh

Bokeh seems to have a lot of the same advantages/disadvantages as Folium, though their mapping offering is not as mature and feature-rich. I played around with it a bit and I prefer Folium. 

### matplotlib

I use matplotlib's inline plotting nearly every day, so I was hopeful for this one. Unfortunately, the plotting functionality is built into a different package, `mpl_toolkits.basemap`. I had issues with dependencies and was not able to get native plotting to work. I called it a day after an hour or two of wrangling with dependencies and pip/conda errors, and several questions on stackoverflow indicate this is an issue for other users as well. Hopefully the install procedure is fixed, as I'd love to give this one a try.

### Geopandas

Geopandas is similar to pandas in plotting capabilities. The following snippet of code will plot the well locations atop a basement rock geologic map of the region.

~~~
from shapely.geometry import Point, Polygon

bedrock_shp = gpd.read_file("data/MAP_600/DIG_2013_0018/bdrk_py_ll.shp")

geom = [Point(xy) for xy in zip(well_locations['lng'],well_locations['lat'])]
geo_df = gpd.GeoDataFrame(well_locations, geometry =geom)
geo_df.head()

ax = bedrock_shp.plot(cmap='Dark2', figsize=(20,40))

minx, miny, maxx, maxy = geo_df.total_bounds
ax.set_xlim(minx, maxx)
ax.set_ylim(miny, maxy)

geo_df.plot(markersize=20, ax=ax, color="white")
~~~

![Map with geologic basemap](https://i.imgur.com/FxuyWIB.png)

Geopandas simplifies work with shapefiles and other more GIS-friendly formats, and can output in those formats or output static images. Geopandas also gives much more control over coordinate systems and the details surrounding projections and mapping. Of course, it is non-optional, so you will not be able to visualize your data if you don't know exactly which CRS it's in. 

I also appreciate the fact that you can use a basemap from a tile server as a figure background:

~~~
import contextily as ctx

def add_basemap(ax, zoom, url='http://tile.stamen.com/terrain/tileZ/tileX/tileY.png'):
    xmin, xmax, ymin, ymax = ax.axis()
    basemap, extent = ctx.bounds2img(xmin, ymin, xmax, ymax, zoom=zoom, url=url)
    ax.imshow(basemap, extent=extent, interpolation='bilinear')
    # restore original x/y limits
    ax.axis((xmin, xmax, ymin, ymax))

add_basemap(ax, zoom=8)
~~~

![Map with tile basemap](https://i.imgur.com/dxRIOxd.png)

Be sure to set the `zoom_level` to something appropriate, as the figure won't properly render otherwise (and it'll increase the load on the tile server too).

### Conclusions:

* For first-pass visualization and interactive display, I’d use folium. 
* If I were looking to share, display, or publish my data, I’d use geopandas. 
* If I needed to do anything beyond that, especially any work with more complex figures, maps, or data formats, I’d probably start looking at QGIS (more on that in a later blog post)

I’m sure my views on this will evolve as I work with even more spatial data, so I’ll likely return to this topic in the future. 

### Sources:

* [GeoPandas 101: Plot any data with a latitude and longitude on a map](https://towardsdatascience.com/geopandas-101-plot-any-data-with-a-latitude-and-longitude-on-a-map-98e01944b972)

* [GeoPandas](http://geopandas.org/index.html)

* [Bedrock Geology of Alberta (GIS data)](https://open.alberta.ca/opendata/0066c922-244e-406a-96fd-d02f659bfc97#summary)

* [Essential geospatial Python libraries](https://medium.com/@chrieke/essential-geospatial-python-libraries-5d82fcc38731)

* [Mapping tools for data scientists](http://www.marknagelberg.com/overview-python-and-non-python-mapping-tools-for-data-scientists/)


