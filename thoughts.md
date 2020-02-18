---
layout: default
title: CoffeeCodeRepe.at
permalink: /thoughts/
---

<div id="thoughts">
  <h1>Thoughts of a Sysadmin</h1>
  <ul class="posts">
    {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
</div>
