---
layout: page
permalink: /publications/
title: publications
description: Peer-reviewed publications by categories in reversed chronological order. 
years: [2020,2021,2022,2024]
nav: true
---

<div class="publications">

{% for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
