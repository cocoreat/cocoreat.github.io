---
layout: default
title: CoffeeCodeRepe.at
permalink: /projects/
---

<div id="projects">
  <h1>Spare Time Projects</h1>
  <ul class="posts">
    {% for post in site.categories.projects %}
    <h1>homelab</h1>
      {% if post.tags contains 'homelab' %}
        <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endif %}
    {% endfor %}
  </ul>
</div>
