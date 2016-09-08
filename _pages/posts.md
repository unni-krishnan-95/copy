---
layout: single
title: Posts
author_profile: true
permalink: /posts.html
---

{% include base_path %} {% for post in site.posts %} {% include archive-single.html %} {% endfor %}
