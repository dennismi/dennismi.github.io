---
layout: page
title: Tags
header: Posts By Tag
group: navigation
tagline: ''
---
{% include JB/setup %}

## All tags with their number of posts
<ul>
  {% assign tags_list = site.tags %}  
  {% include JB/tags_list %}
</ul>


{% for tag in site.tags %} 
  <h3 id="{{ tag[0] }}-ref">{{ tag[0] }}</h3>
  <ul>
    {% assign pages_list = tag[1] %}  
    {% include JB/pages_list %}
  </ul>
{% endfor %}
