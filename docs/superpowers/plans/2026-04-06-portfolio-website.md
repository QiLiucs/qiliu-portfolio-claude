# Portfolio Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and deploy a beautiful, elegant single-page portfolio website for Qi Liu to GitHub Pages using pure HTML, CSS, and vanilla JS.

**Architecture:** Single `index.html` with a linked `style.css` and `script.js`. No build step, no dependencies. Deployed directly from the `main` branch root of `github.com/QiLiucs/QiLiucs.github.io`.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox, IntersectionObserver), vanilla JS, Google Fonts (EB Garamond, Jost, DM Sans), GitHub Pages.

---

## File Map

| File | Responsibility |
|---|---|
| `index.html` | All markup — nav, 6 sections, footer |
| `style.css` | All styles — CSS variables, reset, layout, components, animations |
| `script.js` | Nav active state, scroll-reveal, stat counter animation |
| `assets/images/photo-1.jpg` | Amazon achievement photo (placeholder until provided) |
| `assets/images/photo-2.jpg` | Amazon achievement photo (placeholder until provided) |
| `assets/images/photo-3.jpg` | Amazon achievement photo (placeholder until provided) |
| `.gitignore` | Excludes `.superpowers/`, `.DS_Store` |

---

## Task 1: Scaffold — repo, files, and base HTML shell

**Files:**
- Create: `index.html`
- Create: `style.css`
- Create: `script.js`
- Create: `.gitignore`
- Create: `assets/images/` (directory)

- [ ] **Step 1: Create the directory structure**

```bash
cd /Users/june/Documents/workspace/portfolio
mkdir -p assets/images
touch index.html style.css script.js .gitignore
```

- [ ] **Step 2: Write `.gitignore`**

```
.superpowers/
.DS_Store
```

- [ ] **Step 3: Write the base `index.html` shell**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Qi Liu — Software Engineer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=EB+Garamond:ital,wght@0,400;0,500;0,600;1,400;1,500;1,600&family=Jost:wght@200;300;400;500&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;1,9..40,300;1,9..40,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <nav id="nav">
    <!-- Task 2 -->
  </nav>

  <main>
    <section id="hero"><!-- Task 3 --></section>
    <section id="stack"><!-- Task 4 --></section>
    <section id="experience"><!-- Task 5 --></section>
    <section id="projects"><!-- Task 6 --></section>
    <section id="education"><!-- Task 7 --></section>
  </main>

  <footer id="footer"><!-- Task 7 --></footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 4: Initialize git and create the GitHub repo**

```bash
cd /Users/june/Documents/workspace/portfolio
git init
git add index.html style.css script.js .gitignore
git commit -m "chore: initial scaffold"
gh repo create QiLiucs/QiLiucs.github.io --public --source=. --remote=origin --push
```

Expected: repo created at `https://github.com/QiLiucs/QiLiucs.github.io`

---

## Task 2: CSS foundations — variables, reset, typography, body

**Files:**
- Modify: `style.css`

- [ ] **Step 1: Write CSS reset, variables, and base body styles into `style.css`**

```css
/* ── VARIABLES ── */
:root {
  --ink:       #1a2520;
  --sage:      #3d5a4e;
  --sage-mid:  #7a9e8e;
  --sage-lt:   #eaf0ee;
  --warm:      #f8f8f6;
  --parchment: #f4f2ee;
  --rule:      #e4e4e0;
  --muted:     #7a7a72;
  --gold:      #c8a878;

  --font-display: 'EB Garamond', Georgia, serif;
  --font-ui:      'Jost', system-ui, sans-serif;
  --font-body:    'DM Sans', system-ui, sans-serif;
}

/* ── RESET ── */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
  font-size: 16px;
}

body {
  background: var(--warm);
  color: var(--ink);
  font-family: var(--font-ui);
  font-weight: 300;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

img {
  display: block;
  max-width: 100%;
}

a {
  color: inherit;
  text-decoration: none;
}

/* ── SCROLLBAR ── */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--sage-mid); border-radius: 2px; }

/* ── SHARED SECTION LAYOUT ── */
.section-inner {
  padding: 100px 60px;
}

.section-header {
  display: flex;
  align-items: baseline;
  gap: 20px;
  margin-bottom: 64px;
}

.section-num {
  font-family: var(--font-display);
  font-size: 13px;
  font-style: italic;
  color: var(--sage-mid);
  flex-shrink: 0;
}

.section-title {
  font-family: var(--font-display);
  font-size: 42px;
  font-weight: 400;
  color: var(--ink);
  letter-spacing: -0.5px;
  line-height: 1;
}

.section-title em {
  font-style: italic;
  color: var(--sage);
}

.section-rule {
  flex: 1;
  height: 1px;
  background: var(--rule);
  align-self: center;
}

/* ── CHIP ── */
.chip {
  display: inline-block;
  font-size: 9px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--sage);
  background: var(--sage-lt);
  padding: 5px 12px;
  border-radius: 1px;
}

/* ── SCROLL REVEAL ── */
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.reveal.visible {
  opacity: 1;
  transform: none;
}
.reveal-delay-1 { transition-delay: 0.1s; }
.reveal-delay-2 { transition-delay: 0.2s; }
.reveal-delay-3 { transition-delay: 0.3s; }
.reveal-delay-4 { transition-delay: 0.4s; }
```

- [ ] **Step 2: Open `index.html` in a browser and verify the page background is `#f8f8f6` (warm off-white) with no visible content yet**

```bash
open /Users/june/Documents/workspace/portfolio/index.html
```

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "feat: css variables, reset, shared layout utilities"
```

---

## Task 3: Nav

**Files:**
- Modify: `index.html` (nav section)
- Modify: `style.css` (nav styles)

- [ ] **Step 1: Write nav HTML inside `<nav id="nav">`**

```html
<nav id="nav">
  <div class="nav-name">Qi Liu</div>
  <ul class="nav-links">
    <li><a href="#stack">Stack</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#education">Education</a></li>
  </ul>
</nav>
```

- [ ] **Step 2: Write nav CSS, appended to `style.css`**

```css
/* ── NAV ── */
#nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 60px;
  background: rgba(248, 248, 246, 0.92);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--rule);
}

.nav-name {
  font-family: var(--font-display);
  font-size: 17px;
  font-weight: 400;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--ink);
}

.nav-links {
  display: flex;
  gap: 36px;
  list-style: none;
}

.nav-links a {
  font-size: 10px;
  letter-spacing: 2.5px;
  text-transform: uppercase;
  color: var(--muted);
  transition: color 0.2s;
  padding-bottom: 2px;
  border-bottom: 1px solid transparent;
  transition: color 0.2s, border-color 0.2s;
}

.nav-links a:hover,
.nav-links a.active {
  color: var(--sage);
  border-bottom-color: var(--sage-mid);
}
```

- [ ] **Step 3: Verify in browser — fixed nav at top, "Qi Liu" on left, four links on right, warm off-white with blur**

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: fixed nav with blur backdrop"
```

---

## Task 4: Hero section

**Files:**
- Modify: `index.html` (hero section)
- Modify: `style.css` (hero styles)

- [ ] **Step 1: Write hero HTML inside `<section id="hero">`**

```html
<section id="hero">
  <div class="hero-left">
    <div class="hero-left-top">
      <div class="hero-eyebrow">Software Engineer · Bellevue, WA</div>
      <h1 class="hero-headline">Building<br>systems<br>at <em>scale.</em></h1>
      <div class="hero-sub">Amazon · AWS · GenAI</div>
      <p class="hero-desc">5+ years shipping scalable, high-impact systems — from global Prime migrations reaching hundreds of millions of users, to AI-powered automation that redefines how teams build.</p>
      <a class="hero-cta" href="#experience">View Experience →</a>
    </div>
    <div class="hero-stats">
      <div class="hero-stat">
        <div class="hero-stat-n" data-target="5">0</div>
        <div class="hero-stat-l">Years Experience</div>
      </div>
      <div class="hero-stat">
        <div class="hero-stat-n" data-target="100" data-suffix="M+">0</div>
        <div class="hero-stat-l">Users Reached</div>
      </div>
      <div class="hero-stat">
        <div class="hero-stat-n" data-prefix="$" data-target="1" data-suffix="M+">0</div>
        <div class="hero-stat-l">Annual Revenue</div>
      </div>
      <div class="hero-stat">
        <div class="hero-stat-n" data-target="22">0</div>
        <div class="hero-stat-l">Marketplaces</div>
      </div>
    </div>
  </div>

  <div class="hero-right">
    <div class="hero-r-block">
      <div class="hero-r-label">About</div>
      <blockquote class="hero-summary">"Software Engineer with a proven track record in full-stack development, cloud architecture, AI-powered automation, and global platform migrations."</blockquote>
    </div>
    <div class="hero-r-block">
      <div class="hero-r-label">Core Skills</div>
      <div class="hero-chips">
        <span class="chip">Java</span>
        <span class="chip">Python</span>
        <span class="chip">Go</span>
        <span class="chip">React</span>
        <span class="chip">AWS</span>
        <span class="chip">LangGraph</span>
        <span class="chip">Docker</span>
        <span class="chip">FastAPI</span>
      </div>
    </div>
    <div class="hero-r-block">
      <div class="hero-r-label">Contact</div>
      <div class="hero-contacts">
        <a class="hero-contact-item" href="mailto:eillenliu667@gmail.com">
          <span class="contact-dot"></span>eillenliu667@gmail.com
        </a>
        <a class="hero-contact-item" href="tel:+12132040589">
          <span class="contact-dot"></span>+1 (213) 204-0589
        </a>
        <a class="hero-contact-item" href="https://github.com/QiLiucs" target="_blank" rel="noopener">
          <span class="contact-dot"></span>github.com/QiLiucs
        </a>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Write hero CSS, appended to `style.css`**

```css
/* ── HERO ── */
#hero {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding-top: 64px; /* nav height */
}

.hero-left {
  padding: 72px 60px 72px 60px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border-right: 1px solid var(--rule);
}

.hero-left-top { }

.hero-eyebrow {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 9px;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--sage-mid);
  margin-bottom: 20px;
}

.hero-eyebrow::before {
  content: '';
  display: block;
  width: 28px;
  height: 1px;
  background: var(--sage-mid);
  flex-shrink: 0;
}

.hero-headline {
  font-family: var(--font-display);
  font-size: 72px;
  font-weight: 400;
  line-height: 1.0;
  letter-spacing: -1px;
  color: var(--ink);
}

.hero-headline em {
  font-style: italic;
  color: var(--sage);
}

.hero-sub {
  font-size: 10px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--sage-mid);
  margin-top: 20px;
}

.hero-desc {
  font-family: var(--font-body);
  font-size: 14px;
  font-style: italic;
  line-height: 1.75;
  color: var(--muted);
  max-width: 380px;
  margin-top: 28px;
}

.hero-cta {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  margin-top: 36px;
  font-size: 10px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--sage);
  border-bottom: 1px solid var(--sage-mid);
  padding-bottom: 3px;
  align-self: flex-start;
  transition: color 0.2s, border-color 0.2s;
}

.hero-cta:hover {
  color: var(--ink);
  border-color: var(--ink);
}

.hero-stats {
  display: flex;
  gap: 36px;
  padding-top: 48px;
  border-top: 1px solid var(--rule);
}

.hero-stat-n {
  font-family: var(--font-display);
  font-size: 36px;
  font-weight: 400;
  color: var(--ink);
  line-height: 1;
}

.hero-stat-l {
  font-size: 9px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--muted);
  margin-top: 6px;
}

.hero-right {
  padding: 72px 60px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 44px;
  background: var(--parchment);
}

.hero-r-label {
  font-size: 8px;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--sage-mid);
  margin-bottom: 14px;
}

.hero-summary {
  font-family: var(--font-display);
  font-size: 20px;
  font-weight: 400;
  line-height: 1.6;
  color: var(--ink);
  font-style: italic;
  border-left: 2px solid var(--sage-mid);
  padding-left: 20px;
}

.hero-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.hero-contacts {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.hero-contact-item {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 12px;
  color: var(--muted);
  transition: color 0.2s;
}

.hero-contact-item:hover { color: var(--sage); }

.contact-dot {
  display: block;
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: var(--sage-mid);
  flex-shrink: 0;
}
```

- [ ] **Step 3: Verify in browser — two-column hero, large Garamond headline, stats row at bottom, parchment right panel with quote, chips, and contacts. Stat numbers show 0 (animation comes in Task 8).**

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: hero section — headline, stats, about panel"
```

---

## Task 5: Tech Stack section

**Files:**
- Modify: `index.html` (stack section)
- Modify: `style.css` (stack styles)

- [ ] **Step 1: Write stack HTML inside `<section id="stack">`**

```html
<section id="stack">
  <div class="section-inner">
    <div class="section-header reveal">
      <span class="section-num">01</span>
      <h2 class="section-title">Tech <em>Stack</em></h2>
      <div class="section-rule"></div>
    </div>
    <div class="stack-grid">
      <div class="stack-cell reveal reveal-delay-1">
        <div class="stack-cell-label">Backend</div>
        <div class="stack-items">Java, Python, Go, Spring, FastAPI</div>
      </div>
      <div class="stack-cell reveal reveal-delay-2">
        <div class="stack-cell-label">Frontend</div>
        <div class="stack-items">React, JavaScript, HTML, CSS</div>
      </div>
      <div class="stack-cell reveal reveal-delay-3">
        <div class="stack-cell-label">Cloud & DevOps</div>
        <div class="stack-items">AWS, DynamoDB, Lambda, API Gateway, ECS, SQS, Docker, CI/CD</div>
      </div>
      <div class="stack-cell reveal reveal-delay-4">
        <div class="stack-cell-label">GenAI</div>
        <div class="stack-items">LangChain, LangGraph, MCP, Skills, AI Agents, Multi-modal</div>
      </div>
      <div class="stack-cell reveal reveal-delay-1">
        <div class="stack-cell-label">Data</div>
        <div class="stack-items">DynamoDB, PostgreSQL, MySQL, MongoDB, Cassandra, Redis</div>
      </div>
      <div class="stack-cell reveal reveal-delay-2">
        <div class="stack-cell-label">Infrastructure</div>
        <div class="stack-items">Kafka, WebSocket, GraphQL, REST API, Zookeeper</div>
      </div>
      <div class="stack-cell reveal reveal-delay-3">
        <div class="stack-cell-label">Observability</div>
        <div class="stack-items">OpenTelemetry, Grafana, InfluxDB</div>
      </div>
      <div class="stack-cell reveal reveal-delay-4">
        <div class="stack-cell-label">Other</div>
        <div class="stack-items">Microservices, Distributed Systems, Raft, Selenium</div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Write stack CSS, appended to `style.css`**

```css
/* ── STACK ── */
#stack {
  background: var(--parchment);
}

.stack-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1px;
  background: var(--rule);
  border: 1px solid var(--rule);
}

.stack-cell {
  background: var(--parchment);
  padding: 28px 24px;
  transition: background 0.25s;
}

.stack-cell:hover {
  background: var(--sage-lt);
}

.stack-cell-label {
  font-size: 8px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--sage-mid);
  margin-bottom: 14px;
}

.stack-items {
  font-family: var(--font-display);
  font-size: 15px;
  line-height: 1.6;
  color: var(--ink);
}
```

- [ ] **Step 3: Verify in browser — 4×2 grid of cells with hairline borders, category labels in small caps sage, Garamond text for items, hover shows sage-lt background**

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: tech stack section with 8-cell grid"
```

---

## Task 6: Experience section

**Files:**
- Modify: `index.html` (experience section)
- Modify: `style.css` (experience styles)

- [ ] **Step 1: Write experience HTML inside `<section id="experience">`**

```html
<section id="experience">
  <div class="section-inner">
    <div class="section-header reveal">
      <span class="section-num">02</span>
      <h2 class="section-title"><em>Experience</em></h2>
      <div class="section-rule"></div>
    </div>

    <!-- Amazon -->
    <div class="exp-entry reveal">
      <div class="exp-meta">
        <div class="exp-company">Amazon</div>
        <div class="exp-period">Jan 2024 — Present</div>
        <div class="exp-role">Software Engineer II</div>
        <div class="exp-tags">
          <span class="chip">Java</span>
          <span class="chip">React</span>
          <span class="chip">Spring</span>
          <span class="chip">Docker</span>
          <span class="chip">Full-Stack</span>
        </div>
      </div>
      <div class="exp-content">
        <ul class="exp-bullets">
          <li>Led migration of Amazon Prime signup CX to a new scalable architecture across 22 marketplaces, reducing acquisition flow friction by 15% — impacting hundreds of millions of users and driving $M+ revenue growth.</li>
          <li>Spearheaded cross-platform expansion of Prime signup to Fire Tablets, Kindle, and Alexa, increasing acquisition touchpoints by thousands per month and generating $1.1M+ annual revenue from previously untapped segments.</li>
          <li>Designed native rendering solutions on Kindle using KPP (Kindle React Native) frameworks, eliminating browser dependency. Proposed unified OOBE upsell architecture across Fire Tablet, Alexa, and Kindle.</li>
        </ul>
        <div class="exp-photos">
          <div class="photo-slot">
            <img src="assets/images/photo-1.jpg" alt="Amazon achievement" class="exp-photo" onerror="this.parentElement.classList.add('photo-placeholder')">
          </div>
          <div class="photo-slot">
            <img src="assets/images/photo-2.jpg" alt="Amazon achievement" class="exp-photo" onerror="this.parentElement.classList.add('photo-placeholder')">
          </div>
          <div class="photo-slot">
            <img src="assets/images/photo-3.jpg" alt="Amazon achievement" class="exp-photo" onerror="this.parentElement.classList.add('photo-placeholder')">
          </div>
        </div>
      </div>
    </div>

    <!-- AWS -->
    <div class="exp-entry reveal">
      <div class="exp-meta">
        <div class="exp-company">AWS</div>
        <div class="exp-period">Feb 2021 — Dec 2023</div>
        <div class="exp-role">Software Engineer I / II</div>
        <div class="exp-tags">
          <span class="chip">AWS</span>
          <span class="chip">Docker</span>
          <span class="chip">Full-Stack</span>
          <span class="chip">WebSocket</span>
        </div>
      </div>
      <div class="exp-content">
        <ul class="exp-bullets">
          <li>Containerized a parallel testing system using ECS, reducing runtime of 200+ test cases from 3+ hours to ~20 minutes.</li>
          <li>Designed and delivered core components of a network device reservation system — built REST APIs and a no-code CLI auto-generated from API definitions, reducing developer update time by 60%.</li>
          <li>Drove architectural improvements by migrating from polling-based status checks to an event-driven WebSocket architecture.</li>
          <li>Improved latency for team's web services by 85% through algorithm optimization, lazy loading, and SQL tuning.</li>
        </ul>
      </div>
    </div>

  </div>
</section>
```

- [ ] **Step 2: Write experience CSS, appended to `style.css`**

```css
/* ── EXPERIENCE ── */
#experience {
  background: var(--warm);
}

.exp-entry {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 60px;
  padding: 64px 0;
  border-top: 1px solid var(--rule);
}

.exp-entry:last-child {
  border-bottom: 1px solid var(--rule);
}

.exp-company {
  font-family: var(--font-display);
  font-size: 32px;
  font-weight: 400;
  color: var(--ink);
  letter-spacing: -0.5px;
}

.exp-period {
  font-size: 9px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--sage-mid);
  margin-top: 8px;
}

.exp-role {
  font-family: var(--font-body);
  font-size: 12px;
  font-style: italic;
  color: var(--muted);
  margin-top: 4px;
  margin-bottom: 16px;
}

.exp-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.exp-bullets {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.exp-bullets li {
  font-family: var(--font-body);
  font-size: 13px;
  line-height: 1.7;
  color: #4a4a42;
  padding-left: 16px;
  position: relative;
}

.exp-bullets li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 9px;
  width: 6px;
  height: 1px;
  background: var(--sage-mid);
}

.exp-photos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  margin-top: 32px;
}

.photo-slot {
  aspect-ratio: 4 / 3;
  overflow: hidden;
  background: var(--sage-lt);
  border: 1px dashed var(--sage-mid);
  position: relative;
}

/* Show placeholder icon when image fails to load */
.photo-slot.photo-placeholder::after {
  content: '+ Photo';
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 9px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--sage-mid);
}

.exp-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.4s ease;
}

.photo-slot:hover .exp-photo {
  transform: scale(1.04);
}
```

- [ ] **Step 3: Verify in browser — two experience entries with left meta / right content layout, photo slots show dashed placeholder (images not yet present), bullet points with sage dash markers**

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: experience section — Amazon and AWS entries with photo slots"
```

---

## Task 7: GenAI Projects section

**Files:**
- Modify: `index.html` (projects section)
- Modify: `style.css` (project styles)

- [ ] **Step 1: Write projects HTML inside `<section id="projects">`**

```html
<section id="projects">
  <div class="section-inner">
    <div class="section-header reveal">
      <span class="section-num">03</span>
      <h2 class="section-title">GenAI <em>Projects</em></h2>
      <div class="section-rule"></div>
    </div>
    <div class="projects-grid">

      <div class="project-card reveal reveal-delay-1">
        <div class="project-video-wrap">
          <iframe
            src="https://drive.google.com/file/d/1ldP9q42vLpwrqhEgfrTW4VuU17ly7ace/preview"
            allow="autoplay"
            frameborder="0"
            allowfullscreen
            title="AI Browser Agent demo video"
          ></iframe>
        </div>
        <div class="project-body">
          <div class="project-tag">AI Agent · 2024</div>
          <h3 class="project-name">AI Browser Agent</h3>
          <p class="project-tagline">An AI agent that controls your browser automatically — streaming multi-step task execution with persistent context.</p>
          <ul class="project-bullets">
            <li>FastAPI service streaming multi-step task execution with persistent session context</li>
            <li>Optimized token usage by dropping non-interactive elements and trimming old browser snapshots from memory</li>
            <li>Production-grade observability: OpenTelemetry tracing, InfluxDB metrics, Grafana dashboards including token cost and latency</li>
            <li>LangGraph-backed checkpointing on Postgres for resumable conversations and structured chat-history retrieval</li>
          </ul>
          <div class="project-chips">
            <span class="chip">FastAPI</span>
            <span class="chip">LangGraph</span>
            <span class="chip">OpenTelemetry</span>
            <span class="chip">Python</span>
            <span class="chip">PostgreSQL</span>
          </div>
        </div>
      </div>

      <div class="project-card reveal reveal-delay-2">
        <div class="project-video-wrap project-video-placeholder">
          <div class="video-coming-soon">
            <div class="play-ring"><div class="play-arrow"></div></div>
            <span>Video coming soon</span>
          </div>
        </div>
        <div class="project-body">
          <div class="project-tag">Knowledge Pipeline · 2024</div>
          <h3 class="project-name">Distill</h3>
          <p class="project-tagline">Distilling AI trends from X, GitHub, YouTube, and RSS into your knowledge base — while you scroll.</p>
          <ul class="project-bullets">
            <li>Free audio pipeline converting YouTube videos into short, digestible podcast-style audio using a locally deployed TTS model</li>
            <li>End-to-end AI knowledge pipeline ingesting from X, YouTube, GitHub, RSS, and websites with one-click sharing to X, RedNote, or Obsidian</li>
            <li>Condenses transcripts into podcast-style scripts with an LLM and synthesizes speech entirely on-device</li>
          </ul>
          <div class="project-chips">
            <span class="chip">LangChain</span>
            <span class="chip">TTS</span>
            <span class="chip">Python</span>
            <span class="chip">RSS</span>
            <span class="chip">Obsidian</span>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
```

> **Note:** The Distill card uses a placeholder until the user provides the direct Google Drive file ID. To replace it: change `project-video-placeholder` div to an `<iframe src="https://drive.google.com/file/d/FILE_ID_HERE/preview" ...>` matching the AI Browser Agent pattern.

- [ ] **Step 2: Write project CSS, appended to `style.css`**

```css
/* ── PROJECTS ── */
#projects {
  background: var(--parchment);
}

.projects-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 36px;
}

.project-card {
  background: var(--warm);
  border: 1px solid var(--rule);
  overflow: hidden;
  transition: box-shadow 0.35s ease, transform 0.35s ease;
}

.project-card:hover {
  box-shadow: 0 16px 48px rgba(61, 90, 78, 0.1);
  transform: translateY(-4px);
}

.project-video-wrap {
  aspect-ratio: 16 / 9;
  width: 100%;
  overflow: hidden;
  background: var(--ink);
  position: relative;
}

.project-video-wrap iframe {
  width: 100%;
  height: 100%;
  border: none;
  display: block;
}

.project-video-placeholder {
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #1a2520 0%, #2a3f35 100%);
}

.video-coming-soon {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  color: rgba(200, 168, 120, 0.6);
  font-size: 9px;
  letter-spacing: 3px;
  text-transform: uppercase;
}

.play-ring {
  width: 48px;
  height: 48px;
  border: 1.5px solid rgba(200, 168, 120, 0.5);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.play-arrow {
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 8px 0 8px 14px;
  border-color: transparent transparent transparent rgba(200, 168, 120, 0.7);
  margin-left: 4px;
}

.project-body {
  padding: 28px 28px 32px;
}

.project-tag {
  font-size: 8px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--sage-mid);
  margin-bottom: 8px;
}

.project-name {
  font-family: var(--font-display);
  font-size: 26px;
  font-weight: 400;
  color: var(--ink);
  margin-bottom: 8px;
  letter-spacing: -0.3px;
}

.project-tagline {
  font-family: var(--font-body);
  font-size: 13px;
  font-style: italic;
  color: var(--muted);
  line-height: 1.6;
  margin-bottom: 20px;
}

.project-bullets {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.project-bullets li {
  font-family: var(--font-body);
  font-size: 12px;
  line-height: 1.6;
  color: #5a5a52;
  padding-left: 14px;
  position: relative;
}

.project-bullets li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 8px;
  width: 5px;
  height: 1px;
  background: var(--sage-mid);
}

.project-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 20px;
  padding-top: 20px;
  border-top: 1px solid var(--rule);
}
```

- [ ] **Step 3: Verify in browser — two project cards side by side, AI Browser Agent shows Google Drive video iframe, Distill shows dark placeholder. Cards lift on hover.**

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: genai projects section with video embeds"
```

---

## Task 8: Education section + Footer

**Files:**
- Modify: `index.html` (education section and footer)
- Modify: `style.css` (education and footer styles)

- [ ] **Step 1: Write education HTML inside `<section id="education">`**

```html
<section id="education">
  <div class="section-inner">
    <div class="section-header reveal">
      <span class="section-num">04</span>
      <h2 class="section-title"><em>Education</em></h2>
      <div class="section-rule"></div>
    </div>
    <div class="edu-grid">
      <div class="edu-cell reveal reveal-delay-1">
        <div class="edu-degree">M.S. Computer Science</div>
        <div class="edu-school">University of Southern California, Los Angeles CA</div>
        <div class="edu-period">May 2018 — Dec 2020</div>
      </div>
      <div class="edu-cell reveal reveal-delay-2">
        <div class="edu-degree">B.S. Biomedical Engineering</div>
        <div class="edu-school">Southern Medical University, Guangzhou, China</div>
        <div class="edu-period">Sep 2013 — Dec 2017</div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Write footer HTML inside `<footer id="footer">`**

```html
<footer id="footer">
  <div class="footer-name">Qi Liu</div>
  <div class="footer-links">
    <a href="mailto:eillenliu667@gmail.com">Email</a>
    <a href="https://github.com/QiLiucs" target="_blank" rel="noopener">GitHub</a>
    <a href="tel:+12132040589">+1 213 204 0589</a>
  </div>
  <div class="footer-copy">© 2025 Qi Liu</div>
</footer>
```

- [ ] **Step 3: Write education + footer CSS, appended to `style.css`**

```css
/* ── EDUCATION ── */
#education {
  background: var(--warm);
}

.edu-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1px;
  background: var(--rule);
  border: 1px solid var(--rule);
}

.edu-cell {
  background: var(--warm);
  padding: 40px 36px;
  transition: background 0.25s;
}

.edu-cell:hover {
  background: var(--sage-lt);
}

.edu-degree {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 500;
  color: var(--ink);
  margin-bottom: 8px;
}

.edu-school {
  font-family: var(--font-body);
  font-size: 13px;
  font-style: italic;
  color: var(--muted);
  margin-bottom: 8px;
}

.edu-period {
  font-size: 9px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--sage-mid);
}

/* ── FOOTER ── */
#footer {
  background: var(--ink);
  padding: 56px 60px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-name {
  font-family: var(--font-display);
  font-size: 20px;
  font-weight: 300;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.85);
}

.footer-links {
  display: flex;
  gap: 28px;
}

.footer-links a {
  font-size: 10px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.3);
  transition: color 0.2s;
}

.footer-links a:hover {
  color: rgba(200, 168, 120, 0.8);
}

.footer-copy {
  font-size: 10px;
  letter-spacing: 1px;
  color: rgba(255, 255, 255, 0.18);
}
```

- [ ] **Step 4: Verify full page in browser — scroll through all sections, check education grid and dark footer look correct**

- [ ] **Step 5: Commit**

```bash
git add index.html style.css
git commit -m "feat: education section and footer"
```

---

## Task 9: JavaScript — nav active state, scroll-reveal, stat counter

**Files:**
- Modify: `script.js`

- [ ] **Step 1: Write the complete `script.js`**

```js
/* ── NAV ACTIVE STATE ── */
const sections = document.querySelectorAll('main section[id], footer[id]');
const navLinks = document.querySelectorAll('.nav-links a');

const navObserver = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        navLinks.forEach((link) => {
          link.classList.toggle(
            'active',
            link.getAttribute('href') === '#' + entry.target.id
          );
        });
      }
    });
  },
  { rootMargin: '-40% 0px -55% 0px' }
);

sections.forEach((section) => navObserver.observe(section));

/* ── SCROLL REVEAL ── */
const revealEls = document.querySelectorAll('.reveal');

const revealObserver = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
        revealObserver.unobserve(entry.target);
      }
    });
  },
  { threshold: 0.12 }
);

revealEls.forEach((el) => revealObserver.observe(el));

/* ── STAT COUNTER ANIMATION ── */
function animateCounter(el) {
  const target = parseInt(el.dataset.target, 10);
  const prefix = el.dataset.prefix || '';
  const suffix = el.dataset.suffix || (target === 5 ? '+' : '');
  const duration = 1200;
  const start = performance.now();

  function tick(now) {
    const elapsed = now - start;
    const progress = Math.min(elapsed / duration, 1);
    // ease-out cubic
    const eased = 1 - Math.pow(1 - progress, 3);
    const current = Math.floor(eased * target);
    el.textContent = prefix + current + (progress < 1 ? '' : suffix);
    if (progress < 1) requestAnimationFrame(tick);
  }

  requestAnimationFrame(tick);
}

const statEls = document.querySelectorAll('.hero-stat-n[data-target]');
let statsAnimated = false;

const statsObserver = new IntersectionObserver(
  (entries) => {
    if (entries[0].isIntersecting && !statsAnimated) {
      statsAnimated = true;
      statEls.forEach((el) => animateCounter(el));
      statsObserver.disconnect();
    }
  },
  { threshold: 0.5 }
);

const statsSection = document.querySelector('.hero-stats');
if (statsSection) statsObserver.observe(statsSection);
```

- [ ] **Step 2: Verify in browser:**
  - Scroll down — sections fade + slide up as they enter viewport
  - On load, hero stats count up from 0 to their targets
  - As you scroll through sections, the corresponding nav link highlights in sage

- [ ] **Step 3: Commit**

```bash
git add script.js
git commit -m "feat: scroll-reveal, nav active state, stat counter animation"
```

---

## Task 10: Mobile responsiveness

**Files:**
- Modify: `style.css` (media query block at end)

- [ ] **Step 1: Append mobile media queries to the end of `style.css`**

```css
/* ── RESPONSIVE ── */
@media (max-width: 900px) {
  /* Nav */
  #nav {
    padding: 0 24px;
  }
  .nav-links {
    gap: 20px;
  }

  /* Hero */
  #hero {
    grid-template-columns: 1fr;
    min-height: auto;
  }
  .hero-left {
    padding: 72px 24px 48px;
    border-right: none;
    border-bottom: 1px solid var(--rule);
  }
  .hero-headline {
    font-size: 52px;
  }
  .hero-stats {
    gap: 20px;
    flex-wrap: wrap;
  }
  .hero-right {
    padding: 48px 24px;
  }

  /* Shared section padding */
  .section-inner {
    padding: 72px 24px;
  }
  .section-title {
    font-size: 32px;
  }

  /* Stack */
  .stack-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  /* Experience */
  .exp-entry {
    grid-template-columns: 1fr;
    gap: 28px;
    padding: 40px 0;
  }
  .exp-photos {
    grid-template-columns: repeat(2, 1fr);
  }

  /* Projects */
  .projects-grid {
    grid-template-columns: 1fr;
  }

  /* Education */
  .edu-grid {
    grid-template-columns: 1fr;
  }

  /* Footer */
  #footer {
    padding: 40px 24px;
    flex-direction: column;
    gap: 20px;
    text-align: center;
  }
  .footer-links {
    gap: 20px;
  }
}

@media (max-width: 480px) {
  .hero-headline {
    font-size: 40px;
  }
  .stack-grid {
    grid-template-columns: 1fr;
  }
  .exp-photos {
    grid-template-columns: 1fr;
  }
}
```

- [ ] **Step 2: Open browser DevTools, switch to mobile viewport (375px), scroll through entire page. Verify: single column layout, readable type, no horizontal overflow.**

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "feat: mobile responsive layout"
```

---

## Task 11: Deploy to GitHub Pages

**Files:** None (repo configuration only)

- [ ] **Step 1: Push all commits to remote**

```bash
git push origin main
```

- [ ] **Step 2: Enable GitHub Pages via CLI**

```bash
gh api repos/QiLiucs/QiLiucs.github.io/pages \
  --method POST \
  --field source='{"branch":"main","path":"/"}' \
  --silent || echo "Pages may already be enabled"
```

- [ ] **Step 3: Wait ~60 seconds, then verify the live site**

```bash
sleep 60
open https://QiLiucs.github.io
```

Expected: the full portfolio loads at `https://QiLiucs.github.io` with all sections, fonts, and animations.

- [ ] **Step 4: Final check — verify each section visually on the live URL**

  - [ ] Nav is fixed, blur works
  - [ ] Hero headline, stats animate on load
  - [ ] Stack grid 8 cells
  - [ ] Experience — Amazon entry with 3 placeholder photo slots, AWS entry
  - [ ] Projects — AI Browser Agent video plays via Google Drive iframe; Distill shows placeholder
  - [ ] Education grid
  - [ ] Footer dark bar
  - [ ] Mobile viewport looks correct

- [ ] **Step 5: Commit a deploy tag**

```bash
git tag v1.0.0
git push origin v1.0.0
```

---

## Self-Review

**Spec coverage check:**
- [x] Porcelain & Ink visual identity (CSS variables, EB Garamond, Jost, DM Sans) — Task 2
- [x] Fixed nav with blur, active state — Tasks 3, 9
- [x] Hero two-column split, stats row — Task 4
- [x] Tech stack 8-cell grid with all categories from spec — Task 5
- [x] Experience: Amazon (3 bullets + 3 photo slots) + AWS (4 bullets) — Task 6
- [x] GenAI Projects: AI Browser Agent (Drive iframe) + Distill (placeholder) — Task 7
- [x] Education 2-cell grid — Task 8
- [x] Footer — Task 8
- [x] Scroll-reveal + stat counter + nav active state — Task 9
- [x] Mobile responsive — Task 10
- [x] GitHub Pages deploy — Task 11
- [x] `.gitignore` excludes `.superpowers/` — Task 1

**Placeholder scan:** No TBDs. Distill video placeholder is intentional and documented with exact replacement instructions in Task 7.

**Type consistency:** CSS class names used consistently — `.exp-entry`, `.project-card`, `.stack-cell`, `.hero-stat-n`, `.reveal` — all defined in the task they're introduced and referenced identically in later tasks.
