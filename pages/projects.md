---
layout: page
title: Projects
permalink: /projects
---

<table class="project-table">
  <tbody>
    {% for post in site.posts %}
      <tr>
        <td class="project-cell-left">
          <a href="{{ post.url }}"><img src="/assets/img/{{ post.image }}" class="project-thumbnail"></a>
        </td>
        <td class="project-cell-right">
          <ul>
            {{ forloop.index }}. <a href="{{ post.url }}">{{ post.title }}</a> by {{ post.author }} ({{ post.year }}).
              <span class="project-description">{{ post.short }}</span>
          </ul>
        </td>
      </tr>
    {% endfor %}
  </tbody>
</table>