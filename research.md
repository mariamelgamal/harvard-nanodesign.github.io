---
layout: default
title: Research Projects
permalink: /research/
---

# Our Research

Description

<div class="projects-hierarchy">
  {% assign umbrella_projects = site.projects | where: "is_umbrella", true %}
  
  {% if umbrella_projects.size > 0 %}
    <h2>Research Thrusts</h2>
    {% for umbrella in umbrella_projects %}
      <details class="thrust-group" style="margin-bottom: 2rem; border: 1px solid #ddd; padding: 1rem; border-radius: 8px;">
        <summary style="cursor: pointer; font-size: 1.5rem; font-weight: bold;">
          {{ umbrella.title }} ({{ umbrella.status }})
        </summary>
        
        <div class="thrust-description" style="margin-top: 1rem; color: #555;">
          <p>{{ umbrella.excerpt | strip_html | truncatewords: 50 }}</p>
          <a href="{{ umbrella.url }}">View Full Research Thrust Details →</a>
        </div>

        <div class="sub-projects" style="margin-top: 1.5rem; margin-left: 1.5rem; border-left: 2px solid #007bff; padding-left: 1rem;">
          <h4>Projects within this Thrust</h4>
          {% assign children = site.projects | where: "parent_projects", umbrella.title %}
          {% if children.size > 0 %}
            <ul>
              {% for child in children %}
                <li>
                  <a href="{{ child.url }}"><strong>{{ child.title }}</strong></a> - {{ child.status }}
                </li>
              {% endfor %}
            </ul>
          {% else %}
            <p><em>No sub-projects listed yet.</em></p>
          {% endif %}
        </div>
      </details>
    {% endfor %}
  {% endif %}

  {% assign individual_projects = site.projects | where_exp: "item", "item.is_umbrella != true" | where_exp: "item", "item.parent_projects == nil" %}
  {% if individual_projects.size > 0 %}
    <h2>Standalone Research Projects</h2>
    <div class="projects-list">
      {% for project in individual_projects %}
        <article class="project-entry">
          <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
          <p><strong>Status:</strong> {{ project.status }}</p>
          <p>{{ project.excerpt | strip_html | truncatewords: 30 }}</p>
          <hr>
        </article>
      {% endfor %}
    </div>
  {% endif %}
</div>
