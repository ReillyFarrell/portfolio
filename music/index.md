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

Scores and code I wrote for my musical compositions.  Audio examples of these pieces and more are available on [SoundCloud](https://soundcloud.com/capybarrage-reilly).

<div class="tiles">
{% for post in site.categories.music %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
