---
layout: page
title: Projects
permalink: /projects
---

{% for post in site.posts %}
  {{ forloop.index }}. <a href="{{ post.url }}">{{ post.title }}</a> by {{ post.author }} ({{ post.year }}).
  <br>
  <span class="project-description">{{ post.short }}</span>
{% endfor %}
