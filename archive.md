---
layout: page
title: Archive
permalink: /archive/
---

<div>
	{% for post in site.posts %}
		{% unless post.next %}
			<strong>{{ post.date | date: '%Y %b' }}</strong>
			<ul class="archive">
		{% else %}
			{% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
			{% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
			{% if year != nyear %}
				</ul>
				<strong>{{ post.date | date: '%Y %b' }}</strong>
				<ul class="archive">
			{% endif %}
		{% endunless %}
		<li><a href="{{ post.url }}">{{ post.title }}</a></li>
	{% endfor %}
	</ul>
</div>
