# CLAUDE.md

This file provides guidance to AI assistants (Claude and others) working in this repository.

## Repository Overview

**Repository:** `raz-nussbaum-cc-github.io`
**Type:** GitHub Pages personal website
**Purpose:** Personal portfolio/website hosted at `https://raz-nussbaum.github.io` (or a custom domain if configured)

This is a freshly initialized GitHub Pages repository with no content yet. GitHub Pages serves static files directly from the repository root (or a `/docs` folder, or a `gh-pages` branch, depending on configuration).

## GitHub Pages Basics

GitHub Pages can host:
- **Plain HTML/CSS/JS** — files served as-is from the repo root
- **Jekyll sites** — GitHub Pages natively builds Jekyll projects; no separate build step needed when pushing to GitHub
- **Pre-built static sites** — output from any static site generator (Hugo, Gatsby, Next.js export, Astro, etc.) committed directly

## Recommended Development Workflows

### If using Jekyll (GitHub's default)

```bash
# Install dependencies (requires Ruby + Bundler)
bundle install

# Serve locally with live reload
bundle exec jekyll serve --livereload

# Build for production (GitHub builds this automatically on push)
bundle exec jekyll build
```

Key files:
- `_config.yml` — site-wide configuration (title, baseurl, theme, plugins)
- `Gemfile` — Ruby gem dependencies
- `_layouts/` — page layout templates
- `_includes/` — reusable HTML partials
- `_posts/` — blog posts (named `YYYY-MM-DD-title.md`)
- `_data/` — YAML/JSON/CSV data files
- `_sass/` — Sass partials
- `assets/` — static assets (CSS, JS, images)

### If using a Node.js-based static site generator

```bash
# Install dependencies
npm install

# Start development server
npm run dev       # or: npm start

# Build for production
npm run build

# Preview production build
npm run preview
```

### Plain HTML

No build step required. Open `index.html` in a browser or use a local server:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## File & Directory Conventions

| Path | Purpose |
|------|---------|
| `index.html` / `index.md` | Site homepage |
| `_config.yml` | Jekyll configuration |
| `assets/` | Static assets (CSS, JS, images, fonts) |
| `_layouts/` | Jekyll layout templates |
| `_includes/` | Jekyll reusable partials |
| `_posts/` | Blog posts (Jekyll) |
| `404.html` | Custom 404 error page |
| `CNAME` | Custom domain configuration |
| `.nojekyll` | Disables Jekyll processing (use for pre-built sites) |

## Git Workflow

### Branch Strategy

- `main` (or `master`) — production branch; GitHub Pages deploys from here
- Feature branches — use descriptive names: `feature/add-portfolio-section`, `fix/nav-mobile-layout`
- Claude branches — prefixed `claude/` per session convention

### Commit Style

Use concise, imperative commit messages:

```
Add portfolio projects section
Fix mobile navigation overflow
Update about page with current bio
Remove outdated work experience entry
```

### Deploying

Push to the configured GitHub Pages branch (`main` by default). GitHub automatically builds and deploys within ~1 minute.

```bash
git push origin main
```

## Content Conventions

- Use semantic HTML (`<header>`, `<nav>`, `<main>`, `<article>`, `<footer>`)
- Optimize images before committing (target <200KB per image; use WebP where possible)
- Keep CSS/JS minimal; prefer native browser features over heavy frameworks for a personal site
- Ensure the site is accessible: add `alt` text to all images, use sufficient color contrast, ensure keyboard navigation works

## Common Gotchas

- **`baseurl`** — If the site is hosted at a subpath (e.g., `username.github.io/repo-name`), set `baseurl: /repo-name` in `_config.yml` and use `{{ site.baseurl }}/path` for internal links
- **`username.github.io` repos** — For personal/org sites (this repo), `baseurl` is usually empty and the site serves from the root
- **`.nojekyll`** — Add this empty file to the repo root if you are committing a pre-built static site and do not want GitHub to run Jekyll on it
- **Large files** — Do not commit binaries, videos, or node_modules; use `.gitignore` appropriately
- **CNAME file** — If using a custom domain, GitHub creates this automatically via Settings; do not delete it

## Security Considerations

- Never commit secrets, API keys, or credentials to this repository — it is public
- Use environment variables or GitHub Actions secrets for any build-time secrets
- Be cautious with third-party JavaScript includes; prefer self-hosted assets or reputable CDNs

## Setting Up (First Time)

1. Choose your site generator (Jekyll recommended for simplicity with GitHub Pages)
2. Create the initial site structure
3. Configure `_config.yml` (or equivalent) with site title, description, and author info
4. Add `index.html` or `index.md` as the homepage
5. Push to `main` — GitHub Pages will automatically build and deploy
6. (Optional) Configure a custom domain under repository Settings → Pages
