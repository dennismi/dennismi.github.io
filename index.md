---
layout: page
title: DMAL Blog!
tagline: a new world...
---
{% include JB/setup %}
## Introduction
something will show up here :)

## Post List

<ul class="posts">
  {% for post in site.posts %}
    <li><h3>{{ post.date | date_to_string }} &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3><br/>
    {{ post.content }} </li>
  {% endfor %}
</ul>
