# Portfolio Website — Design Spec
**Date:** 2026-04-06
**Owner:** Qi Liu (QiLiucs)

---

## Overview

A personal portfolio website for Qi Liu, a Software Engineer II at Amazon with 5+ years of experience at Amazon and AWS. Hosted as a static site on GitHub Pages under the repository `QiLiucs/QiLiucs.github.io` (or equivalent repo name). Zero dependencies — pure HTML, CSS, and vanilla JS only.

**Audience:** Primarily male technical recruiters and hiring managers.
**Tone:** Beautiful, elegant, graceful. Feminine confidence without being girly. Exquisite design details. Think Hermès, not Hello Kitty.

---

## Visual Identity — Porcelain & Ink

| Token | Value | Usage |
|---|---|---|
| `--ink` | `#1a2520` | Body text, headings, footer bg |
| `--sage` | `#3d5a4e` | Primary accent, links, italic headlines |
| `--sage-mid` | `#7a9e8e` | Secondary accent, eyebrows, rules |
| `--sage-lt` | `#eaf0ee` | Chip backgrounds, hover states |
| `--warm` | `#f8f8f6` | Main page background |
| `--parchment` | `#f4f2ee` | Alternate section background |
| `--rule` | `#e4e4e0` | Hairline borders, dividers |
| `--muted` | `#7a7a72` | Body copy, secondary text |

**Typography:**
- Display/headings: `EB Garamond` (400, 500, italic) — elegant, literary
- UI labels/nav: `Jost` (200, 300, 400) — clean, modern
- Body copy/descriptions: `DM Sans` (300, italic) — refined, readable
- All loaded from Google Fonts

**Design principles:**
- Generous white space
- Hairline borders (1px `var(--rule)`)
- Numbered sections (`01`, `02`, etc.) in small italic Garamond
- Section titles always have one italic word in sage green
- Sage-green accent bar (3px gradient) as a recurring motif

---

## Architecture

Single-page static site. Three files:

```
portfolio/
├── index.html       # All markup, Google Fonts link
├── style.css        # All styles (CSS variables, layout, components)
├── script.js        # Smooth scroll, nav active state, scroll animations
└── assets/
    └── images/      # Amazon photos (photo-1.jpg, photo-2.jpg, photo-3.jpg)
```

Deployed to GitHub Pages from the `main` branch root. Repository: `github.com/QiLiucs/QiLiucs.github.io`.

---

## Page Structure (single long scroll)

Fixed top nav with smooth anchor links. Sections flow top to bottom:

### Nav
- Fixed, `backdrop-filter: blur(12px)`, height 64px
- Left: `Qi Liu` in small-caps Garamond
- Right: `Stack · Experience · Projects · Education`
- Active link highlights in sage on scroll (IntersectionObserver)

### 1. Hero
Two-column split (50/50), full viewport height:
- **Left** (white bg): Large EB Garamond headline `"Building systems at scale."` (italic "scale." in sage), eyebrow label, short description paragraph, CTA link, bottom stat row (5+ years · 100M+ users · $1M+ revenue · 22 marketplaces)
- **Right** (parchment bg): About quote (blockquote with left sage border), core skills chips, contact info (email, phone, GitHub)

### 2. Tech Stack (`#stack`, parchment bg)
8-cell grid (4 columns × 2 rows), hairline borders between cells. Categories:
- Backend: Java, Python, Go, Spring, FastAPI
- Frontend: React, JavaScript, HTML, CSS
- Cloud & DevOps: AWS, DynamoDB, Lambda, API Gateway, ECS, SQS, Docker, CI/CD
- GenAI: LangChain, LangGraph, MCP, Skill, AI Agents, multi-modal
- Data: DynamoDB, PostgreSQL, MySQL, MongoDB, Cassandra, Redis
- Infrastructure: Kafka, WebSocket, GraphQL, REST API, Zookeeper
- Observability: OpenTelemetry, Grafana, InfluxDB
- Other: Microservices, Distributed Systems, Raft, Selenium

### 3. Experience (`#experience`, white bg)
Two entries, each in a 2-column grid (meta left, content right):

**Amazon** (Jan 2024 – Present) — Software Engineer II
- Tags: Java, React, Spring, docker, full-stack
- 3 bullet points from resume
- 3 photo slots in a 3-column grid below bullets
  - On deploy: placeholders with dashed sage border + "⊕ Photo N" label
  - When photos are added: `<img>` tags replace placeholders, `object-fit: cover`

**AWS** (Feb 2021 – Dec 2023) — Software Engineer I/II
- Tags: AWS cloud services, Docker, full-stack, WebSocket
- 4 bullet points from resume
- No photos

### 4. GenAI Projects (`#projects`, parchment bg)
Two cards side by side:

**AI Browser Agent**
- Video: Google Drive embed `https://drive.google.com/file/d/1ldP9q42vLpwrqhEgfrTW4VuU17ly7ace/preview` in a 16:9 iframe
- 4 bullet points, tech chips: FastAPI, LangGraph, OpenTelemetry, Python, PostgreSQL

**Distill**
- Video: Google Drive embed (link: `https://drive.google.com/drive/search?dmr=1&ec=wgc-drive-[module]-goto&q=distill` — user to provide direct file ID before deploy; placeholder used until then)
- 3 bullet points, tech chips: LangChain, TTS, Python, RSS, Obsidian

Video embed implementation: `<iframe>` with `allow="autoplay"`, `frameborder="0"`, wrapped in a 16:9 aspect-ratio container.

### 5. Education (`#education`, white bg)
2-cell grid:
- M.S. Computer Science — University of Southern California (May 2018 – Dec 2020)
- B.S. Biomedical Engineering — Southern Medical University (Sep 2013 – Dec 2017)

### 6. Footer
Dark ink background. Three columns: name (Garamond), nav links (Email · GitHub · Phone), copyright.

---

## Interactions (script.js)

1. **Smooth scroll** — `scroll-behavior: smooth` on `html`, JS fallback for Safari
2. **Nav active state** — IntersectionObserver watches each section, adds `.active` class to matching nav link
3. **Scroll-reveal animations** — sections fade + slide up on first entry (CSS `@keyframes` + IntersectionObserver adds `.visible` class). Staggered delays for stat numbers and grid cells.
4. **Stat counter animation** — hero stats count up from 0 on first viewport entry

---

## GitHub Pages Deployment

- Repository name: `QiLiucs.github.io`
- Branch: `main`, root directory
- URL will be: `https://QiLiucs.github.io`
- `.gitignore` excludes `.superpowers/`
- No build step required — files served directly

---

## Out of Scope

- Contact form (no backend)
- Dark mode toggle
- Blog / writing section
- Mobile-first responsive (desktop-first, basic mobile support via media queries)
