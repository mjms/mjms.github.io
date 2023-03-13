---
layout: post
title: 65th St and Woodlawn Community Garden
date: 2023-03-12
description: The start of a series on our journey of growing sustainably in a 10x10 plot
tags: gardening code
categories: 65th-woodlawn-series
---

On April 10th 2021, my partner and I joined [The 65th st and Woodlawn Ave Community Garden](https://www.65thandwoodlawn.com/).

To celebrate two years of being part of this incredible place, I will be posting a series this month about the things we learned along the way.
<br>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/posts/post-65th-and-woodlawn/april-10-2023.jpg" class="img-fluid rounded z-depth-1" caption = "April 10, 2021" zoomable=true%}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/posts/post-65th-and-woodlawn/aug-13-2021.jpg" class="img-fluid rounded z-depth-1" caption = "...5 months later on August 13, 2021" zoomable = true%}
    </div>
</div>

I will also be using this space to explore and learn about handling and visualizing spatial data in Python, finetuning image classification models, and other fun projects involving coding, data, and gardening.

Follow along this month, as I talk about how to use climbing wall hardware to build a trellis, hand knitting a biodegradable mesh for pole beans, and the wonders of the stiff goldenrod!

<br>
<hr>
<br>
### Looking at historical images of 65th and Woodlawn

<br>
To kick us off this series, I want to look at how the garden has changed over the years.

[`geemap`](https://geemap.org/) makes it easy to visualize and interact with datasets from Google Earth Engine in Python. It has functionality for interactive maps, as well as creating time series and timelapses from Google Earth datasets using the built `timelapse` functions. There are also a lot more features and in-depth tutorials on [`geemap`](https://geemap.org/)`, as well as documentation for the API found [here](https://geemap.org/)

I will be following the [`geemap`](https://geemap.org/) <b>[tutorial](https://geemap.org/notebooks/90_naip_timelapse/)</b> to create a timelapse of the garden from 2005 to 2019 from dataset from the National Agriculture Imagery Program ([NAIP](https://naip-usdaonline.hub.arcgis.com/)) 


In a Jupyter notebook, import the Google Earth Engine Python API and [`geemap`](https://geemap.org/)

{% highlight python linenos %}

# Google Earth Engine

import ee

# Trigger the authentication flow.
ee.Authenticate()

# Initialize the library.
ee.Initialize()

# import geemap
import geemap

# import os, and path to save files to an output folder 
import os
from os.path import dirname, join as pjoin

output_folder = "output"
{% endhighlight %}

The coordinates of the garden (and of other locations, if you have more than one region of interest) are stored in a dictionary like this
{% highlight python linenos %}
coords = {
"<location_name>": {
"lon": <longitude in decimal degrees>,
"lat": <latitude in decimal degress>,
"scale": <scale in meters>
},
"<another_location_name>": {
"lon": <longitude in decimal degrees>,
"lat": <latitude in decimal degress>,
"scale": <scale in meters>
}
...
}

{% endhighlight %}

We use the [`ee.Geometry.Point.buffer`](https://developers.google.com/earth-engine/apidocs/ee-geometry-point-buffer) to draw a circle centered around the coordinate point with the radius given by the `scale` to define the region of interest (ROI).

Let's check if we have the correct coordinates and scale of the ROI is correct.
{% highlight python linenos %}
Map = geemap.Map()
Map
location_name = 'community_garden'
lon = coords[location_name]["lon"]
lat = coords[location_name]["lat"]
scale = coords[location_name]["scale"]
geom_point = ee.Geometry.Point(lon,lat)
roi = geom_point.buffer(scale)
Map.addLayer(roi)
Map.centerObject(roi)
Map
{% endhighlight %}

<div align="center">
 {% include figure.html path="assets/img/posts/post-65th-and-woodlawn/geemap-screenshot.png" class="img-fluid rounded z-depth-1" zoomable=true%}
</div>

Looks good! Now let's get the images from the dataset
{% highlight python linenos %}
# create a time series from the NAIP image collection 
im_col = geemap.naip_timeseries(roi,start_year=2005,RGBN=True)
images = im_col.toList(im_col.size())

# Get dates
dates = geemap.image_dates(im_col).getInfo()
size = images.size().getInfo()

# add images to Map
for i in range(size):
    image = ee.Image(images.get(i))
    Map.addLayer(image, {'bands': ['R','G','B']}, dates[i][:4],shown=False)

{% endhighlight %}

and finally, create the timelapse

{% highlight python linenos %}
timelapse = geemap.naip_timelapse(
    roi, start_year=2005, out_gif=pjoin(output_folder,f"{location_name}-{scale}m-naip.gif"), bands=['R','G','B'], frames_per_second=1,fading=1,)
geemap.show_image(timelapse)
{% endhighlight %}

<div align="center">
 {% include figure.html path="assets/img/posts/post-65th-and-woodlawn/community_garden-200m-naip.gif" class="img-fluid rounded z-depth-1" zoomable=true %}
</div>

Find the Jupyter Notebook to create this timelapse [here](https://github.com/mjms/65th-woodlawn/blob/main/make_timelapse/make_timelapse.ipynb)!
