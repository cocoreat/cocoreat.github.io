---
layout: default
title: CoffeeCodeRepe.at
---

<div id="home">
  <h1>Thoughts of a Sysadmin</h1>
  <ul class="posts">
    {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>

  <h1>Spare Time Projects</h1>
  <ul class="posts">
    <li><span>02 Apr 2005</span> &raquo; <a href="https://web.archive.org/web/20061214040137/http://joshuaink2006.johnoxton.co.uk/blog/240/seven-and-a-half-questions-for-tom-werner">JoshuaInk: Seven and a half questions for Tom Werner</a></li>
  </ul>

  <h1>Unattended Installations</h1>
  <ul class="posts">
    {% for post in site.unattend %}
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
