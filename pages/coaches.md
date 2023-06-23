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
          <img src="{{ site.github.url }}/assets/img/people/{{ coachUniq | downcase | replace: ' ', '-'}}.jpg" class="coach-logo" />
          <span class="anchor-coach" id="{{ coachUniq | downcase | replace: ' ', '-' }}"></span><h4 class="coaches-coach-caption"><a href="{{ websitesUniq[counter] }}" target="_blank">{{ coachUniq }}</a><a href="#{{ coachUniq | downcase | replace: ' ', '-' }}"><svg class="octicon" viewBox="0 0 16 16" version="1.1" width="16" height="32" aria-hidden="true"><path fill-rule="evenodd" d="M7.775 3.275a.75.75 0 001.06 1.06l1.25-1.25a2 2 0 112.83 2.83l-2.5 2.5a2 2 0 01-2.83 0 .75.75 0 00-1.06 1.06 3.5 3.5 0 004.95 0l2.5-2.5a3.5 3.5 0 00-4.95-4.95l-1.25 1.25zm-4.69 9.64a2 2 0 010-2.83l2.5-2.5a2 2 0 012.83 0 .75.75 0 001.06-1.06 3.5 3.5 0 00-4.95 0l-2.5 2.5a3.5 3.5 0 004.95 4.95l1.25-1.25a.75.75 0 00-1.06-1.06l-1.25 1.25a2 2 0 01-2.83 0z"></path></svg></a></h4>
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