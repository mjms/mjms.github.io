---
layout: page
permalink: /research/
title: research
description: 
years: [2022,2021,2018,2015]
nav: true
nav_order: 2
---
<div class="research">

</div>

<!-- _pages/research.md -->
<div class="publications">
  <h2 >publications</h2>
    {%- for y in page.years %}

      <h2 class="year">{{y}}</h2>
      {% bibliography -f papers -q @*[year={{y}}]* %}
    {% endfor %}

</div>