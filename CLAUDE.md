# CLAUDE.md — fyregard.github.io

## Purpose

Static GitHub Pages portfolio site for **Leo Fyregård**, live at **fyregard.dev**.
Showcases Chrome extensions, links to their privacy policies, and hosts those policy documents.

---

## Tech Stack

- Plain HTML + CSS only — no frameworks, no build tools, no preprocessors
- JavaScript: inline or in dedicated `.js` files where it adds genuine value
- Fonts: loaded from Google Fonts (see Fonts section below)
- Hosting: GitHub Pages, custom domain `fyregard.dev` via `CNAME`

---

## Fonts

Both fonts are loaded in `<head>` via Google Fonts `<link>` tags:

| Variable   | Family               | Weights / styles loaded          | Use                        |
|------------|----------------------|----------------------------------|----------------------------|
| `--mono`   | JetBrains Mono       | 300, 400, 600, 700 (+ italic 300)| Body text, UI, code        |
| `--serif`  | DM Serif Display     | Regular + Italic                 | Headings (h1, h2, ext-name)|

---

## Colour Tokens

All colours are defined as CSS custom properties on `:root` in `style.css`. **Never hardcode a colour value** — always reference the variable.

| Variable      | Hex       | Usage                                                         |
|---------------|-----------|---------------------------------------------------------------|
| `--bg`        | `#0d0f14` | Page background (`body`)                                     |
| `--surface`   | `#13161d` | Card and box backgrounds (ext-card, toc, contact-box, etc.)  |
| `--border`    | `#1f2430` | All borders, grid texture lines                              |
| `--amber`     | `#f5a623` | Primary accent — brand, links on hover, arrows, numbers, tags|
| `--amber-dim` | `#c27d0e` | Subdued amber — tag text                                     |
| `--green`     | `#4ade80` | "Live" tag, `.ext-status` active indicator                   |
| `--muted`     | `#4a5060` | Footer text, breadcrumb separator                            |
| `--text`      | `#d4d8e2` | Primary body text                                            |
| `--text-dim`  | `#7a8090` | Secondary / subdued text (descriptions, meta, nav links)     |

---

## Layout

`.wrap` is the single layout constraint used everywhere:

```css
.wrap {
  max-width: 860px;
  margin: 0 auto;
  padding: 0 28px;
  position: relative;
  z-index: 1;   /* sits above the fixed grid texture and glow blob */
}
```

Both `<main>` and `<footer>` on `index.html` carry `.wrap` directly. On privacy pages, `.wrap` wraps the inner content div (not the `<nav>` — that uses `.wrap.breadcrumb`).

---

## Established Patterns

### Section structure (index.html)

```html
<section id="slug">
  <div class="section-header">
    <span class="section-num">01</span>
    <h2 class="section-title">Title</h2>
    <div class="section-line"></div>
  </div>
  <!-- section body -->
</section>
```

- `section-num`: two-digit amber label (01, 02, …)
- `section-title`: serif heading
- `section-line`: flex-1 horizontal rule that fills remaining width

### Extension card structure

```html
<div class="ext-card">
  <div>
    <div class="ext-tags">
      <span class="tag">Label</span>
      <span class="tag green">Live</span>
    </div>
    <h3 class="ext-name">Name</h3>
    <p class="ext-desc">Description.</p>
    <ul class="ext-features">
      <li>Feature one</li>
    </ul>
  </div>
  <div class="ext-actions">
    <span class="ext-status">Active</span>
    <a href="..." class="btn btn-primary btn-sm">Install ↗</a>
    <a href="privacy/..." class="btn btn-ghost btn-sm">Privacy Policy</a>
  </div>
</div>
```

- Add `.dim` to `.ext-card` for a dimmed "coming soon" placeholder (sets `pointer-events: none`)
- Add `.muted` to `.ext-name` for italic dimmed placeholder name

### Privacy policy list item (index.html #privacy section)

```html
<a href="privacy/slug.html" class="policy-item">
  <div class="policy-item-left">
    <span class="policy-item-name">Extension Name</span>
    <span class="policy-item-meta">Last updated · D Month YYYY</span>
  </div>
  <span class="policy-arrow">→</span>
</a>
```

### Privacy policy page structure

All privacy pages live in `/privacy/` and reference `../style.css`.
Follow `privacy/snippet-manager.html` exactly. Structure:

```
nav > .wrap.breadcrumb
  a.back  ("← Portfolio" → ../index.html)
  span.sep  ("/")
  span.crumb  ("Privacy · Extension Name")

.wrap
  header.doc-header
    p.doc-label     ("// privacy policy")
    h1              (Extension name)
    div.doc-meta    (Effective / Last updated / Version spans)

  div.summary-box
    p.summary-label ("// plain english summary")
    p               (intro sentence)
    ul.summary-points > li (icon span + text)

  div.toc
    p.toc-title     ("Contents")
    ol > li > a     (one entry per policy-section)

  div.doc-content
    div.policy-section#slug  (one per TOC entry)
      div.ps-header
        span.ps-num   (01, 02, …)
        h2.ps-title
      (p / table.data-table / ul.highlight-list / div.contact-box)

footer
  div.wrap
    p  ("© YYYY Leo Fyregård · Portfolio link")
    p  ("Extension Name Privacy Policy · vX.Y")
```

---

## File Structure

```
fyregard.github.io/
  index.html               — Main portfolio page
  style.css                — All styles (single shared stylesheet)
  CNAME                    — Custom domain: fyregard.dev
  privacy/
    snippet-manager.html   — Privacy policy for Snippet Manager extension
```

---

## Working Agreements

1. **Never hardcode colours.** Every colour value must come from a `--variable` defined in `:root`.
2. **Never change `:root` variables or global rules in `style.css` without explicit instruction.** These tokens affect every page.
3. **Always match existing patterns exactly** when adding new sections, cards, or policy list items. Copy the HTML structure above — do not invent new class names or wrapper elements.
4. **New privacy policy pages go in `/privacy/`** and must follow `privacy/snippet-manager.html` exactly in document structure, nav breadcrumb, footer format, and stylesheet reference (`../style.css`).
5. **JavaScript is fine when it adds genuine value** — keep it inline or in a dedicated `.js` file as appropriate.
6. **CSS may be split into multiple files if it improves organisation** — use logical separation (e.g. per-page or per-component).

---

## Contact & Links

- Email: leo@fyregard.dev
- GitHub: github.com/Fyregard
- Live site: fyregard.dev
