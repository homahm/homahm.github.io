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

### Production Build (with LSI and CSS optimization)
```bash
JEKYLL_ENV=production bundle exec jekyll build --lsi
purgecss -c purgecss.config.js
```

### Quick Local Preview (without Docker/Jekyll)
```bash
cd _site && python3 -m http.server 8000
# Serves at localhost:8000
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
group: "Team Members"|"Co-founders"|"Research Assistants"|"Faculty"
group_rank: 1-10      # Display ordering within group
group_order: 1-10     # Group display order on team page
external: True        # For external collaborators (capital T)
title: Full Name
lastname: LastName    # Used for filename matching
publications: 'author^=*LastName'  # Scholar query for filtering
teaser: >             # Brief bio shown in listings
  Short description...
profile:
  name: Full Name           # Append "(Collaborator)" for external members
  position: Optional position field
  align: right
  image: filename.jpg       # Must exist in BOTH assets/img/ AND assets/img/team/
  role: Position Title
  email: user@ucla.edu
  website: https://example.com/
  github: username    # Optional
  orcid: 0000-0000-0000-0000  # Optional
```

**Important**: Member profile images must be placed in **both** `assets/img/` (for the about layout on individual pages) and `assets/img/team/` (for the team listing page). The team page template prepends `/assets/img/team/` to the image path, while the about layout prepends `assets/img/`. Omit empty optional fields entirely rather than leaving them blank (blank values can cause build errors).

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
- **`_data/coauthors.yml`**: Co-author profile data for publication disambiguation
- **`_data/repositories.yml`**: GitHub repositories to display on site
- **`_data/venues.yml`**: Venue/conference data for publications
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
2. Add optimized profile image to **both** `assets/img/` and `assets/img/team/` (large images slow page loads)
3. Use square-cropped images for consistency with existing team member photos
4. Set `group`, `group_rank`, and `group_order` for automatic organization on `/team/`
5. External collaborators: set `external: True` (capital T) and add "(Collaborator)" to the `profile.name` field
6. Use `publications` field to filter author's papers (e.g., `'author^=*LastName'`)

### Navigation Structure
- Top-level pages use `nav: true` and `nav_order` in frontmatter
- Dropdown menus are defined in separate `.md` files with `dropdown: true` and `children` list
- To nest a page under a dropdown: set `nav: false` on the page, add it as a child in the dropdown file
- Example dropdown file (`_pages/resources.md`):
  ```yaml
  layout: page
  title: resources
  nav: true
  nav_order: 6
  dropdown: true
  children:
      - title: cv
        permalink: /cv/
      - title: conferences
        permalink: /conferences/
  ```

### Updating Publications
1. Edit `_bibliography/papers.bib` with new BibTeX entries
2. Restart Jekyll to rebuild scholar cache
3. Link publications to projects via `related_publications` field

### Docker Development Notes
- Config changes (`_config.yml`) trigger automatic container restart via `bin/entry_point.sh`
- The entry point script uses `inotifywait` to monitor config file changes
- Serves on port 8080 (not default 4000) with `--livereload` enabled

## Deployment

- **GitHub Actions** automatically builds and deploys on push to `master` branch
- The workflow builds with `--lsi` (Latent Semantic Indexing), runs PurgeCSS, and deploys to `gh-pages` branch
- A `.nojekyll` file is created during deployment to bypass GitHub Pages' built-in Jekyll processing
- Manual deployment available via `bin/deploy` script

## Production Considerations

- **GitHub Pages**: Some plugins require pre-building via GitHub Actions workflow
- **Image optimization**: Enable `imagemagick` in `_config.yml` for WebP conversion
- **Responsive images**: Generated in widths 480px, 800px, 1400px (configured in `_config.yml`)
- **Open Graph/Schema.org**: Verify `serve_og_meta` and `serve_schema_org` settings for social media sharing

## Site Structure

### Current Page Routing
- `/` → About/homepage (`_pages/about.md`)
- `/team.html` → OASIS Lab team page (`_pages/team.md`)
- `/projects/` → Research projects (`_pages/projects.md`)
- `/publications/` → Publications (`_pages/publications.md`)
- `/cv/` → CV (under "resources" dropdown)
- `/conferences/` → Conferences list (under "resources" dropdown)

### File Structure
- `_includes/`: Reusable HTML components (header, footer, social links, news feed, project cards)
- `_layouts/`: Page templates
- `_pages/`: Main site pages (about, publications, cv, team, projects, conferences, resources)
- `_sass/`: SCSS stylesheets (variables, themes, layouts)
- `_site/`: Generated output (excluded from git)
- `assets/img/`: General images and member profile images (for about layout)
- `assets/img/team/`: Member profile images (for team listing page)
- `assets/pdf/`: PDF files (CV, papers)
- `bin/`: Build and deployment scripts

## Troubleshooting

- **Build requires UTF-8**: Use `LANG=en_US.UTF-8 bundle exec jekyll build` if BibTeX encoding fails
- **ImageMagick warnings**: `convert: command not found` warnings are safe to ignore locally; images will use originals
- **`.jekyll-cache/`**: Delete this directory if builds seem stale after major changes
- **Bibliography not updating**: Requires full Jekyll restart (not just live reload)
- **Member image not showing**: Ensure the image exists in both `assets/img/` and `assets/img/team/`
