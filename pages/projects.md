---
layout: page
title: Projects
permalink: /projects
---

<table class="project-table">
  <tbody id="projects-tbody">
    {% for post in site.posts %}
      <tr>
        <td class="project-cell-left">
          <a href="{{ post.url }}"><img src="/assets/img/{{ post.image }}" class="project-thumbnail"></a>
        </td>
        <td class="project-cell-right">
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
        </td>
      </tr>
    {% endfor %}
  </tbody>
</table>

  <div id="projects-pagination" class="pagination" aria-label="Projects pagination"></div>

  <script>
  document.addEventListener('DOMContentLoaded', function(){
    const perPage = 25;
    const rows = Array.from(document.querySelectorAll('#projects-tbody tr'));
    const total = rows.length;
    const pages = Math.max(1, Math.ceil(total / perPage));
    let current = 1;

    function render() {
      const start = (current-1)*perPage;
      const end = start + perPage;
      rows.forEach((r,i)=> r.style.display = (i>=start && i<end) ? '' : 'none');

      const pag = document.getElementById('projects-pagination');
      if (!pag) return;
      pag.innerHTML = '';
      if (pages <= 1) return;

      // Previous
      if (current > 1) {
        const prev = document.createElement('a');
        prev.href = '#projects';
        prev.className = 'pagination-button pagination-active';
        prev.textContent = 'Previous';
        prev.addEventListener('click', function(e){ e.preventDefault(); current--; render(); });
        pag.appendChild(prev);
      } else {
        const span = document.createElement('span'); span.className='pagination-button'; span.textContent='Previous'; pag.appendChild(span);
      }

      // Info
      const info = document.createElement('span');
      info.className = 'pagination-info';
      info.textContent = ' Page ' + current + ' of ' + pages + ' ';
      pag.appendChild(info);

      // Next
      if (current < pages) {
        const next = document.createElement('a');
        next.href = '#projects';
        next.className = 'pagination-button pagination-active';
        next.textContent = 'Next';
        next.addEventListener('click', function(e){ e.preventDefault(); current++; render(); });
        pag.appendChild(next);
      } else {
        const span = document.createElement('span'); span.className='pagination-button'; span.textContent='Next'; pag.appendChild(span);
      }
    }

    render();
  });
  </script>