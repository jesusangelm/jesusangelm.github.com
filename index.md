---
layout: page
title: Jam Blog - Venezuela
---
{% include JB/setup %}

##Bienvenido a Jam Blog

### Aqui esta una lista de los ultimos articulos:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


