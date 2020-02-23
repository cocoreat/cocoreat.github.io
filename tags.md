---
layout: default
title: CoffeeCodeRepe.at
permalink: /tags/
---

<div id="tags">

  <h1>All Entries (sorted by tags)</h1>

  {% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}

  <h1>{{ t | downcase }}</h1>
  <ul class="posts">
    {% for post in posts %}
      {% if post.tags contains t %}
        <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endif %}
    {% endfor %}
  </ul>
  {% endfor %}

</div>
