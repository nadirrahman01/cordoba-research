---
layout: default
title: Research Home
---

# Cordoba Capital Research

## Latest notes

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      – {{ post.date | date: "%d %b %Y" }} – {{ post.author }} ({{ post.category }})
    </li>
  {% endfor %}
</ul>
