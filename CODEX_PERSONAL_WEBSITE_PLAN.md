# Codex Implementation Brief: Personal Academic Website with Hidden Blog

## 0. Goal

Build a clean, professional, maintainable personal academic website for Ruihong Cen, hosted on GitHub Pages.

The visible website should have only four public navigation entries:

- Home
- Publications
- Projects
- About

The site should also include a hidden blog/writing section. The blog must be accessible by direct URL only, but must not appear in the header, footer, homepage, sitemap navigation, or any visible menu.

Recommended hidden route:

```txt
/writing/
/writing/[slug]/
```

Do **not** use `/blog/` unless the user explicitly changes this decision. `/writing/` is more subtle and more compatible with an academic personal website.

The website should support:

- Static deployment to GitHub Pages
- Light/dark mode toggle
- MDX-based writing posts
- Math rendering for technical notes
- Code highlighting
- Clean publication/project management through structured content files
- Professional academic visual style

The design should be minimal, modern, readable, and research-oriented. Avoid flashy animations and overly decorative UI.

---

## 1. Recommended Tech Stack

Use:

```txt
Astro + MDX + Tailwind CSS + GitHub Pages + GitHub Actions
```

Required integrations/libraries:

- Astro
- MDX integration
- Tailwind CSS
- Shiki or Astro's built-in code highlighting
- KaTeX or rehype-katex / remark-math for math rendering
- A small client-side theme toggle script for light/dark mode

Optional but useful later:

- Pagefind for static search, but do not implement in v1 unless requested
- Giscus comments, but do not implement in v1
- RSS feed, optional only for public content; do not include hidden writing unless requested

---

## 2. Information Architecture

Visible routes:

```txt
/
/publications/
/projects/
/about/
```

Hidden routes:

```txt
/writing/
/writing/[slug]/
```

The header navigation must contain only:

```txt
Home | Publications | Projects | About
```

The footer may contain:

```txt
Email | GitHub | Google Scholar | LinkedIn | CV
```

The footer must not link to `/writing/`.

The homepage must not show recent writing/blog posts.

---

## 3. Visual Design Requirements

Style direction:

```txt
minimal academic × modern engineering
```

Design principles:

- White/light background in light mode
- Near-black or deep gray background in dark mode
- Clean typography
- Generous spacing
- Narrow readable content width for text-heavy pages
- No heavy shadows
- No gimmicky effects
- Subtle borders and muted colors
- Strong readability for math/code

Recommended typography:

- Sans-serif: Inter, IBM Plex Sans, Source Sans 3, or system font stack
- Monospace: JetBrains Mono, IBM Plex Mono, or system monospace

Suggested layout widths:

```txt
Main container: max-width 960px to 1120px
Article content: max-width 720px to 800px
Publication/project list: max-width 900px to 1000px
```

Light/dark mode:

- Use class-based dark mode, e.g. `<html class="dark">`
- Store user preference in `localStorage`
- Respect system preference on first visit
- Avoid flash of incorrect theme by adding a small inline script in the document head

---

## 4. Suggested Repository Structure

```txt
personal-website/
├── public/
│   ├── favicon.svg
│   ├── cv.pdf
│   ├── images/
│   │   ├── profile.jpg
│   │   ├── publications/
│   │   ├── projects/
│   │   └── writing/
│   └── robots.txt
│
├── src/
│   ├── content/
│   │   ├── publications/
│   │   │   └── publications.json
│   │   ├── projects/
│   │   │   ├── shellular-homogenization.md
│   │   │   └── llm-paper-digest-agent.md
│   │   └── writing/
│   │       ├── flow-matching-vs-diffusion.md
│   │       └── jvp-trace-estimator.md
│   │
│   ├── layouts/
│   │   ├── BaseLayout.astro
│   │   ├── PageLayout.astro
│   │   ├── WritingPostLayout.astro
│   │   └── ProjectLayout.astro
│   │
│   ├── pages/
│   │   ├── index.astro
│   │   ├── publications.astro
│   │   ├── projects/
│   │   │   ├── index.astro
│   │   │   └── [...slug].astro
│   │   ├── about.astro
│   │   └── writing/
│   │       ├── index.astro
│   │       └── [...slug].astro
│   │
│   ├── components/
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   ├── ThemeToggle.astro
│   │   ├── PublicationItem.astro
│   │   ├── ProjectCard.astro
│   │   ├── WritingPostCard.astro
│   │   └── Seo.astro
│   │
│   ├── styles/
│   │   └── global.css
│   │
│   └── content.config.ts
│
├── astro.config.mjs
├── package.json
├── tsconfig.json
└── .github/
    └── workflows/
        └── deploy.yml
```

---

## 5. Content Models

Use Astro Content Collections for projects and writing posts. Publications may be either a JSON file or a collection. Prefer JSON for easier manual ordering.

### 5.1 Writing Post Frontmatter

Each hidden writing post should use this schema:

```yaml
---
title: "Flow Matching vs Diffusion for Multi-Solution Physics"
description: "A technical reflection on whether flow-based generative models are suitable for modeling multi-solution equilibria in nonlinear mechanics."
date: 2026-05-17
updated: 2026-05-17
tags: ["flow matching", "diffusion", "physical simulation", "generative AI"]
draft: false
noindex: true
---
```

Rules:

- `draft: true` posts must not be rendered in production.
- All writing posts should default to `noindex: true`.
- Writing posts should support LaTeX math and code blocks.

### 5.2 Project Frontmatter

```yaml
---
title: "Shellular Structure Homogenization"
description: "Homogenization pipeline for shell-based cellular structures using trace finite element shell simulation."
date: 2026-05-17
status: "ongoing"
tags: ["shell", "homogenization", "simulation"]
github: ""
paper: ""
featured: true
---
```

Project page sections should support:

- Overview
- Motivation
- Method
- Results
- Related publications
- Code/demo links, if available

### 5.3 Publication Data Model

Use `src/content/publications/publications.json`:

```json
[
  {
    "title": "Paper Title",
    "authors": ["Ruihong Cen", "Coauthor A", "Coauthor B"],
    "venue": "Conference / Journal / Preprint",
    "year": 2026,
    "status": "published",
    "links": {
      "paper": "",
      "project": "",
      "code": "",
      "bibtex": ""
    },
    "summary": "One-sentence summary of the work.",
    "selected": true
  }
]
```

Publication page requirements:

- Reverse chronological order by year
- Selected publications may be visually emphasized
- Author name `Ruihong Cen` should be bolded
- Empty links should not be rendered

---

## 6. Page Requirements

### 6.1 Home Page `/`

The homepage should include:

1. Hero section
   - Name: Ruihong Cen
   - Short identity line, e.g.:
     `PhD researcher in computer graphics, physical simulation, and computational design.`
   - Short research summary
   - Links: Email, GitHub, Google Scholar, CV

2. Research interests
   - Physical simulation
   - Shell mechanics / shellular structures / homogenization
   - Differentiable simulation
   - Generative AI for computational design
   - LLM-based design agents

3. Selected publications
   - Show 2 to 4 selected publications
   - Link to `/publications/`

4. Featured projects
   - Show 2 to 4 featured projects
   - Link to `/projects/`

Do not show writing/blog posts on the homepage.

### 6.2 Publications Page `/publications/`

The publications page should be clean and academic.

Requirements:

- Title: `Publications`
- Group by year or list reverse chronologically
- Show authors, venue/status, year, and links
- Use compact but readable spacing
- Bold Ruihong Cen in author lists

### 6.3 Projects Page `/projects/`

Requirements:

- Title: `Projects`
- Card/list layout
- Each project card shows title, description, tags, status, and optional links
- Dynamic project detail route at `/projects/[slug]/`

### 6.4 About Page `/about/`

Requirements:

- Short biography
- Research interests
- Education
- Experience, if provided
- Skills/tooling, optional
- Contact links
- CV download link

### 6.5 Hidden Writing Page `/writing/`

Requirements:

- Route exists and can be accessed directly
- Not linked from header, footer, homepage, or public nav
- Has `<meta name="robots" content="noindex, nofollow">`
- Lists non-draft writing posts
- Simple title such as `Writing`
- Subtitle: `Technical notes, research thoughts, and informal essays.`

### 6.6 Writing Post Pages `/writing/[slug]/`

Requirements:

- Also use `<meta name="robots" content="noindex, nofollow">`
- Render title, description, date, updated date, and tags
- Support math and code highlighting
- Keep layout narrow and readable
- No comments in v1

---

## 7. SEO and Privacy Requirements

Public pages:

```html
<meta name="robots" content="index, follow">
```

Hidden writing pages:

```html
<meta name="robots" content="noindex, nofollow">
```

Important: `/writing/` is not truly private. It is public but unlisted and de-indexed. Do not treat it as secure storage.

Sitemap:

- Prefer excluding `/writing/` from sitemap.
- If implementing automatic sitemap, configure it to avoid hidden writing routes.

Robots.txt:

```txt
User-agent: *
Disallow: /writing/
```

This is a discoverability reduction, not a security boundary.

---

## 8. Astro Configuration Requirements

`astro.config.mjs` must be correct for GitHub Pages.

If deploying to the user site repository:

```txt
ruihongcen11.github.io
```

use:

```js
import { defineConfig } from 'astro/config';
import mdx from '@astrojs/mdx';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  site: 'https://ruihongcen11.github.io',
  integrations: [mdx()],
  vite: {
    plugins: [tailwindcss()],
  },
});
```

If deploying to a project repository, for example:

```txt
personal-website
```

then use:

```js
import { defineConfig } from 'astro/config';
import mdx from '@astrojs/mdx';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  site: 'https://ruihongcen11.github.io',
  base: '/personal-website',
  integrations: [mdx()],
  vite: {
    plugins: [tailwindcss()],
  },
});
```

Prefer deploying from the existing `ruihongcen11.github.io` repository if the user wants it as the primary personal homepage.

---

## 9. GitHub Actions Deployment Workflow

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: npm

      - name: Install dependencies
        run: npm ci

      - name: Build
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

The repository's GitHub Pages source must be configured to use GitHub Actions.

---

## 10. Theme Toggle Requirements

Implement a theme toggle that:

- Defaults to system preference if no saved preference exists
- Saves selected mode in `localStorage`
- Applies `dark` class to `<html>`
- Avoids flash of incorrect theme with an inline script in the `<head>`

Pseudo logic:

```js
const saved = localStorage.getItem('theme');
const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
const shouldUseDark = saved ? saved === 'dark' : prefersDark;
document.documentElement.classList.toggle('dark', shouldUseDark);
```

UI:

- Small button in header
- Use text/icon: `Light`, `Dark`, or sun/moon icon
- Must be keyboard accessible
- Must have `aria-label`

---

## 11. Content and Copy Placeholders

Use placeholders where exact content is unknown.

Home hero draft:

```txt
Ruihong Cen
PhD researcher in computer graphics, physical simulation, and computational design.

I work on physically based simulation, shell and solid mechanics, differentiable simulation, and generative AI methods for computational design.
```

Research interests draft:

```txt
- Physically based simulation
- Shell mechanics and shellular structures
- Homogenization and computational mechanics
- Differentiable simulation and inverse design
- Generative AI for physical design
- LLM-based computational design agents
```

About draft:

```txt
I am a PhD researcher working at the intersection of computer graphics, computational mechanics, and generative AI. My research interests include physically based simulation, shell and solid mechanics, differentiable simulation, and AI-assisted computational design.
```

Do not invent publications. Use placeholder publication entries only if needed, clearly marked as placeholders.

---

## 12. Quality Checklist

Before final delivery, verify:

- `npm install` works
- `npm run dev` works
- `npm run build` works
- `npm run preview` works
- Header contains exactly: Home, Publications, Projects, About
- Footer does not link to writing/blog
- Homepage does not show writing/blog
- `/writing/` exists and is accessible directly
- `/writing/` has noindex/nofollow
- `/writing/[slug]/` has noindex/nofollow
- Dark/light toggle works
- Math rendering works
- Code highlighting works
- Publications page handles empty links gracefully
- Projects page renders project cards correctly
- GitHub Actions workflow is present
- `astro.config.mjs` has correct `site` and optional `base`

---

## 13. Suggested First Writing Posts for Testing

Create 2 sample hidden writing posts:

1. `flow-matching-vs-diffusion.md`
2. `jvp-trace-estimator.md`

Each should contain:

- Frontmatter
- One paragraph of placeholder text
- One LaTeX display equation
- One code block

Example equation:

```latex
\frac{d}{dt}\log p_t(\phi_t(x)) = -\nabla \cdot v_t(\phi_t(x))
```

Example code block:

```python
import torch

x = torch.randn(16, 3)
print(x.shape)
```

---

## 14. Implementation Priority

Build in this order:

1. Initialize Astro project
2. Add MDX and Tailwind
3. Create base layout, header, footer, theme toggle
4. Create public pages: Home, Publications, Projects, About
5. Create content collections for projects and writing
6. Create hidden writing routes
7. Add math/code rendering
8. Add noindex/no robots handling for writing
9. Add GitHub Actions deployment
10. Test production build

