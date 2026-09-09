---
layout: default
title: CTF Writeups
---
<section class="archive-content">
  <header class="page-heading"><p class="eyebrow">OUR CTF WRITEUP ARCHIVE / {{ site.posts | size }} WRITEUPS</p><h1>Every flag has a story.</h1><p>Breaking down the challenges, highlighting the dead ends and discussing our methodology for the captures.</p></header>
  {% assign groups = site.posts | group_by_exp: 'post', "post.date | date: '%Y'" %}
  {% for group in groups %}
  <section class="archive-year"><h2>{{ group.name }}</h2><div class="writeup-list">
    {% for post in group.items %}
    <a class="writeup-row" href="{{ post.url | relative_url }}"><span class="category">{{ post.categories | first | default: 'CTF' | escape }}</span><div><h3>{{ post.title | escape }}</h3></div><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: '%b %d' }}</time><span class="row-arrow" aria-hidden="true">↗</span></a>
    {% endfor %}
  </div></section>
  {% endfor %}
</section>
