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
    <li><a href="https://www.microsoft.com/en-us/download/details.aspx?id=56846">maiLab:</a> Holt euch einen Tee, Freunde der Sonne, macht es euch gemütlich - Zeit für Science!</li>
    <li><a href="https://www.youtube.com/watch?v=7AYnF5hOhuM">Twin Peaks ACTUALLY EXPLAINED (No, Really)</a></li>
  </ul>

  <h1>How to do things</h1>
  <ul class="posts">
    <li><a href="https://www.hanselman.com/blog/HowToRemoteDesktopFullscreenRDPWithJustSOMEOfYourMultipleMonitors.aspx">How to remote desktop fullscreen RDP with just SOME of your multiple monitors</a></li>
    <li><a href="https://www.microsoft.com/en-us/download/details.aspx?id=56846">Windows Command Reference</a></li>
  </ul>

  <h1>Noteworthy Open Source Projects</h1>
  <ul class="posts">
    <li><a href="http://github.com/jekyll/jekyll">Jekyll:</a> A simple, blog aware, static site generator (used for this site).</li>
    <li><a href="https://github.com/pi-hole/pi-hole">Pi-hole</a> Network-wide ad blocking via your own Linux hardware</li>
  </ul>

  <h1>Application Recommendations</h1>
  <ul class="posts">
    <li><a href="http://github.com/jekyll/jekyll/">Jekyll:</a> A simple, blog aware, static site generator (used for this site).</li>
  </ul>

</div>
