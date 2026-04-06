# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Personal landing page for Pavel Rozentsvet (DevOps Engineer), built with Jekyll using the [al-folio](https://github.com/alshedivat/al-folio) theme. Deployed to GitHub Pages at https://paulroze.github.io via the `master` branch.

The site has 3 active pages: **About** (homepage), **CV**, and **Repositories**. Blog, projects, publications, and other al-folio features are disabled (pages removed or hidden with `nav: false`).

## Build & Dev Commands

```bash
# Local development with Docker (recommended)
docker compose up

# Without Docker (requires Ruby 3.2.2, bundler)
bundle install
bundle exec jekyll serve --livereload

# Production build (used by CI)
JEKYLL_ENV=production bundle exec jekyll build --lsi

# Format Liquid/HTML/JS files
npx prettier --write .

# PurgeCSS (post-build, run after jekyll build)
npx purgecss -c purgecss.config.js
```

The Docker container serves on port 8080 with live reload and auto-restarts on `_config.yml` changes.

## Architecture

- **`_config.yml`** — Central configuration: site metadata, social links, plugin settings. Most site-wide changes happen here.
- **`_pages/`** — Active pages: `about.md` (homepage, `permalink: /`), `cv.md`, `repositories.md`. Also contains `blog.md`, `projects.md`, `404.md` (hidden from nav).
- **`_data/cv.yml`** — CV content (experience, education, certifications, skills). Also mirrored in `assets/json/resume.json` for the JSON Resume format.
- **`_data/repositories.yml`** — GitHub users and repos displayed on the repositories page.
- **`_layouts/`** — Liquid templates. Key ones: `about.liquid`, `cv.liquid`, `page.liquid`.
- **`_includes/`** — Reusable Liquid partials (header, footer, social icons, comments, etc.).
- **`_sass/`** — SCSS partials. `_variables.scss` for theme customization, `_themes.scss` for light/dark mode.
- **`_plugins/`** — Custom Ruby plugins (cache busting, external posts, etc.).
- **`assets/`** — Static files: CSS, JS, images, fonts.

## Key Conventions

- **Front matter** — All content files use YAML front matter for layout, title, metadata.
- **Prettier** — Configured with `@shopify/prettier-plugin-liquid`, 150 char print width, ES5 trailing commas.
- **Pre-commit hooks** — Trailing whitespace, end-of-file fixer, YAML validation, large file check.
- **Deployment** — Push to `master` triggers GitHub Actions (`deploy.yml`) which builds with Jekyll, purges unused CSS, and deploys to GitHub Pages. Build output goes to `_site/`.

## Disabled Features

These al-folio features are not in use but the infrastructure remains if needed later:
- **Blog** — `_posts/` is empty, `_pages/blog.md` exists with `nav: false`
- **Projects** — `_projects/` is empty, `_pages/projects.md` exists with `nav: false`
- **Publications** — Jekyll Scholar plugin removed, `_bibliography/` is empty
- **News/Announcements** — `_news/` is empty, disabled in config
