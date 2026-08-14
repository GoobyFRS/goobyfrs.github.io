---
layout: minimal
title: HTML5 and CSS3 Code Quality
nav_enabled: true
parent: Open Source Projects
nav_order: 8
---
# HTML5 Standards & Style Guide

## Philosophy

Vanilla-first means the platform is your framework. Prefer what the browser gives you natively before reaching for abstractions. Every dependency is a liability — add them deliberately, not habitually. Progressive enhancement is the default posture: content and function first, presentation layered on top.

---

## HTML5

### Document Structure

Every page starts with this canonical shell.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Page description — 150–160 characters">
    <title>Page Title — Site Name</title>
    <link rel="stylesheet" href="css/main.css">
</head>
<body>
    <!-- content -->
    <script src="js/main.js" defer></script>
</body>
</html>
```

Key rules:

- `lang` attribute on `<html>` is **mandatory** — affects screen readers and search.
- `charset` and `viewport` come before anything else in `<head>`.
- Scripts use `defer` and go at the bottom of `<body>` — never in `<head>` without `defer` or `async`.
- `<title>` follows the `Page — Site` pattern for breadcrumb clarity in browser tabs.

### Semantic Markup

Use the element that describes the content, not the one that looks right by default.

```html
<!-- Bad — div soup -->
<div class="header">
  <div class="nav">
    <div class="nav-item"><a href="/">Home</a></div>
  </div>
</div>
<div class="main-content">
  <div class="article">
    <div class="article-title">How to Write HTML</div>
  </div>
</div>

<!-- Good — semantic structure -->
<header>
  <nav aria-label="Primary navigation">
    <ul>
      <li><a href="/">Home</a></li>
    </ul>
  </nav>
</header>
<main>
  <article>
    <h1>How to Write HTML</h1>
  </article>
</main>
```

Landmark elements and their purposes:

| Element | Use for |
| --------- | --------- |
| `<header>` | Site or section header |
| `<nav>` | Navigation blocks |
| `<main>` | Primary page content (one per page) |
| `<article>` | Self-contained, independently distributable content |
| `<section>` | Thematic grouping with a heading |
| `<aside>` | Tangentially related content (sidebars, callouts) |
| `<footer>` | Footer for page or section |
| `<figure>` + `<figcaption>` | Images, diagrams, code blocks with captions |

### Heading Hierarchy

- One `<h1>` per page — the primary topic.
- Never skip levels (`<h1>` → `<h3>` without `<h2>`).
- Headings communicate document structure, not visual size. Use CSS for size.

### Forms

```html
<!-- Always pair labels with inputs -->
<label for="email">Email address</label>
<input
    type="email"
    id="email"
    name="email"
    autocomplete="email"
    required
    aria-describedby="email-hint"
>
<p id="email-hint">We'll never share your email.</p>

<!-- Fieldsets for grouped inputs -->
<fieldset>
    <legend>Notification preferences</legend>
    <label><input type="checkbox" name="notify" value="email"> Email</label>
    <label><input type="checkbox" name="notify" value="sms"> SMS</label>
</fieldset>
```

- Every `<input>` has a `<label>` — never use `placeholder` as a substitute for a label.
- Use the most specific `type` attribute available: `email`, `tel`, `url`, `number`, `date`.
- `autocomplete` attributes improve UX and reduce friction.

### Accessibility (WCAG 2.1 AA)

These are non-negotiable for static pages:

```html
<!-- Images: meaningful vs decorative -->
<img src="chart.png" alt="Bar chart showing Q3 revenue up 12% YoY">
<img src="divider.svg" alt="" role="presentation"> <!-- decorative: empty alt -->

<!-- Interactive elements need accessible names -->
<button aria-label="Close dialog">×</button>
<a href="/report.pdf" aria-label="Download Q3 report (PDF, 2MB)">Download</a>

<!-- ARIA only when native semantics don't exist -->
<div role="status" aria-live="polite" id="form-status"></div>
```

Rules:

- All images have `alt`. Decorative images have `alt=""`.
- Interactive elements are keyboard navigable — never remove `outline` without providing a replacement focus style.
- Color alone never conveys meaning.
- Minimum contrast ratio: 4.5:1 for normal text, 3:1 for large text.

---

## CSS3

### File Organisation

```
css/
├── main.css          # @import entry point only
├── base/
│   ├── reset.css     # Normalize/reset
│   └── typography.css
├── layout/
│   ├── grid.css
│   └── page.css
├── components/
│   ├── buttons.css
│   ├── forms.css
│   └── cards.css
└── utilities/
    └── helpers.css
```

`main.css` imports only — no rules directly in it:

```css
@import 'base/reset.css';
@import 'base/typography.css';
@import 'layout/grid.css';
@import 'components/buttons.css';
```

### Custom Properties (CSS Variables)

Define your entire design system as custom properties. Never hardcode values.

```css
:root {
    /* Color palette */
    --color-brand-primary: #1a6eff;
    --color-brand-secondary: #0d4abf;
    --color-neutral-900: #0f0f0f;
    --color-neutral-600: #4a4a4a;
    --color-neutral-200: #e8e8e8;
    --color-neutral-50:  #fafafa;
    --color-surface:     #ffffff;
    --color-error:       #c0392b;
    --color-success:     #27ae60;

    /* Typography */
    --font-heading: 'Georgia', serif;
    --font-body:    'system-ui', sans-serif;
    --font-mono:    'Fira Code', monospace;

    --text-xs:   0.75rem;   /* 12px */
    --text-sm:   0.875rem;  /* 14px */
    --text-base: 1rem;      /* 16px */
    --text-lg:   1.125rem;  /* 18px */
    --text-xl:   1.25rem;   /* 20px */
    --text-2xl:  1.5rem;    /* 24px */
    --text-4xl:  2.25rem;   /* 36px */

    /* Spacing (4px base) */
    --space-1:  0.25rem;
    --space-2:  0.5rem;
    --space-3:  0.75rem;
    --space-4:  1rem;
    --space-6:  1.5rem;
    --space-8:  2rem;
    --space-12: 3rem;
    --space-16: 4rem;

    /* Layout */
    --max-width-content: 72ch;
    --max-width-page:    1200px;

    /* Borders */
    --radius-sm: 4px;
    --radius-md: 8px;
    --radius-lg: 16px;

    /* Shadows */
    --shadow-sm: 0 1px 3px rgba(0,0,0,0.12);
    --shadow-md: 0 4px 12px rgba(0,0,0,0.10);

    /* Transitions */
    --transition-fast:   150ms ease;
    --transition-normal: 250ms ease;
}
```

### Reset

Use a minimal, explicit reset rather than a framework reset. Own what you apply.

```css
/* base/reset.css */
*, *::before, *::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

html {
    font-size: 100%;
    -webkit-text-size-adjust: 100%;
    scroll-behavior: smooth;
}

body {
    min-height: 100dvh;
    line-height: 1.6;
    font-family: var(--font-body);
    color: var(--color-neutral-900);
    background-color: var(--color-surface);
    -webkit-font-smoothing: antialiased;
}

img, video, svg {
    max-width: 100%;
    height: auto;
    display: block;
}

input, button, textarea, select {
    font: inherit;
}

p, h1, h2, h3, h4, h5, h6 {
    overflow-wrap: break-word;
}

/* Remove list styles when list is used for navigation (no bullet = semantic intent) */
:where(nav) ul {
    list-style: none;
}
```

### Selectors & Specificity

```css
/* Bad — high specificity, hard to override */
#main-content .article-list li.featured a.read-more { }

/* Bad — element selectors for styled components */
div { color: red; }

/* Good — low specificity, composable */
.card { }
.card--featured { }
.card__link { }

/* Good — :is() and :where() for specificity management */
:where(h1, h2, h3, h4) {
    font-family: var(--font-heading);
    line-height: 1.2;
}
```

Specificity rules:

- Prefer class selectors over ID selectors for styling.
- Never use `!important` except in utility override classes (`.sr-only`, `.visually-hidden`).
- Keep selector depth to **3 levels maximum**.
- BEM naming (`.block__element--modifier`) for component-level CSS.

### Layout: Grid & Flexbox

Prefer CSS Grid for two-dimensional layout; Flexbox for one-dimensional (row or column).

```css
/* Page-level layout — Grid */
.page-layout {
    display: grid;
    grid-template-columns: 1fr min(var(--max-width-content), 100%) 1fr;
    grid-template-rows: auto 1fr auto;
    min-height: 100dvh;
}

.page-layout > * {
    grid-column: 2;
}

/* Navigation items — Flexbox */
.nav__list {
    display: flex;
    flex-wrap: wrap;
    gap: var(--space-4);
    align-items: center;
    list-style: none;
}

/* Card grid — Grid with auto-fit */
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: var(--space-6);
}
```

### Responsive Design

Mobile-first. Write base styles for small screens; use `min-width` breakpoints to enhance for larger screens.

```css
/* Breakpoints as custom properties */
:root {
    --bp-sm: 640px;
    --bp-md: 768px;
    --bp-lg: 1024px;
    --bp-xl: 1280px;
}

/* Base: mobile */
.container {
    padding: var(--space-4);
}

/* Enhance for larger screens */
@media (min-width: 768px) {
    .container {
        padding: var(--space-8);
    }
}

@media (min-width: 1024px) {
    .container {
        max-width: var(--max-width-page);
        margin-inline: auto;
    }
}
```

### Accessibility in CSS

```css
/* Focus styles — never just remove outline */
:focus-visible {
    outline: 2px solid var(--color-brand-primary);
    outline-offset: 3px;
}

/* Screen-reader-only utility */
.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
}

/* Respect user motion preferences */
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
        scroll-behavior: auto !important;
    }
}

/* Respect user color scheme preference */
@media (prefers-color-scheme: dark) {
    :root {
        --color-surface:      #0f0f0f;
        --color-neutral-900:  #f0f0f0;
        --color-neutral-600:  #a0a0a0;
        --color-neutral-200:  #2a2a2a;
        --color-neutral-50:   #1a1a1a;
    }
}
```
