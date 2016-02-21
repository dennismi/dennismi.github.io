---
layout: page
title: DMAL Blog
---
{% include JB/setup %}

{% for post in site.posts %}
<article>
<header class="post-header"><h2 class="post-title"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h2></header>
<section class="post-excerpt">{{ post.excerpt | strip_html }}</section>
<footer class="post-meta"><img class="author-thumb" src="//www.gravatar.com/avatar/{{ site.author.gravatar }}?s=250&d=mm&r=x" alt="{{ site.author.name }}">{{ site.author.name }} in {% assign tags_list = post.tags %}{% include JB/inline_tags_list %}</footer> 
</article>
{% endfor %}
