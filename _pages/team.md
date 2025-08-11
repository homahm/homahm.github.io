<style>
  /* spacing between groups */
  .group-container { margin-bottom: 2rem; }

  .group-heading {
    margin: 1rem 0 0.5rem;
    font-size: 1.75rem;
    font-weight: bold;
  }

  /* default (non-RA) cards (your current wide layout) */
  .team-card { margin-bottom: 1rem; }

  /* ===== Research Assistants: compact, 4-per-row grid ===== */
  .ra-grid .ra-card { margin-bottom: 1rem; }
  .ra-grid .ra-card .card-body { padding: 0.5rem 0.5rem 0.75rem; }
  .ra-grid .ra-card .card-title { font-size: 1rem; margin-bottom: 0.25rem; }
  .ra-grid .ra-card .card-subtitle { font-size: 0.85rem; }
  .ra-grid .ra-img {
    width: 100%;
    aspect-ratio: 1 / 1;
    object-fit: cover;
    border-radius: .5rem;
  }
  .ra-grid .card-text { font-size: 0.85rem; }
</style>

{% assign groups = site.members | sort: "group_rank" | map: "group" | uniq %}
{% for group in groups %}
  {% assign members = site.members | sort: "group_order" | where: "group", group %}

  <div class="group-container">
    <h2 class="group-heading">{{ group }}</h2>

    {% if group == 'Research Assistants' %}
      <!-- Research Assistants: compact 4-per-row grid -->
      <div class="row ra-grid">
        {% for member in members %}
          <div class="col-6 col-md-3">
            <div class="card ra-card {% if member.inline == false %}hoverable{% endif %}">
              {% if member.inline == false %}
                {% if member.external == true %}
                  <a href="{{ member.profile.website }}">
                {% else %}
                  <a href="{{ member.url | relative_url }}">
                {% endif %}
              {% endif %}

              <img
                src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}"
                class="ra-img"
                alt="{{ member.profile.name }}"
              />

              <div class="card-body">
                <h5 class="card-title">{{ member.profile.name }}</h5>
                {% if member.profile.team-position or member.profile.position %}
                  <h6 class="card-subtitle mb-2 text-muted">
                    {{ member.profile.team-position | default: member.profile.position }}
                  </h6>
                {% endif %}
                {% if member.teaser %}
                  <p class="card-text">{{ member.teaser }}</p>
                {% endif %}
                {% if member.profile.email %}
                  <a href="mailto:{{ member.profile.email }}" class="card-link"><i class="fas fa-envelope"></i></a>
                {% endif %}
                {% if member.profile.github %}
                  <a href="https://github.com/{{ member.profile.github }}" class="card-link" target="_blank"><i class="fab fa-github"></i></a>
                {% endif %}
                {% if member.profile.website %}
                  <a href="{{ member.profile.website }}" class="card-link" target="_blank"><i class="fas fa-globe"></i></a>
                {% endif %}
              </div>

              {% if member.inline == false %}</a>{% endif %}
            </div>
          </div>
        {% endfor %}
      </div>

    {% else %}
      <!-- Everyone else: keep the wide card layout -->
      {% for member in members %}
        <div class="card team-card {% if member.inline == false %}hoverable{% endif %}">
          <div class="row no-gutters">
            <div class="col-sm-4 col-md-3">
              <img src="{{ '/assets/img/team/' | append: member.profile.image | relative_url }}" class="card-img img-fluid" alt="{{ member.profile.name }}" />
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
                <p class="card-text">{{ member.teaser }}</p>
                {% if member.inline == false %}</a>{% endif %}
                {% if member.profile.email %}
                  <a href="mailto:{{ member.profile.email }}" class="card-link"><i class="fas fa-envelope"></i></a>
                {% endif %}
                {% if member.profile.phone %}
                  <a href="tel:{{ member.profile.phone }}" class="card-link"><i class="fas fa-phone"></i></a>
                {% endif %}
                {% if member.profile.orcid %}
                  <a href="https://orcid.org/{{ member.profile.orcid }}" class="card-link" target="_blank"><i class="fab fa-orcid"></i></a>
                {% endif %}
                {% if member.profile.twitter %}
                  <a href="https://twitter.com/{{ member.profile.twitter }}" class="card-link" target="_blank"><i class="fab fa-twitter"></i></a>
                {% endif %}
                {% if member.profile.github %}
                  <a href="https://github.com/{{ member.profile.github }}" class="card-link" target="_blank"><i class="fab fa-github"></i></a>
                {% endif %}
                {% if member.profile.website %}
                  <a href="{{ member.profile.website }}" class="card-link" target="_blank"><i class="fas fa-globe"></i></a>
                {% endif %}
              </div>
            </div>
          </div>
        </div>
      {% endfor %}
    {% endif %}
  </div>
{% endfor %}