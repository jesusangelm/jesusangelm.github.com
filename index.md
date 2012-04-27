---
layout: page
title: Jam Blog - Venezuela
---
{% include JB/setup %}

##¡Aprende Linux Facilmente!

###Lista de mis ultimos articulos:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>Publicado: {{ post.date | date_to_string }}</span><br> Titulo: <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li><br>
  {% endfor %}
</ul>


