---
layout: page
title: projects
permalink: /projects/
description: Our lab's work is grouped into four broad tracks which make up the primary research programs at the Computational Social Science Lab.
nav: true
nav_order: 2
---

<!-- pages/projects.md -->
<style>
.project-blocks {
  max-width: 1000px;
  margin: 3rem auto;
}

.project-block {
  background-color: #4a5568;
  color: white;
  min-height: 280px;
  display: block;
  text-align: center;
  padding: 2rem;
  text-decoration: none;
  transition: all 0.3s ease;
  border-radius: 0;
  margin-bottom: 1.5rem;
}

.project-block > * {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 280px;
}

.project-block:hover {
  background-color: #5a6778;
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
  text-decoration: none;
}

.project-block h3 {
  color: white;
  font-size: 1.75rem;
  font-weight: 400;
  margin: 0;
  line-height: 1.4;
}

.project-block:hover h3 {
  color: white;
}

@media (max-width: 768px) {
  .project-block {
    min-height: 200px;
  }
  .project-block h3 {
    font-size: 1.5rem;
  }
}
</style>

<div class="project-blocks">
  <div class="row g-4">
    <div class="col-12 col-md-6">
      <a href="#llm-studies" class="project-block">
        <h3>Large Language Models and Agentic AI</h3>
      </a>
    </div>
    <div class="col-12 col-md-6">
      <a href="#sociotechnical-systems" class="project-block">
        <h3>Sociotechnical System's intergirty and safety</h3>
      </a>
    </div>
    <div class="col-12 col-md-6">
      <a href="#information-ecosystems" class="project-block">
        <h3>Media and Demoncracy</h3>
      </a>
    </div>
    <div class="col-12 col-md-6">
      <a href="#computational-methods" class="project-block">
        <h3>Computational Methods</h3>
      </a>
    </div>
  </div>
</div>

<!-- Detailed project sections -->
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
