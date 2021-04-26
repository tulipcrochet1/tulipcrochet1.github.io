---
layout: page
title: Gündelik Yazılarım
slug: gundelik
menu: true
order: 2

---

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>