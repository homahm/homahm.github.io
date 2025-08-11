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
  /* Base spacing + headings */
  .group-container { margin-bottom: 2rem; }
  .group-heading { margin: 1rem 0 0.5rem; font-size: 1.75rem; font-weight: bold; }
  .team-card { margin-bottom: 1rem; }

  /* Preserve side-by-side layout for non-RA and non-former groups */
  .group-container:not(.ra):not(.former) .row.no-gutters { display: flex; }
  .group-container:not(.ra):not(.former) .col-sm-4.col-md-3 { flex: 0 0 25%; max-width: 25%; }
  .group-container:not(.ra):not(.former) .team.col-sm-8.col-md-9 { flex: 0 0 75%; max-width: 75%; }

  /* ===== Research Assistants: stacked cards, 4 per row ===== */
  .group-container.ra {
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    gap: .75rem;
  }
  .group-container.ra > .group-heading {
    grid-column: 1 / -1;
    margin-bottom: .5rem;
  }
  .group-container.ra .team-card { margin: 0; font-size: .9rem; }
  .group-container.ra .row.no-gutters { display: block; }
  .group-container.ra .col-sm-4.col-md-3,
  .group-container.ra .team.col-sm-8.col-md-9 { width: 100%; max-width: 100%; }
  .group-container.ra img.card-img,
  .group-container.ra img.img-fluid {
    width: 100%;
    height: 180px;
    object-fit: cover;
    border-radius: .5rem .5rem 0 0;
    display: block;
  }
  .group-container.ra .card-body { padding: .5rem .6rem .75rem; }
  .group-container.ra .card-title { font-size: 1rem; margin-bottom: .25rem; }
  .group-container.ra .card-subtitle { font-size: .85rem; }
  .group-container.ra .card-text { font-size: .9rem; }
  @media (max-width: 991.98px) { .group-container.ra { grid-template-columns: repeat(3, 1fr); } }
  @media (max-width: 575.98px) { .group-container.ra { grid-template-columns: repeat(2, 1fr); } }

  /* ===== Former lab members: mini stacked cards, 5 per row, name only ===== */
  .group-container.former {
    display: grid;
    grid-template-columns: repeat(5, minmax(0, 1fr));
    gap: .75rem;
  }
  .group-container.former > .group-heading {
    grid-column: 1 / -1;
    margin-bottom: .5rem;
  }
  .group-container.former .mini-card {
    margin: 0;
    text-align: center;
    padding: 0;
    border: none;
    box-shadow: none;
    background: transparent;
  }
  .group-container.former .mini-img {
    width: 100%;
    height: 110px; /* adjust to resize photo */
    object-fit: cover;
    border-radius: .5rem;
    display: block;
  }
  .group-container.former .mini-name {
    font-size: .95rem;
    margin-top: .4rem;
    font-weight: 600;
  }
  @media (max-width: 991.98px) { .group-container.former { grid-template-columns: repeat(4, 1fr); } }
  @media (max-width: 575.98px) { .group-container.former { grid-template-columns: repeat(3, 1fr); } }
</style>

{% comment %}
Special groups:
- Research Assistants → stacked 4-up layout.
- Former lab members → mini stacked 5-up layout (name only).
- Everything else → original wide card layout.
{% endcomment %}

{% assign groups = site.members | sort: "group_rank" | map: "group" | uniq %}
{% for group in groups %}
  {% assign members = site.members | sort: "group_order" | where: "group", group %}
  <div class="group-container
    {% if group == 'Research Assistants' %}ra{% endif %}
    {% if group | downcase == 'former lab members' %}former{% endif %}">
    <h2 class="group-heading">{{ group }}</h2>

    {% if group | downcase == 'former lab members' %}
      {% for member in members %}
        <div class="mini-card">
          {% if member.inline == false %}
            {% if member.external == true %}
              <a href="{{ member.profile.website }}">
            {% else %}
              <a href="{{ member.url | relative_url }}">
            {% endif %}
          {% endif %}
          <img src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}"
               class="mini-img" alt="{{ member.profile.name }}" />
          <div class="mini-name">{{ member.profile.name }}</div>
          {% if member.inline == false %}</a>{% endif %}
        </div>
      {% endfor %}

    {% else %}
      {% for member in members %}
        <div class="card team-card {% if member.inline == false %}hoverable{% endif %}">
          <div class="row no-gutters">
            <div class="col-sm-4 col-md-3">
              <img src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}"
                   class="card-img img-fluid" alt="{{ member.profile.name }}" />
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
                {% if member.profile.email %}<a href="mailto:{{ member.profile.email }}" class="card-link"><i class="fas fa-envelope"></i></a>{% endif %}
                {% if member.profile.phone %}<a href="tel:{{ member.profile.phone }}" class="card-link"><i class="fas fa-phone"></i></a>{% endif %}
                {% if member.profile.orcid %}<a href="https://orcid.org/{{ member.profile.orcid }}" class="card-link" target="_blank"><i class="fab fa-orcid"></i></a>{% endif %}
                {% if member.profile.twitter %}<a href="https://twitter.com/{{ member.profile.twitter }}" class="card-link" target="_blank"><i class="fab fa-twitter"></i></a>{% endif %}
                {% if member.profile.github %}<a href="https://github.com/{{ member.profile.github }}" class="card-link" target="_blank"><i class="fab fa-github"></i></a>{% endif %}
                {% if member.profile.website %}<a href="{{ member.profile.website }}" class="card-link" target="_blank"><i class="fas fa-globe"></i></a>{% endif %}
              </div>
            </div>
          </div>
        </div>
      {% endfor %}
    {% endif %}
  </div>
{% endfor %}