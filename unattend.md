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

  {% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}

  {{ t | downcase }}
  <ul>
    {% for post in posts %}
      {% if post.tags contains t %}
        <li>
          <a href="{{ post.url }}">{{ post.title }}</a>
          <span class="date">{{ post.date | date: "%B %-d, %Y"  }}</span>
        </li>
      {% endif %}
    {% endfor %}
  </ul>
  {% endfor %}

</div>
