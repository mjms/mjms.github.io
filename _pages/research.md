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
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
</div>

<!-- _pages/research.md -->
<div class="publications">
  <h2 >publications</h2>
    {%- for y in page.years %}

      <h2 class="year">{{y}}</h2>
      {% bibliography -f papers -q @*[year={{y}}]* %}
    {% endfor %}

</div>