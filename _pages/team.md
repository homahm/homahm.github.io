---
layout: page
permalink: /team.html
title: OASIS Lab
page-title: Team
description: Online and AI Systems' Integrity & Safety Lab
nav: true
nav_order: 1
nav_rank: 1
---

<h2 class="group-heading">Lab News</h2>
<div class="lab-news-box">
{% include lab_news.html %}
</div>

<style>
  .lab-news-box {
    max-height: 200px;
    overflow-y: auto;
    font-size: 0.75rem;
    margin-bottom: 2rem;
    border: 1px solid var(--global-divider-color, #dee2e6);
    border-radius: 0.25rem;
    padding: 0.5rem;
  }
  .lab-news-box .table { margin-bottom: 0; }

  /* spacing between groups */
  .group-container { margin-bottom: 2rem; }

  /* group heading */
  .group-heading {
    margin: 1rem 0 0.5rem;
    font-size: 1.75rem;
    font-weight: bold;
  }

  /* default (non-special) wide cards */
  .team-card { margin-bottom: 1rem; }

  /* ===== Research Assistants: all 6 in one row ===== */
  .group-container.ra .ra-grid{
    display:flex !important;
    flex-wrap:nowrap !important;
    justify-content:space-around;
    gap:.5rem;
    text-align:center;
  }
  .group-container.ra .team-card{
    margin:0 !important;
    border:none !important;
    background:transparent !important;
    flex:1;
    max-width:130px;
  }
  .group-container.ra img.card-img,
  .group-container.ra img.img-fluid{
    width:90px !important;
    height:90px !important;
    object-fit:cover !important;
    object-position:top !important;
    border-radius:50% !important;
    display:block !important;
    margin:0 auto !important;
  }
  .group-container.ra .card-body{ padding:.3rem 0 0 !important; }
  .group-container.ra .card-title{ font-size:.85rem !important; margin-bottom:.1rem !important; }
  .group-container.ra .card-subtitle{ font-size:.7rem !important; }

  /* ===== Co-founders: 2 per row, equal images with equal spacing, name only ===== */
  .group-container.co-founders {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 0.5rem 3rem;
    text-align: center;
    margin-bottom: 2rem;
  }

  .group-container.co-founders > .group-heading {
    grid-column: 1 / -1;
    margin-bottom: 0.25rem;
    text-align: left;
  }

  .group-container.co-founders .card {
    border: none;
    background: transparent;
    padding: 0.25rem;
  }

  .group-container.co-founders img.card-img,
  .group-container.co-founders img.img-fluid {
    width: 200px;
    height: 200px;
    object-fit: cover;
    border-radius: .5rem;
    display: block;
    margin: 0 auto;
  }

  .group-container.co-founders .card-body {
    padding: 0.25rem 0 0;
    background: transparent;
  }

  .group-container.co-founders .card-title {
    font-size: 1rem;
    margin: 0;
    font-weight: 600;
    color: var(--global-text-color);
  }

  @media (max-width: 575.98px) {
    .group-container.co-founders {
      grid-template-columns: 1fr;
      gap: 2rem;
    }
  }

  /* ===== Team Members: default cards with smaller images ===== */
  .group-container .col-sm-4.col-md-3 {
    max-width: 20% !important;
    flex: 0 0 20% !important;
  }

  /* ===== Collaborators section ===== */
  .collaborators-section { margin-bottom: 2rem; }
  .collab-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1rem;
    text-align: center;
  }
  .collab-item {
    display: block;
    padding: 1rem 0.5rem;
    border: 1px solid var(--global-divider-color, #dee2e6);
    border-radius: 0.5rem;
    text-decoration: none;
    color: var(--global-text-color);
    font-size: 0.85rem;
    transition: box-shadow 0.2s;
  }
  .collab-item:hover {
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    text-decoration: none;
  }
  .collab-item strong { color: var(--global-theme-color, #2698BA); }
  @media (max-width: 575.98px) {
    .collab-grid { grid-template-columns: repeat(2, 1fr); }
  }

  /* ===== Former Lab Members: 4 per row, small proportional image, name only ===== */
  .group-container.former-members {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1rem;
    text-align: center;
  }

  /* Make the section header span the whole row */
  .group-container.former-members > .group-heading {
  grid-column: 1 / -1;
  margin-bottom: .5rem; /* space below header */
  text-align: left; /* left align the header */
  }

  .group-container.former-members img.card-img,
  .group-container.former-members img.img-fluid {
    width: 100px;   /* smaller image width */
    height: auto;   /* scale proportionally */
    object-fit: contain;
    border-radius: .5rem;
    display: block;
    margin: 0 auto;
  }
  .group-container.former-members .card-body {
    padding: 0.25rem 0 0;
  }
  .group-container.former-members .card-title {
    font-size: 0.85rem;
    margin-top: 0.25rem;
  }
</style>

{% assign groups = site.members | sort: "group_rank" | map: "group" | uniq %}
{% for group in groups %}
  {% assign members = site.members | sort: "group_order" | where: "group", group %}

  <div class="group-container
    {% if group == 'Research Assistants' %}ra{% endif %}
    {% if group == 'Co-founders' %}co-founders{% endif %}
    {% if group == 'Collaborators' %}collaborators{% endif %}
    {% if group == 'Former Lab Members' %}former-members{% endif %}">
    <h2 class="group-heading">{{ group }}</h2>

    {% if group == 'Research Assistants' %}
    <div class="ra-grid">
    {% endif %}

    {% for member in members %}
      {% if group == 'Co-founders' %}
        <!-- Co-founders: photo + name, clickable to website -->
        {% if member.lastname == 'Hosseinmardi' %}
          <a href="{{ '/' | relative_url }}" class="text-decoration-none">
        {% elsif member.external == true %}
          <a href="{{ member.profile.website }}" class="text-decoration-none" target="_blank">
        {% else %}
          <a href="{{ member.url | relative_url }}" class="text-decoration-none">
        {% endif %}
          <div class="card team-card">
            <img
              src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}"
              class="card-img img-fluid"
              alt="{{ member.profile.name }}"
            />
            <div class="card-body">
              <h5 class="card-title">{{ member.profile.name }}</h5>
            </div>
          </div>
        </a>
      {% elsif group == 'Research Assistants' %}
        <!-- Research Assistants: photo + name only -->
        <div class="card team-card">
          <img
            src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}"
            class="card-img img-fluid"
            alt="{{ member.profile.name }}"
          />
          <div class="card-body">
            <h5 class="card-title">{{ member.profile.name }}</h5>
          </div>
        </div>
      {% elsif group == 'Former Lab Members' %}
        <!-- Former Lab Members: only photo + name -->
        <div class="card team-card">
          <img
            src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}"
            class="card-img img-fluid"
            alt="{{ member.profile.name }}"
          />
          <div class="card-body">
            <h5 class="card-title">{{ member.profile.name }}</h5>
          </div>
        </div>
      {% else %}
        <!-- Default layout for other groups -->
        <div class="card team-card {% if member.inline == false %}hoverable{% endif %}">
          <div class="row no-gutters">
            <div class="col-sm-4 col-md-3">
              <img
                src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}"
                class="card-img img-fluid"
                alt="{{ member.profile.name }}"
              />
            </div>
            <div class="team col-sm-8 col-md-9">
              <div class="card-body">
                {% if member.inline == false %}
                  {% if member.external == true %}
                    <a href="{{ member.profile.website }}">
                  {% else %}
                    <a href="{{ member.url | relative_url }}">
                  {% endif %}
                {% endif %}

                <h5 class="card-title">{{ member.profile.name }}</h5>

                {% if member.profile.team-position or member.profile.position %}
                  <h6 class="card-subtitle mb-2 text-muted">
                    {{ member.profile.team-position | default: member.profile.position }}
                  </h6>
                {% endif %}

                {% if member.teaser %}
                  <p class="card-text">{{ member.teaser }}</p>
                {% endif %}

                {% if member.inline == false %}</a>{% endif %}
              </div>
            </div>
          </div>
        </div>
      {% endif %}
    {% endfor %}

    {% if group == 'Research Assistants' %}
    </div>
    {% endif %}
  </div>
{% endfor %}

<div class="group-container collaborators-section">
<h2 class="group-heading">Collaborators</h2>
<div class="collab-grid">
<a href="https://css.seas.upenn.edu/" target="_blank" class="collab-item">
<strong>CSSLab</strong><br>
UPenn
</a>
<a href="https://www.microsoft.com/en-us/research/people/davidmr/" target="_blank" class="collab-item">
<strong>MSR</strong><br>
NYU
</a>
<a href="https://www.shadirezapour.com/research-team" target="_blank" class="collab-item">
<strong>Social NLP Lab</strong><br>
Drexel
</a>
<a href="https://www.ethos-lab.org/home" target="_blank" class="collab-item">
<strong>ETHOS Lab</strong><br>
Drexel
</a>
</div>
</div>