---
layout: page
title: Coaches
permalink: /coaches
---
<!-- Unique list of coaches -->
{% assign coachesUniq = site.posts | map: "coaches" | map: "name" | uniq %}
<!-- Websites of coaches -->
{% assign websitesUniq = site.posts | map: "coaches" | map: "website" | uniq %}
{% assign coaches = site.posts | group_by: "coaches" %}
{% assign coachesSorted = coaches | sort: "name" %}
<table class="project-table">
  <tbody>
    <!-- Counter for iterative over websites -->
    {% assign counter = -1 %}
    <!-- Loop over coaches -->
    {% for coachUniq in coachesUniq %}
      <!-- Increment counter for website -->
      {% assign counter = counter|plus:1 %}
      <!-- Skip NA -->
      {% if coachUniq == "na" %}
        {% continue %}
      {% endif %} 
      {% assign coachUniqPosts = "" | split: ',' %}
      <tr>
        <td class="project-cell-left">
          <img src="{{ site.github.url }}/assets/img/people/{{ coachUniq | downcase | replace: ' ', '-'}}.jpg" class="coach-logo"/>
          <a href="{{ websitesUniq[counter] }}">{{ coachUniq }}</a>
        </td>
        <td class="project-cell-right">
        <!-- Loop over projects by coach -->
        {% for coach in coachesSorted %}
          <!-- Find projects of the coach -->
          {% if coach.name contains coachUniq %}
            <!-- Add projects to the list of the coach -->
            {% assign coachUniqPosts = coachUniqPosts | concat: coach.items | uniq | sort: "year" %}
          {% endif %}
        {% endfor %}
        {% for post in coachUniqPosts %}
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