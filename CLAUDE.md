# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for **Airsoft Rhône Immersion (ARI)**, a French airsoft association. Built with Hugo extended + Tailwind CSS 4, based on the `hugoplate` theme. All content is in French.

## Commands

```bash
npm run dev          # Local dev server with live reload at http://localhost:1313/
npm run build        # Production build (minified, with GC)
npm run preview      # Preview production build locally
npm run format       # Format with Prettier (supports Go templates)
npm run project-setup  # Initialize project / install Hugo modules (run once after clone)
```

**Prerequisites:** Hugo extended 0.151.0+, Go 1.21+, Node.js 18.16.1+

## Architecture

### Theme System

This project uses `hugoplate` as a Hugo module theme. **Never modify files inside `themes/hugoplate/`** — override them by creating matching files under `layouts/` or `assets/`.

### Configuration

- `config/_default/hugo.toml` — core site settings (URL, imaging, markup, outputs)
- `config/_default/params.toml` — theme parameters (logo, navbar, search, feature toggles)
- `config/_default/menus.toml` — navigation (5 main sections with dropdowns + footer)
- `config/_default/module.toml` — 22 Hugo module imports (search, PWA, icons, SEO, etc.)

### Design Tokens

`data/theme.json` defines colors and fonts. During `npm run dev` / `npm run build`, `scripts/themeGenerator.js` reads these tokens and generates Tailwind CSS classes. Edit `data/theme.json` to change colors or fonts — do not hardcode them in CSS.

### Content

All content lives in `content/` (single French-language site):
- `content/pages/` — static pages rendered at their slug
- `content/sections/` — homepage sections (not rendered as standalone pages; referenced from `layouts/home.html`)
- `content/blog/` — blog posts
- `content/_index.md` — homepage front matter

### Layouts

- `layouts/home.html` — homepage: renders banner then iterates over `sections/`
- `layouts/single.html` — single page layout
- `layouts/shortcodes/` — custom shortcodes: `features`, `columns`/`column`, `gslides`
- `layouts/_partials/` — reusable template partials (head, footer, call-to-action, etc.)

### Assets & Styling

- `assets/css/main.css` — Tailwind CSS entry point; processed through Hugo Pipes
- `assets/images/` — images processed by Hugo (WebP generation, Lanczos resampling)
- CSS cache busting is driven by `hugo_stats.json` — Hugo regenerates it on class usage changes

### Social & Data

- `data/social.json` — social links (Discord, Facebook, YouTube)

## Deployment

The site deploys to GitHub Pages via `.github/workflows/` on push to `main`. Config files for Netlify (`netlify.toml`), Vercel (`vercel.json`), and AWS Amplify (`amplify.yml`) are also present.
