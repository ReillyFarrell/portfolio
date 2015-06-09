---
layout: archive
title: "Pictures"
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: 
tags: []
image:
  feature:
  teaser:
---

Well, I'm no visual artist, but here's some original visual art just for you.

<div class="tiles">
{% for post in site.categories.pictures %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
