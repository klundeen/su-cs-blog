# CS Perspectives

[Proposed] Faculty blog for Seattle University's Department of Computer Science.

## Quick Start

### GitHub Pages deployment

1. Create a new repo on GitHub (e.g., `su-cs-blog` or `cs-perspectives`)
2. Push this directory to the repo:
   ```bash
   cd su-cs-blog
   git init
   git add .
   git commit -m "Initial blog setup"
   git branch -M main
   git remote add origin git@github.com:klundeen/cs-perspectives.git
   git push -u origin main
   ```
3. In GitHub repo settings → Pages → Source, select **GitHub Actions**
4. The deploy workflow will run automatically on push
5. Your site will be live at `https://klundeen.github.io/cs-perspectives/`

### Local development

```bash
bundle install
bundle exec jekyll serve
# Site available at http://localhost:4000
```

### Writing a new post

Create a file in `_posts/` named `YYYY-MM-DD-your-title.md`:

```markdown
---
layout: post
title: "Your Post Title"
subtitle: "Optional subtitle"
date: 2026-04-01
author: Your Name
author_title: "Your Title, Department of Computer Science"
---

Your post content in Markdown.
```

## Structure

```
├── _config.yml          # Site configuration
├── _layouts/
│   ├── default.html     # Base layout (header, footer)
│   └── post.html        # Blog post layout
├── _posts/              # Blog posts (Markdown)
├── assets/css/
│   └── style.css        # SU-branded stylesheet
├── index.html           # Blog index page
├── about.md             # About page
└── .github/workflows/
    └── deploy.yml       # GitHub Pages CI/CD
```

## Brand

Uses Seattle University's brand-approved free alternate typefaces:
- **Oswald** (headlines) — alternate for Knockout
- **Montserrat** (body) — alternate for Neutraface 2
- **Roboto Slab** (accent) — alternate for Neutraface Slab

Primary color: SU Red `#AA0000`
