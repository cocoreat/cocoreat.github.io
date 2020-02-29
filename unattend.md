---
layout: default
title: CoffeeCodeRepe.at
permalink: /unattend/
---

<div id="unattend">
  <h1>Unattended Installations</h1>
  <ul class="posts">
    {% for post in site.categories.unattend %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
</div>
