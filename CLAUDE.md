# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A minimal personal blog (Gregg Roseker's "mutable state") built with Hugo, deployed to GitHub Pages at `nicetrygee.github.io/mutable-state`. No JS framework, no build tooling beyond Hugo itself — styles are inlined in `layouts/_default/baseof.html`.

## Commands

```bash
hugo server          # local dev server at http://localhost:1313, live reload
hugo new content posts/your-post-title.md   # scaffold a new post (use posts/your-post-title/index.md if it will have images)
hugo --minify         # production build (what CI runs), outputs to ./public
```

There is no test suite, linter, or package manager — Hugo is the only dependency (`brew install hugo`).

## Architecture

- **Content is Markdown with front matter** in `content/posts/*.md`. Required fields: `title`, `date`. Optional: `tagline` (shown after `·` on the homepage post list).
- **Images in posts (one convention)**: a post with images is a page bundle, `content/posts/<slug>/index.md`, with its images in the same folder. Reference them with plain Markdown and relative paths, putting the caption in the title: `![alt text](screenshot.png "Caption")`. Never use `/`-prefixed paths or `static/` for post images: the site lives under `/mutable-state/`, so they break. `layouts/_default/_markup/render-image.html` renders an image on its own line as a `<figure>` with a `<figcaption>`, resolves the path with the right prefix, and **fails the build** if the file isn't in the post's folder. (`hugo.toml` sets `wrapStandAloneImageWithinParagraph = false` for this.) The About page photo is separate: it's set by the `photo` front-matter param.
- **Permalinks are flattened**: `[permalinks] posts = "/:slug/"` in `hugo.toml` means posts publish at `/post-slug/`, not `/posts/post-slug/`.
- **Three templates, total**, under `layouts/`:
  - `_default/baseof.html` — the shell (head, inline `<style>`, header, footer). All page chrome and CSS lives here — there is no separate stylesheet in use for page layout (`static/assets/style.css` exists but is not wired into `baseof.html`).
  - `index.html` — homepage; groups posts by year (`GroupByDate "2006"`) via `{{ define "main" }}`.
  - `_default/single.html` — individual post rendering.
  - Changing site-wide look and feel (colors, fonts, spacing) means editing the `<style>` block in `baseof.html` directly.
- **Analytics**: GoatCounter (cookieless). The site code is `goatcounter` under `[params]` in `hugo.toml`; `baseof.html` adds the script only when `hugo.IsProduction`, so `hugo server` visits aren't counted. Dashboard: https://nicetrygree.goatcounter.com
- **Deploy**: `.github/workflows/deploy.yml` builds with `hugo --minify` and publishes to GitHub Pages on every push to `main` (via `actions/deploy-pages`). Pushing to `main` deploys — there's no separate release step.
- `public/` is the Hugo build output and is gitignored; don't hand-edit it.
