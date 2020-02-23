---
layout: default
title: CoffeeCodeRepe.at
permalink: /projects/
---

<div id="projects">
  <h1>Spare Time Projects</h1>
  <ul class="posts">
  {% for post in site.categories.project %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  </ul>
</div>
