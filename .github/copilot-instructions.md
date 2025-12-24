# Copilot Instructions for homahm.github.io

This is an academic personal website built with the **al-folio Jekyll theme**, designed for Homa Hosseinmardi (computational social scientist). The site showcases research, publications, team members, and academic activities.

## Architecture Overview

This is a **Jekyll-powered GitHub Pages site** with these key architectural components:
- **Jekyll Collections**: `_members/`, `_news/`, `_projects/` for structured academic content
- **Jekyll Scholar**: Bibliography management via `_bibliography/papers.bib` with custom citation formatting
- **Academic-specific layouts**: Custom `about.html`, `cv.html`, `profiles.html` layouts optimized for research portfolios
- **Docker containerization**: Development environment with Ruby, Jekyll, and academic plugins pre-configured

## Critical File Structure Patterns

### Academic Content Collections
- `_members/*.md`: Team member profiles with standardized frontmatter (`group`, `group_rank`, `profile` block)
- `_news/*.md`: News announcements with date-based naming (`announcement_N.md`) and inline posts
- `_projects/*.md`: Research project showcases with `importance`, `category`, and `related_publications` fields
- `_pages/`: Core site pages (`about.md`, `publications.md`, `cv.md`, `team.md`)

### Bibliography & Citations
- **Primary bibliography**: `_bibliography/papers.bib` - BibTeX entries with custom fields (`preview`, `bibtex_show`, `selected`)
- **Scholar configuration**: `_config.yml` defines author matching, citation style (APA), and display options
- **Publication badges**: Altmetric and Dimensions integration via `enable_publication_badges`

### Frontmatter Conventions
```yaml
# For academic pages
layout: about|cv|profiles
title: page_name
permalink: /path/
social: true  # Enable social links
news: true    # Show news feed
selected_papers: true  # Show featured publications

# For member profiles
group: "Research Assistants"|"Faculty"|"PhD Students"
group_rank: 1-10  # Display ordering within group
external: true    # For external collaborators
profile:
  image: filename.jpg
  role: "Position Title"
```

## Development Workflow

### Local Development
```bash
# Option 1: Docker (recommended for consistency)
docker-compose up
# Serves at localhost:8080 with live reload

# Option 2: Native Jekyll
bundle install
bundle exec jekyll serve --watch --livereload
```

### Key Jekyll Plugins
- `jekyll/scholar`: Academic bibliography processing
- `jekyll-jupyter-notebook`: Notebook rendering support  
- `jekyll-imagemagick`: Responsive image generation
- `jekyll-archives`: Tag/category/year-based archives

## Content Management Patterns

### Adding Publications
1. Add BibTeX entry to `_bibliography/papers.bib`
2. Use custom fields: `preview={image.png}`, `bibtex_show={true}`, `selected={true}`
3. Reference in projects via `related_publications: key1, key2`

### Team Member Workflow
1. Create `_members/lastname.md` with standardized frontmatter
2. Add profile image to `assets/img/`
3. Set `group` and `group_rank` for automatic organization on `/team/`

### News & Announcements
- Use `inline: true` for brief announcements
- Date format: `YYYY-MM-DD HH:MM:SS-OFFSET`
- HTML allowed in content for rich formatting

## Critical Dependencies

- **Jekyll Scholar**: Bibliography processing - breaking changes affect publication display
- **ImageMagick**: Required for responsive images - missing breaks asset processing
- **Node.js 20**: Required by build process and some plugins
- **Ruby gems**: Defined in `Gemfile` - version conflicts can break plugins

## Configuration Hotspots

- `_config.yml`: Scholar settings, social links, feature toggles
- `_data/cv.yml`: Structured CV data (education, experience, awards)
- `_sass/_variables.scss`: Theme colors and responsive breakpoints
- `assets/json/resume.json`: Machine-readable resume data

## Common Pitfalls

- **Bibliography changes**: Require Jekyll restart to rebuild scholar cache
- **Member photos**: Must be optimized - large images slow page loads significantly  
- **Frontmatter validation**: Missing required fields break collection pages
- **External links**: Configure in `_config.yml` external_links for proper handling
- **Docker volumes**: Changes to `_config.yml` trigger container restart via `entry_point.sh`

## Production Considerations

- **GitHub Pages limitations**: Some plugins require pre-building via GitHub Actions
- **Image optimization**: Enable `imagemagick` for WebP conversion and responsive sizing
- **Social media**: Verify Open Graph and Schema.org settings for proper sharing
- **Analytics**: Google Analytics integration via `google_analytics` config field