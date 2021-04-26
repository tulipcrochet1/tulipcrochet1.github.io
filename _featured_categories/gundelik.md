---
layout: page
title: Gündelik Yazılarım
slug: gundelik
menu: true
order: 2

---

<ul>
  {% for gundelik in site.gundeliks %}
    <li>
      <a href="{{ gundelik.url }}">{{ gundelik.title }}</a>
    </li>
  {% endfor %}
</ul>