# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file static marketing website for **Vikara**, an education consultancy. The entire site lives in `index.html` — no build step, no bundler, no framework, no external JS dependencies. Deploy via Vercel (project: `vikara`, org: `team_w3R1N8IdrVmCx8vPohtkV53A`).

## Running locally

Open `index.html` directly in a browser, or use any static file server:

```
npx serve .
# or
python3 -m http.server
```

## Architecture: single-page tab system

The site uses a **custom tab navigation** rather than traditional scroll-through sections. Key rules:

- Nav links have `data-page="<section>"` attributes — clicking them calls `window.vikaraShowPage(page)`
- Page sections are `<section class="page-section" data-page="<section>">` — hidden by default (`display: none`)
- Active section gets `.active` class; `body.page-active` hides the hero and hero-video sections
- The hero (`#hero`) and fullscreen video (`#hero-video`) are only visible on the "home" state

**Sections:** `problem`, `shift`, `proof`, `students`, `services`, `contact`, `team`

Stat counters (`[data-count]`) animate when a page becomes active via `window.animateCountersInPage(page)`.

## File structure

```
index.html          — entire site: CSS, HTML, JS
images/             — vikara-logo.svg, headshots, pamphlet scans, etc.
vikara video 2.mp4  — hero fullscreen background video
*.html              — playground/prototype files (not part of the live site)
```

The playground files (`*-playground.html`, `demo.html`, `vikara-preview.html`, etc.) are scratch files for experimenting with backgrounds and effects — not deployed.

## Design system

Defined entirely via CSS custom properties at the top of `index.html`:

- **Light theme** (`[data-theme="light"]`): warm cream `#EAE2D2` bg, deep brown text `#2A1F0E`, forest green accent `#2D6B5A`
- **Dark theme** (`[data-theme="dark"]`): deep forest `#0E1C14` bg, light text `#E8F2EC`, teal accent `#4AAE8E`
- **Fonts:** Bebas Neue (display/headlines), Crimson Pro (body/serif), DM Sans (UI text)
- Theme persisted to `localStorage` as `vikara-theme`

## Canvas effects

Two animated canvas backgrounds run on every page:

1. **`#orbital-bg`** (fixed, z-index -1) — seeded orbital ring system, always running
2. **`#particles`** (inside `#hero`) — floating dot particles, only visible on hero

Both read `data-theme` to switch between teal/copper color palettes.

## Brand constraints (from `.impeccable.md`)

- **Bold, alive, purposeful** — not corporate ed-tech, not SaaS dashboard aesthetic
- Warm earthy palette; no purple-to-blue gradients, no glassmorphism everywhere
- Bebas Neue for all display text, Crimson Pro for body/serif moments
- **The student is the hero** — imagery and framing centers the learner, not the consultant
- Every element earns its place; no redundancy
