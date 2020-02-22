---
layout: default
title: CoffeeCodeRepe.at
---

<div id="home">
  <h1>Recent Entries</h1>
  <ul class="posts">
    {% for post in site.posts limit:15 %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>

  <h1>Highlighted Web Content</h1>
  <ul class="posts">
    <li><a href="https://www.youtube.com/watch?v=7AYnF5hOhuM">Video: Twin Peaks ACTUALLY EXPLAINED (No, Really)</a></li>
  </ul>

  <h1>Noteworthy Open Source Projects</h1>
  <ul class="posts">
    <li><a href="http://github.com/jekyll/jekyll/">Jekyll:</a> A simple, blog aware, static site generator (used for this site).</li>
  </ul>
</div>
