---
layout: page
title: Companies
permalink: /companies
---

{% assign companies = site.posts | group_by: "company" %}
{% assign companiesSorted = companies | sort: "name" %}

<table class="project-table">
  <tbody>
    {% for company in companiesSorted %}
      {% if company.name == "na" %}
          {% continue %}
      {% endif %}
      <tr>
        <td class="project-cell-left">
          <img src="{{ site.github.url }}/assets/img/companies/{{ company.name | downcase }}.jpg" class="company-logo"/>
        </td>
        <td class="project-cell-right">
          <ul>
        {% assign yearTitlesSorted = company.items | sort: "year" %}
        {% for post in yearTitlesSorted %}
          {{ forloop.index }}. <a href="{{ post.url }}">{{ post.title }}</a> by {{ post.author }} ({{ post.year }}).
          <span class="project-description">{{ post.short }}</span>
        {% endfor %}
      </ul>
        </td>
      </tr>
    {% endfor %}
  </tbody>
</table>