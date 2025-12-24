---
layout: page
title: projects
permalink: /projects/
description: A subset of my current work organized by research themes. Stay tuned for more.
nav: true
nav_order: 2
display_categories: [llm-studies, sociotechnical-systems, information-ecosystems]
horizontal: false
---

<!-- pages/projects.md -->
<div class="projects">
{%- if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {%- for category in page.display_categories %}
  
  {%- if category == "llm-studies" %}
    <h2 class="category">Studies of Large Language Models</h2>
    <p class="text-muted mb-4">Investigating the safety, behavior, and societal impact of large language models through red teaming, auditing, and experimental evaluation.</p>
  {%- elsif category == "sociotechnical-systems" %}
    <h2 class="category">Studies of Sociotechnical Systems</h2>
    <p class="text-muted mb-4">Examining how algorithmic systems, human behavior, and platform design interact to shape online experiences and societal outcomes.</p>
  {%- elsif category == "information-ecosystems" %}
    <h2 class="category">Studies of Information Ecosystems</h2>
    <p class="text-muted mb-4">Understanding how information flows, fragments, and influences society through traditional and digital media platforms.</p>
  {%- else %}
    <h2 class="category">{{ category }}</h2>
  {%- endif %}
  
  {%- assign categorized_projects = site.projects | where: "category", category -%}
  {%- assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}

{%- else -%}
<!-- Display projects without categories -->
  {%- assign sorted_projects = site.projects | sort: "importance" -%}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
{%- endif -%}
</div>
