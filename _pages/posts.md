---
layout: single
author_profile: true
title: Posts
header:
  overlay_image: ZenBG.png
permalink: /posts.html
---

<ul>
{% for post in site.posts %}
  {% assign currentdate = post.date | date: "%Y" %}
  {% if currentdate != date %}
    <h3>{{ currentdate }}</h3>
    {% assign date = currentdate %} 
  {% endif %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {{ post.excerpt }}
{% endfor %}
</ul>
