---
layout: default
title: CoffeeCodeRepe.at
permalink: /projects/
---

<div id="projects">
  <h1>HomeLab (ongoing)</h1>
  <ul>
  {% for post in site.posts.category.project %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
</div>
