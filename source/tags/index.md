---
layout: page
title: "Tags"
comments: false
sharing: true
footer: true
---

<h2>Top Categories</h2>
<ul>
  <li><a href="https://euccas.github.io/categories/system-design/">System Design</a></li>
  <li><a href="https://euccas.github.io/categories/product-design/">Product Design</a></li>
</ul>

{% capture tags %}
  {% for tag in site.categories %}
    {{ tag[0] }}
  {% endfor %}s
{% endcapture %}
{% assign sortedtags = tags | split:' ' | sort %}

<h2>All Tags</h2>
{% for tag in sortedtags %}
  <h3 id="{{ tag }}">{{ tag }}</h3>
  <ul>
  {% for post in site.categories[tag] %}
    <li>
      {% include postlistitem.html %}
    </li>
  {% endfor %}
  </ul>
{% endfor %}