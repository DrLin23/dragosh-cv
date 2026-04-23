# dragosh.dev (working title)

Personal CV / landing page for Dragosh Vatamanu.
Built with [Astro](https://astro.build) + [Tailwind CSS v4](https://tailwindcss.com).

## Run it

```sh
npm install     # first time only
npm run dev     # local dev server at http://localhost:4321
npm run build   # production build to ./dist
npm run preview # serve the production build locally
```

## Structure

```
src/
  components/          section components (Hero, About, Education, Projects, Skills, Contact, …)
  content/projects/    one markdown file per project — add files here to add projects
  content.config.ts    schema for the projects collection
  layouts/Layout.astro HTML shell, fonts, meta tags
  pages/index.astro    single-page homepage that composes everything
  styles/global.css    Tailwind entry + design tokens (colours, fonts)
public/                static assets (favicon, CV PDF, images)
```

## Adding a project

1. Drop a new file at `src/content/projects/my-thing.md`
2. Fill out the frontmatter:

```yaml
---
title: "Project title"
summary: "One-sentence pitch."
date: 2026-04-20
tech: ["TypeScript", "React"]
link: "https://live-url.example"   # optional
repo: "https://github.com/you/x"   # optional
featured: true                     # optional
draft: false                       # set to true to hide
---
```

That's it — the homepage picks it up automatically and sorts by date.

## Editing the look

- **Colours / fonts**: `src/styles/global.css` (`@theme` block)
- **Copy**: each section lives in `src/components/*.astro`
- **Order of sections**: `src/pages/index.astro`

## Deploying to Cloudflare Pages (recommended)

Cloudflare Pages builds from your GitHub repo and deploys on every push.

1. **Push to GitHub**
   ```sh
   gh repo create dragosh-cv --public --source=. --push
   # or manually: create the repo on github.com, then
   # git remote add origin git@github.com:<you>/dragosh-cv.git
   # git push -u origin main
   ```

2. **Connect Cloudflare Pages**
   - Go to https://dash.cloudflare.com → Workers & Pages → Create → Pages → Connect to Git
   - Pick the repo
   - Framework preset: **Astro**
   - Build command: `npm run build`
   - Build output directory: `dist`
   - Deploy

3. **Custom domain** (when you get one)
   - Pages → your project → Custom domains → Add
   - Point DNS at Cloudflare per their instructions

## Deploying to GitHub Pages (alternative)

If you'd rather stay entirely on GitHub:

1. Follow https://docs.astro.build/en/guides/deploy/github/ to create `.github/workflows/deploy.yml`.
2. Repo settings → Pages → Source: **GitHub Actions**.
3. Add `site: "https://<you>.github.io"` and (if project page) `base: "/<repo>"` to `astro.config.mjs`.

Cloudflare Pages is simpler and faster, but GitHub Pages works fine if you prefer one fewer account.
