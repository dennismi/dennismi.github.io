---
layout: front_page
title: dennismi Blog
theme_name: dmal
---
{% include JB/setup %}

{% for post in site.posts limit: 5 %}
<article>
<header class="post-header"><h2 class="post-title"><time>{{ post.date | date: "%b %-d, %Y" }}</time> - <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h2></header>
{% capture lastref %}{{post.date | date: "%Y-%B"}}{% endcapture %}
<footer class="post-meta">
{% unless post.categories == empty %} in {% assign categories_list = post.categories %} {% include JB/inline_categories_list %} {% endunless %} {% unless post.tags == empty %}Tagged: {% assign tags_list = post.tags %}{% include JB/inline_tags_list %} {% endunless %} 
</footer>
<hr> 
</article>
{% endfor %}

<a href="{{ site.JB.archive_path }}#{{lastref}}-ref">Archive</a>


