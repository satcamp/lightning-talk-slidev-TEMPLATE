# SatCamp Lightning Talk Template (Slidev)

A [Slidev](https://sli.dev) template for 5-minute [SatCamp](https://satcamp.xyz) lightning talks. Slides auto-advance every 15 seconds. 20 slides × 15 seconds = 5 minutes.

**Live demo:** https://satcamp.github.io/lightning-talk-slidev-TEMPLATE/

---

## Create your own deck

1. Go to **[Use this template](https://github.com/new?template_name=lightning-talk-slidev-TEMPLATE&template_owner=satcamp)** on GitHub
2. Create a new repository under your account
3. Clone it locally and follow the setup steps below

---

## Setup

This project uses [pnpm](https://pnpm.io/).

```bash
pnpm install
pnpm dev
```

Open http://localhost:3030 in your browser. Append `?noauto` to the URL to pause auto-advance during editing.

---

## What to edit

| What | Where |
|---|---|
| Talk title and author | Top of `slides.md` (frontmatter `title:` field and first slide) |
| Your 6 content slides | Slides 12–17 — replace `[Hook]`, `[Problem]`, `[Idea]`, `[Steps]`, `[Demo]`, `[Results]` |
| Links slide | Slide 20 — replace the satcamp.xyz links with your own |
| Slide timing | `SLIDE_MS = 15_000` in `global-bottom.vue` (value in milliseconds) |

**Before presenting:** delete slide 19 ("Make it yours") so the deck has exactly 20 slides.

---

## Enable GitHub Pages

1. In your repo, go to **Settings → Pages**
2. Under **Source**, select **GitHub Actions**
3. Push any change to `main` — the workflow in `.github/workflows/publish.yml` will build and deploy automatically
4. Your deck will be live at `https://<your-username>.github.io/<repo-name>/`
