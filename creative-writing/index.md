---
layout: archive
title: "Creative Writing"
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: 
tags: []
image:
  feature: 
  teaser: 
---
Spacially organized words.  Suggested reading order is left-to-right, top-to-bottom across the page.  

<div class="tiles">
{% for post in site.categories.creative-writing %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
