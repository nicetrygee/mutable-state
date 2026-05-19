# mutable state

A minimal personal blog built with Hugo.

## Local setup

1. **Install Hugo** — download the binary for your OS from https://gohugo.io/installation/
   - Mac: `brew install hugo`
   - Windows: `winget install Hugo.Hugo.Extended`
   - Linux: `snap install hugo`

2. **Run locally:**
   ```bash
   hugo server
   ```
   Open http://localhost:1313 — live reloads as you edit.

## Writing a post

Create a new Markdown file in `content/posts/`:

```bash
hugo new content posts/your-post-title.md
```

Or just create the file manually with this front matter:

```markdown
---
title: Your Post Title
tagline: An optional one-line description
date: 2025-05-18
---

Your content here...
```

The `tagline` is optional — it appears after the · separator on the homepage.

## Deploy to GitHub Pages

1. Create a new repo on GitHub and push this folder to it
2. Go to **Settings → Pages → Source: GitHub Actions**
3. Push to `main` — the workflow in `.github/workflows/deploy.yml` builds and deploys automatically
4. Your site will be live at `https://USERNAME.github.io/REPO-NAME/`

   If using a custom domain, add a `CNAME` file in the `static/` folder containing your domain,
   then configure your DNS. See: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

   Also update `baseURL` in `hugo.toml` to your domain.

## Customise

- **Site title, author, URL**: edit `hugo.toml`
- **Styles**: edit `static/assets/style.css`
- **Homepage layout**: edit `layouts/index.html`
- **Post layout**: edit `layouts/_default/single.html`
- **Base template** (header/footer): edit `layouts/_default/baseof.html`
