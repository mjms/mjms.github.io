---
layout: post
title: 65th St and Woodlawn Community Garden
date: 2023-03-12
description: The start of a series on our journey of growing sustainably in a 10x10 plot
tags: gardening code
categories: 65th-woodlawn-series
---

On April 10th 2021, my partner and I joined The 65th st and Woodlawn Ave Community Garden.

To celebrate two years of being part of this incredible place, I will be posting about some of the things we learned along the way.

Follow along this month, as I talk about how to use climbing wall hardware to build a trellis, hand knitting a biodegradable mesh for pole beans, and the wonders of the stiff goldenrod!

I will also be using this space to explore and learn about handling and visualizing spatial data, and finetuning image classification models.

<br>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets\img\posts\post-65th-and-woodlawn\april-10-2023.jpg" class="img-fluid rounded z-depth-1" caption = "April 10, 2021" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets\img\posts\post-65th-and-woodlawn\aug-13-2021.jpg" class="img-fluid rounded z-depth-1" caption= "...5 months later on August 13, 2021" %}
    </div>
</div>

<hr>
<br>
### Looking at historical images of 65th and Woodlawn

<br>
We will use [Google Earth Engine](https://earthengine.google.com/), [`geemap`](https://geemap.org/) and a dataset from the National Agriculture Imagery Program ([NAIP](https://naip-usdaonline.hub.arcgis.com/)) to create a timelapse of how the garden has changed from 2005 to 2019.

`geemap` makes it easy to generate time series and timelapses from NAIP data using the built `timelapse` functions. Follow their tutorial [HERE](https://geemap.org/notebooks/90_naip_timelapse/)

<div align="center">
 {% include figure.html path="assets\img\posts\post-65th-and-woodlawn\community_garden-200m-naip.gif" class="img-fluid rounded z-depth-1" %}
</div>

Find the Jupyter Notebook to create this `.gif` [here](https://github.com/mjms/65th-woodlawn/blob/main/make_timelapse/make_timelapse.ipynb)!
