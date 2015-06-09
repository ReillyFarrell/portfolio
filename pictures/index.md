---
layout: archive
title: Pictures
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: 
tags: []
image:
  feature:
  teaser:
---
####Pictures
I'm no visual artist - but here's some original visual art just for you, created in Microsoft Word on a default 6x6 table.

<div class="tiles">
{% for post in site.categories.pictures %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->

####Creative Writing
<div class="tiles">
{% for post in site.categories.creative-writing %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
