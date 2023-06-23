---
layout: page
title: Companies
permalink: /companies
---
{% assign companies = site.posts | group_by: "company" %}
{% assign companiesSorted = companies | sort: "company" %}
<table class="project-table">
  <tbody>
    {% for company in companiesSorted %}
      {% if company.items[0].company[0].name == "na" %}
          {% continue %}
      {% endif %}
      <tr>
        <td class="project-cell-left">
          <a href="{{ company.items[0].company[0].website }}" target="_blank"><img src="{{ site.github.url }}/assets/img/companies/{{ company.items[0].company[0].name | downcase }}.jpg" class="company-logo"/></a>
        </td>
        <td class="project-cell-right">
        {% assign yearTitlesSorted = company.items | sort: "year" %}
        {% for post in yearTitlesSorted %}
          <ul>
            {{ forloop.index }}. <a href="{{ post.url }}">{{ post.title }}</a> by
              {% if post.authors %}
                {% for author in post.authors %}
                  <!-- Website present -->
                  {% if author.website %} 
                    <a href="{{ author.website }}">{{ author.name }}</a>{% if forloop.last == false %}, {% endif %}
                  <!-- No website present -->
                  {% else %}
                    {{ author.name }}{% if forloop.last == false %}, {% endif %}
                  {% endif %}
                {% endfor %}
              {% else %}
                {{ site.author.website }}
              {% endif %}
              ({{ post.year }}).
            <span class="project-description">{{ post.short }}</span>
          </ul>
        {% endfor %}
        </td>
      </tr>
    {% endfor %}
  </tbody>
</table>