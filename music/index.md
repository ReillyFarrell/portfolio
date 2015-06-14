---
layout: archive
title: "Music"
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: 
tags: []
image:
  feature:
  teaser:
---

Summaries, scores, and code for musical compositions and projects.

####Acoustic<br>
<div class="tiles">
{% for post in site.categories.acoustic %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->

####Electronic
<div class="tiles">
{% for post in site.categories.music %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
