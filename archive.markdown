---
layout: default
permalink: /archive/
title: Archive - Martin Lundberg
---

Archive
================

<ul id="archive">
	{% for post in site.posts %}
	<li><a href="{{ post.url }}">{{ post.title }}</a> • {{ post.date | date:"%B %d, %Y" }}</li>
	{% endfor %}
</ul>
