---
layout: page
title: Archive
permalink: /archive/
---

{% for post in site.posts %}
	{% unless post.next %}
__{{ post.date | date: '%Y %b' }}__
{% else %}
	{% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
	{% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
	{% if year != nyear %}
__{{ post.date | date: '%Y %b' }}__
	{% endif %}
{% endunless %}
<ul>
	<li><a href="{{ post.url }}">{{ post.title }}</a></li>
</ul>
{% endfor %}
