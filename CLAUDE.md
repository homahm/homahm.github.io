# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic personal website built with the **al-folio Jekyll theme** for Homa Hosseinmardi (computational social scientist). This is a **Jekyll-powered GitHub Pages site** that showcases research, publications, team members, and academic activities.

The al-folio theme is specifically designed for academics and provides features like:
- Automatic bibliography generation from BibTeX files
- Academic CV layouts with structured data
- Team member profiles with group organization
- Project showcases with publication linking
- Responsive design with dark mode support

## Development Commands

### Local Development

**Docker (Recommended for consistency):**
```bash
docker-compose up
# Serves at localhost:8080 with live reload
# Changes to _config.yml automatically trigger container restart
```

**Native Jekyll:**
```bash
bundle install
bundle exec jekyll serve --watch --livereload
# Default serves at localhost:4000
```

### Building
```bash
bundle exec jekyll build
# Outputs to _site/ directory
```

## Architecture Overview

### Jekyll Collections System
This site uses three custom collections for structured academic content:
- **`_members/`**: Team member profiles with group-based organization (filenames: `lastname.md`)
- **`_news/`**: News announcements with sequential naming (`announcement_0.md`, `announcement_1.md`, etc.)
- **`_projects/`**: Research project showcases with bibliography integration (filenames: `N_project.md`)

### Academic Bibliography System
- **Jekyll Scholar** processes `_bibliography/papers.bib` for publication management
- BibTeX entries support custom fields: `preview`, `bibtex_show`, `selected`
- Publications link to projects via `related_publications` frontmatter field
- Scholar configuration in `_config.yml` defines author matching and citation style (APA)

### Layout Architecture
Custom academic layouts in `_layouts/`:
- `about.html`: Homepage with profile, news feed, and social links
- `profiles.html`: Team member directory with group-based organization
- `cv.html`: Structured CV display from `_data/cv.yml`
- `bib.html`: Publication entry template with badges (Altmetric, Dimensions)

## Content Frontmatter Conventions

### Academic Pages (`_pages/`)
```yaml
layout: about|cv|profiles
title: page_name
permalink: /path/
social: true        # Enable social links
news: true          # Show news feed on page
selected_papers: true  # Show featured publications
```

### Member Profiles (`_members/`)
```yaml
layout: about
inline: false
group: "Co-founders"|"Research Assistants"|"Faculty"|"PhD Students"
group_rank: 1-10      # Display ordering within group
group_order: 1-10     # Group display order on team page
external: True        # For external collaborators (capital T)
title: Full Name
lastname: LastName    # Used for filename matching
publications: 'author^=*LastName'  # Scholar query for filtering
teaser: >             # Brief bio shown in listings
  Short description...
profile:
  name: Full Name
  position: Optional position field
  align: right
  image: filename.jpg  # Must exist in assets/img/
  role: Position Title
  email: user@ucla.edu
  website: https://example.com/
  github: username    # Optional
  orcid: 0000-0000-0000-0000  # Optional
```

### Projects (`_projects/`)
```yaml
layout: page
title: Project Title
description: Brief description
img: assets/img/preview.png
importance: 1-10    # Lower number = higher priority on display
category: category-slug  # Groups projects on /projects/ page (e.g., "information-ecosystems")
related_publications: bibtexkey1, bibtexkey2  # Links to bibliography (comma-separated)
publications_list:  # Optional: manually list publications instead of using related_publications
  - title: "Paper Title"
    authors: "Author1, Author2"
    year: 2024
    venue: "Venue Name"
```

### News Announcements (`_news/`)
```yaml
layout: post
date: YYYY-MM-DD HH:MM:SS-OFFSET
inline: true        # For brief announcements without dedicated page
related_posts: false
---
# HTML content allowed for rich formatting
```

## Bibliography Management

### Adding Publications
1. Add BibTeX entry to `_bibliography/papers.bib`
2. Use custom fields for display control:
   - `preview={image.png}`: Thumbnail image
   - `bibtex_show={true}`: Show BibTeX toggle
   - `selected={true}`: Feature on homepage
3. Reference in projects: `related_publications: key1, key2`

### Important Notes
- Bibliography changes require **Jekyll restart** to rebuild scholar cache
- Author matching configured in `_config.yml` under `scholar.last_name` and `scholar.first_name`
- Badge integration: `enable_publication_badges` in `_config.yml`

## Key Configuration Files

- **`_config.yml`**: Site-wide settings, Jekyll Scholar config, social links, feature toggles
- **`_data/cv.yml`**: Structured CV data (education, experience, awards)
- **`_sass/_variables.scss`**: Theme colors and responsive breakpoints
- **`assets/json/resume.json`**: Machine-readable resume data (loaded via `jekyll_get_json`)

## Critical Dependencies

- **Jekyll Scholar**: Bibliography processing - version changes may break publication display
- **ImageMagick**: Required for responsive image generation - missing breaks asset processing
- **Node.js 20**: Required by build process and plugins
- **Ruby gems**: Defined in `Gemfile` - maintain version compatibility

## Important Plugins

- `jekyll/scholar`: Academic bibliography processing
- `jekyll-jupyter-notebook`: Notebook rendering support
- `jekyll-imagemagick`: Responsive WebP image generation from JPG/PNG
- `jekyll-archives`: Tag/category/year-based blog archives
- `jekyll-paginate-v2`: Blog pagination
- `jekyll-email-protect`: Email obfuscation

## Critical Workflow Patterns

### Adding Team Members
1. Create `_members/lastname.md` with required frontmatter (see conventions above)
2. Add optimized profile image to `assets/img/` (large images slow page loads)
3. Set `group`, `group_rank`, and `group_order` for automatic organization on `/team/`
4. External collaborators: set `external: True` (capital T)
5. Use `publications` field to filter author's papers (e.g., `'author^=*LastName'`)

### Updating Publications
1. Edit `_bibliography/papers.bib` with new BibTeX entries
2. Restart Jekyll to rebuild scholar cache
3. Link publications to projects via `related_publications` field

### Docker Development Notes
- Config changes (`_config.yml`) trigger automatic container restart via `bin/entry_point.sh`
- The entry point script uses `inotifywait` to monitor config file changes
- Serves on port 8080 (not default 4000) with `--livereload` enabled

## Production Considerations

- **GitHub Pages**: Some plugins require pre-building via GitHub Actions workflow
- **Image optimization**: Enable `imagemagick` in `_config.yml` for WebP conversion
- **Responsive images**: Generated in widths 480px, 800px, 1400px (configured in `_config.yml`)
- **Open Graph/Schema.org**: Verify `serve_og_meta` and `serve_schema_org` settings for social media sharing

## File Structure Notes

- `_includes/`: Reusable HTML components (header, footer, social links, news feed, project cards)
- `_layouts/`: Page templates
- `_pages/`: Main site pages (about, publications, cv, team, projects)
- `_sass/`: SCSS stylesheets (variables, themes, layouts)
- `_site/`: Generated output (excluded from git)
- `assets/`: Static assets (images, JSON, PDFs)
- `bin/`: Build and deployment scripts
