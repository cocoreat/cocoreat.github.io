---
layout: default
title: CoffeeCodeRepe.at
permalink: /timeline/
---

<div id="timeline">
  <h1>All Entries (sorted chronologically)</h1>
  <ul class="posts">
    {% for post in site.posts limit:15 %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
</div>
