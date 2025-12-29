---
layout: page
title: research
permalink: /projects/
description: In today's world, digital technologies are increasingly mediated by artificial intelligence systems whose inner workings are complex and often opaque, raising important questions about their societal impact. Our group brings together strong computational and engineering expertise to study the safety and integrity of online ecosystems. Our work focuses on developing scalable detection and prediction methods for large-scale, real-world data, and on designing controlled experiments to audit the safety and integrity of algorithmic systems, including settings where content may appear benign in isolation but interactions between algorithms and humans lead to consequential outcomes. We apply these methods across a range of societal risk domains, including harassment and abuse of vulnerable groups, biased or discriminatory treatment of minorities, radicalization and political polarization, the reliability of health information, and risks to youth safety and emotional well-being.
nav: true
nav_order: 2
---

<!-- pages/projects.md -->
<style>
.projects p,
.projects .card-text,
.projects .text-muted {
  text-align: justify;
}
.projects .category {
  color: #000000 !important;
}
.publications-toggle {
  cursor: pointer;
  color: #2774AE;
  font-size: 0.9rem;
  margin-top: 0.5rem;
  display: inline-block;
  user-select: none;
}
.publications-toggle:hover {
  color: #F2C75C;
}
.publications-list {
  display: none;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #e0e0e0;
}
.publications-list.show {
  display: block;
}
.publications-list ul {
  list-style: none;
  padding-left: 0;
}
.publications-list li {
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
}
</style>

<script>
function togglePublications(id) {
  const pubList = document.getElementById(id);
  pubList.classList.toggle('show');
}
</script>

<!-- Detailed research sections -->
<div class="projects mt-5">
  <h2 class="category" id="llm-studies">Studies of Large Language Models</h2>
  <p class="text-muted mb-4">Investigating the safety, behavior, and societal impact of large language models through red teaming, auditing, and experimental evaluation.</p>

  {%- assign llm_projects = site.projects | where: "category", "llm-studies" -%}
  {%- assign sorted_llm = llm_projects | sort: "importance" %}
  <div class="container">
    <div class="mb-5">
    {%- for project in sorted_llm -%}
      <div class="row mb-4">
        <div class="col-12">
          <div class="card">
            <div class="row g-0">
              {%- if project.img -%}
              <div class="col-md-3">
                <img src="{{ project.img | relative_url }}" class="img-fluid rounded-start" alt="{{ project.title }}" style="height: 100%; object-fit: cover;">
              </div>
              <div class="col-md-9">
              {%- else -%}
              <div class="col-12">
              {%- endif -%}
                <div class="card-body">
                  {%- if project.related_publications -%}
                  <div onclick="togglePublications('pubs-{{ project.title | slugify }}')" style="cursor: pointer;">
                    <h5 class="card-title">{{ project.title }}</h5>
                    <p class="card-text">{{ project.description }}</p>
                  </div>
                  {%- else -%}
                  <h5 class="card-title">{{ project.title }}</h5>
                  <p class="card-text">{{ project.description }}</p>
                  {%- endif -%}
                </div>
              </div>
            </div>
          </div>
          {%- if project.related_publications -%}
          <div class="publications-list" id="pubs-{{ project.title | slugify }}">
            <ul>
              {%- for pub in project.publications_list -%}
              <li>
                {{ pub.authors }} ({{ pub.year }}). {{ pub.title }}. <em>{{ pub.venue }}</em>.
              </li>
              {%- endfor -%}
            </ul>
          </div>
          {%- endif -%}
        </div>
      </div>
    {%- endfor %}
    </div>
  </div>

  <h2 class="category" id="sociotechnical-systems">Studies of Sociotechnical Systems</h2>
  <p class="text-muted mb-4">Examining how algorithmic systems, human behavior, and platform design interact to shape online experiences and societal outcomes.</p>

  {%- assign sociotech_projects = site.projects | where: "category", "sociotechnical-systems" -%}
  {%- assign sorted_sociotech = sociotech_projects | sort: "importance" %}
  <div class="container">
    <div class="mb-5">
    {%- for project in sorted_sociotech -%}
      <div class="row mb-4">
        <div class="col-12">
          <div class="card">
            <div class="row g-0">
              {%- if project.img -%}
              <div class="col-md-3">
                <img src="{{ project.img | relative_url }}" class="img-fluid rounded-start" alt="{{ project.title }}" style="height: 100%; object-fit: cover;">
              </div>
              <div class="col-md-9">
              {%- else -%}
              <div class="col-12">
              {%- endif -%}
                <div class="card-body">
                  {%- if project.related_publications -%}
                  <div onclick="togglePublications('pubs-{{ project.title | slugify }}')" style="cursor: pointer;">
                    <h5 class="card-title">{{ project.title }}</h5>
                    <p class="card-text">{{ project.description }}</p>
                  </div>
                  {%- else -%}
                  <h5 class="card-title">{{ project.title }}</h5>
                  <p class="card-text">{{ project.description }}</p>
                  {%- endif -%}
                </div>
              </div>
            </div>
          </div>
          {%- if project.related_publications -%}
          <div class="publications-list" id="pubs-{{ project.title | slugify }}">
            <ul>
              {%- for pub in project.publications_list -%}
              <li>
                {{ pub.authors }} ({{ pub.year }}). {{ pub.title }}. <em>{{ pub.venue }}</em>.
              </li>
              {%- endfor -%}
            </ul>
          </div>
          {%- endif -%}
        </div>
      </div>
    {%- endfor %}
    </div>
  </div>

  <h2 class="category" id="information-ecosystems">Studies of Information Ecosystems</h2>
  <p class="text-muted mb-4">Understanding how information flows, fragments, and influences society through traditional and digital media platforms.</p>

  {%- assign info_projects = site.projects | where: "category", "information-ecosystems" -%}
  {%- assign sorted_info = info_projects | sort: "importance" %}
  <div class="container">
    <div class="mb-5">
    {%- for project in sorted_info -%}
      <div class="row mb-4">
        <div class="col-12">
          <div class="card">
            <div class="row g-0">
              {%- if project.img -%}
              <div class="col-md-3">
                <img src="{{ project.img | relative_url }}" class="img-fluid rounded-start" alt="{{ project.title }}" style="height: 100%; object-fit: cover;">
              </div>
              <div class="col-md-9">
              {%- else -%}
              <div class="col-12">
              {%- endif -%}
                <div class="card-body">
                  <h5 class="card-title">{{ project.title }}</h5>
                  <p class="card-text">{{ project.description }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    {%- endfor %}
    </div>
  </div>

  <h2 class="category" id="computational-methods">Computational Methods</h2>
  <p class="text-muted mb-4">Developing novel computational and statistical methods for studying complex sociotechnical systems.</p>

  {%- assign method_projects = site.projects | where: "category", "computational-methods" -%}
  {%- assign sorted_methods = method_projects | sort: "importance" %}
  <div class="container">
    <div class="mb-5">
    {%- for project in sorted_methods -%}
      <div class="row mb-4">
        <div class="col-12">
          <div class="card">
            <div class="row g-0">
              {%- if project.img -%}
              <div class="col-md-3">
                <img src="{{ project.img | relative_url }}" class="img-fluid rounded-start" alt="{{ project.title }}" style="height: 100%; object-fit: cover;">
              </div>
              <div class="col-md-9">
              {%- else -%}
              <div class="col-12">
              {%- endif -%}
                <div class="card-body">
                  <h5 class="card-title">{{ project.title }}</h5>
                  <p class="card-text">{{ project.description }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    {%- endfor %}
    </div>
  </div>
</div>
