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

Summaries, scores, code, and audio recordings for musical compositions and projects.

<div class="tiles">
{% for post in site.categories.music %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->