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
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
