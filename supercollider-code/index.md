---
layout: archive
title: "SuperCollider Code"
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: 
tags: []
image:
  feature:
  teaser:
---
####Code written in SuperCollider to generate and organize electronic compositions
I discovered [SuperCollider](http://supercollider.github.io) from a sound design course taught by [Bruno Ruviaro](http://www.brunoruviaro.com).  This programming language is built for coding sound, and it's hands-down my favorite discovery from my time at Santa Clara University.  

Here you will find the code behind my electronic music projects.  

*(Note: Most of this code can be copied and played in SuperCollider as is.  Code for sampling pieces, however, requires SuperCollider to find a sample wav file located at a specific filepath - which, as I've written the code, only applies to my computer.  To play these pieces, please visit [my SoundCloud account.](https://soundcloud.com/capybarrage-reilly)

####Projects in SuperCollider
<div class="tiles">
{% for post in site.categories.supercollider-code %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
