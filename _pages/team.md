---
layout: page
permalink: /team.html
title: OASIS lab
page-title: Team
description: Online and AI Systems’ Integrity & Safety
nav: true
nav_order: 2
nav_rank: 2
---

<style>
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

  /* ===== Research Assistants: compact grid, 4 per row, text under photo ===== */
  .group-container.ra{
    display:grid;
    grid-template-columns:repeat(4,minmax(0,1fr));
    gap:.75rem;
  }
  .group-container.ra > .group-heading{
    grid-column:1 / -1;
    margin-bottom:.5rem;
  }
  .group-container.ra .team-card{ margin:0; font-size:.9rem; }
  .group-container.ra .row.no-gutters{ display:block; }
  .group-container.ra .col-sm-4.col-md-3,
  .group-container.ra .team.col-sm-8.col-md-9{ width:100%; max-width:100%; }
  .group-container.ra img.card-img,
  .group-container.ra img.img-fluid{
    width:100%;
    height:auto;
    object-fit:cover;
    border-radius:.5rem .5rem 0 0;
    display:block;
  }
  .group-container.ra .card-body{ padding:.5rem .6rem .75rem; }
  .group-container.ra .card-title{ font-size:1rem; margin-bottom:.25rem; }
  .group-container.ra .card-subtitle{ font-size:.85rem; }
  .group-container.ra .card-text{ font-size:.9rem; }
  @media (max-width:991.98px){ .group-container.ra{ grid-template-columns:repeat(3,1fr); } }
  @media (max-width:575.98px){ .group-container.ra{ grid-template-columns:repeat(2,1fr); } }

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
    font-size: 0.9rem;
    margin-top: 0.25rem;
  }
</style>

{% assign groups = site.members | sort: "group_rank" | map: "group" | uniq %}
{% for group in groups %}
  {% assign members = site.members | sort: "group_order" | where: "group", group %}

  <div class="group-container
    {% if group == 'Research Assistants' %}ra{% endif %}
    {% if group == 'Former Lab Members' %}former-members{% endif %}">
    <h2 class="group-heading">{{ group }}</h2>

    {% for member in members %}
      {% if group == 'Former Lab Members' %}
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
  </div>
{% endfor %}