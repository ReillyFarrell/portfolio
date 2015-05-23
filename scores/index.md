---
layout: archive
title: "Scores"
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: 
tags: []
image:
  feature:
  teaser:
---
####Musical scores, write-ups, and related materials.
Here you can find various things I wrote, scribbled or typed for my compositions so that one day other people could understand them.

#PDFs
<div class="tiles">
{% for post in site.categories.scores %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
