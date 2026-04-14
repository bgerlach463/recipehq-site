# MyRecipeHQ Blog & Guide Publishing Reference

Use this document when creating or publishing blog posts and guide pages for the MyRecipeHQ marketing site.

---

## URL Structure

| Content Type | Path Pattern | File Location | Example |
|---|---|---|---|
| Pillar/Guide | `/guides/<cluster-slug>/` | `guides/<slug>.html` | `/guides/kitchen-waste/` |
| Cluster post | `/blog/<post-slug>/` | `_posts/YYYY-MM-DD-<slug>.html` | `/blog/kitchen-waste-log/` |
| Standalone blog post | `/blog/<post-slug>/` | `_posts/YYYY-MM-DD-<slug>.html` | `/blog/what-to-do-with-veggie-scraps/` |

Pillar pages do NOT live in `_posts/` and do NOT appear in the blog archive listing. Cluster posts and standalone blog posts live in `_posts/` and appear in the `/blog/` archive.

---

## Categories

Only three categories exist. Every post must use one:

| Slug | Label |
|---|---|
| `reduce-kitchen-waste` | Reduce Kitchen Waste |
| `meal-planning` | Meal Planning |
| `kitchen-pantry` | Kitchen Pantry |

The blog archive at `/blog/` has filter chips for these three categories plus "All Posts."

---

## Jekyll Frontmatter

### Cluster / Standalone Blog Post

```yaml
---
layout: post
title: "Post Title | MyRecipeHQ"
description: "Meta description for search engines."
date: YYYY-MM-DD
author: Brad Gerlach
nav_active: blog
canonical: /blog/post-slug/
permalink: /blog/post-slug/
category: reduce-kitchen-waste
category_label: "Reduce Kitchen Waste"
read_time: "10 min read"
excerpt_text: "Short excerpt shown on archive cards."
hero_title: '<span class="hl">Highlighted Keywords</span><br>Rest of Title'
og_title: "Open Graph Title"
og_description: "Open Graph description."
og_url: "https://www.myrecipehq.com/blog/post-slug/"
og_type: article
schema_headline: "Schema Headline"
icons:
  - '<svg width="36" height="36" viewBox="0 0 24 24" fill="none">...</svg>'
  - '<svg width="36" height="36" viewBox="0 0 24 24" fill="none">...</svg>'
  - '<svg width="36" height="36" viewBox="0 0 24 24" fill="none">...</svg>'
  - '<svg width="36" height="36" viewBox="0 0 24 24" fill="none">...</svg>'
head_extra: |
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
  <style>
  ...post-specific CSS...
  </style>
  <script type="application/ld+json">...schema...</script>
---
```

### Pillar/Guide Page

Same as above with these differences:

```yaml
nav_active: guides          # not "blog"
canonical: /guides/cluster-slug/
permalink: /guides/cluster-slug/
cluster_tag: "PILLAR"       # triggers amber card style in archive if shown
```

File lives at `guides/<slug>.html`, not in `_posts/`.

---

## Hero Design

### Cluster Posts (dark green hero)

- Background: `#1a4a4a` (dark green)
- 5px orange accent bar at top and bottom of hero
- Two-column layout: title on left, 2x2 icon grid on right
- Title color: `#f0ede8` (cream)
- Keywords wrapped in `<span class="hl">` render in orange (`#F97316`)
- No logo in hero area (site nav provides branding)
- On mobile: icon grid hidden, single column

### Pillar Pages (charcoal hero)

- Background: `#1C1917` (charcoal, matches homepage)
- Eyebrow label above title: "[Topic] Guide" (e.g., "Kitchen Waste Guide")
- Title color: white
- Keywords wrapped in `<span class="hl-teal">` render in orange via CSS override
- Subtitle: pure white, no opacity
- Topic pills below subtitle (e.g., Waste Prevention, Composting, Storage Tips, Gardening)
- Sidebar layout with sticky table of contents

---

## Hero Title Formatting

The `hero_title` frontmatter field supports HTML. Use `<br>` for line breaks and `<span class="hl">` for orange keyword highlighting:

```yaml
hero_title: '<span class="hl">Kitchen Waste Storage:</span><br>Keep Scraps Useful,<br>Not Trash-Bound'
```

The full keyphrase for the post topic should be highlighted, not just one word. Examples:
- "Kitchen Waste Storage:" (not just "Storage")
- "Compost Using Kitchen Waste:" (not just "Compost")
- "Kitchen Waste for Gardening:" (not just "Kitchen Waste")

---

## Hero Icons

Each post has 4 unique SVG icons in the frontmatter `icons:` list. These render in the archive card grid and in the post's hero area.

Icon format: `width="36" height="36" viewBox="0 0 24 24"`, stroke-based with `#F97316` (orange) for primary strokes and `rgba(240,237,232,0.45)` for secondary strokes. Each icon has an `icon-tile-label` in the hero markup (e.g., "Scrap Bag", "Compost Bin").

---

## Blog Archive Card

Cards on `/blog/` show:
- Dark green hero with title + 2x2 icon grid
- Category label + date
- Excerpt text
- "Read the guide" link + read time

The `hero_title`, `icons`, `category_label`, `excerpt_text`, and `read_time` frontmatter fields populate the card.

---

## Sidebar (Pillar Pages Only)

```
IN THIS GUIDE
  · Section 1 title
  · Section 2 title
  · ...
  · Frequently asked questions
  · Explore [topic] management    ← links to #explore (bottom cards)

[CTA box]
  Plan meals around what you already have.
  MyRecipeHQ flags expiring ingredients first.
  [Try MyRecipeHQ Free ->]
```

- Label: "In This Guide" (not "On This Page" or "In This Series")
- The CTA box uses an IntersectionObserver to fade out when the main end-of-article CTA scrolls into view, preventing two competing CTAs visible at once
- No separate "Explore More" cluster-link section in the sidebar. The TOC entry handles navigation to the bottom cards

---

## Bottom Cluster Cards (Pillar Pages Only)

Section heading: **"Explore [Topic] Management"** (e.g., "Explore Kitchen Waste Management")
with `id="explore"` for TOC linking.

Each card has:
- Tag: uppercase category label (USE, TRACK, STORE, COMPOST, GARDEN)
- Title: post title
- Description: one-line summary
- CTA arrow: unique action text per card (not generic "Read guide")

Example CTA text:
- "Sort your scraps" (Veggie Scraps)
- "Start tracking waste" (Waste Log)
- "Better storage habits" (Storage)
- "Set up composting" (Compost)
- "Scraps to garden" (Gardening)

---

## FAQ Section

Use the `.faq-box` pattern. Do NOT use `.faq-item`, `.faq-q`, or `.faq-a` classes (they conflict with the site's accordion FAQ on `/faq/`).

```html
<div class="faq-box" id="faq">
  <h2>Frequently Asked Questions</h2>

  <h3>Question text?</h3>
  <p>Answer text.</p>

  <h3>Another question?</h3>
  <p>Answer text.</p>
</div>
```

Required CSS in `head_extra`:
```css
.faq-box { background: var(--warm-bg); border: 1px solid var(--border); border-radius: 16px; padding: 36px 40px; margin: 2.8rem 0; }
.faq-box h2 { margin-top: 0; padding-bottom: 16px; border-bottom: 1px solid var(--border); margin-bottom: 1.6rem; }
.faq-box h3 { color: var(--orange); margin-top: 1.8rem; font-family: 'Playfair Display', serif; font-size: 1rem; font-weight: 600; font-style: italic; }
.faq-box h3:first-of-type { margin-top: 0; }
.faq-box p { font-size: 0.9rem; color: var(--text-muted); line-height: 1.7; }
.faq-box p:last-child { margin-bottom: 0; }
```

---

## Internal Linking Rules

### Cluster post -> Pillar
Contextual anchor in a body paragraph (usually the intro). Use descriptive anchor text with the pillar's keywords:
```html
<a href="/guides/kitchen-waste/">guides on kitchen waste</a>
```

### Pillar -> Cluster post
Inline `.read-link` button after each body section. Use unique SEO-friendly anchor text, not generic "Read guide":
```html
<a href="/blog/kitchen-waste-log/" class="read-link">Start a kitchen waste log -></a>
```

### Cluster post -> Cluster post
Contextual in-body links with descriptive anchor text:
```html
<a href="/blog/kitchen-waste-storage/">kitchen waste storage guide</a>
```

### Anchor text rules
- Every link gets unique, keyword-rich anchor text
- Never use "Read guide," "Click here," or "Read more"
- Match the target page's primary keyword in the anchor text
- Make it read naturally in the surrounding sentence

---

## CTA Patterns

### Mid-article tip box
```html
<div class="tip-box">
  <p><strong>MyRecipeHQ</strong> suggests recipes based on what you already have, flags ingredients close to expiring, and helps you find ingredient overlap across a week of meals. <a href="/coming-soon/" style="color: var(--teal); font-weight: 600;">Try it free -></a></p>
</div>
```

### End-of-article dark block
```html
<div class="app-cta" id="main-cta">
  <div class="app-cta-text">
    <h3>Plan smarter. Waste less. Cook better.</h3>
    <p>MyRecipeHQ suggests meals based on what you already have, with expiring ingredients first.</p>
  </div>
  <a href="/coming-soon/" class="btn-cta-white">Try MyRecipeHQ Free</a>
</div>
```

### Link card (cross-link to related post)
```html
<a href="/blog/kitchen-waste-storage/" class="link-card">
  <div>
    <div class="link-card-label">Next step</div>
    <div class="link-card-title">Kitchen Waste Storage: Keep Scraps Useful, Not Trash-Bound</div>
  </div>
  <div class="link-arrow">&#8594;</div>
</a>
```

All CTAs link to `/coming-soon/` until Stripe checkout is live.

---

## CSS Override Requirements

Every post using `layout: post` needs this override in `head_extra` because the site's `style.css` applies `section { padding: 96px 0; }` globally:

```css
.page-body section, .cluster-section, .infographic-section { padding: 0; }
```

Pillar pages also need the FAQ box CSS listed above.

---

## File Conversion Process (Standalone HTML -> Jekyll Post)

When Brad provides a standalone HTML blog post file:

1. Extract the `<style>` block content -> put in `head_extra` as `<style>...</style>`
2. Extract JSON-LD `<script type="application/ld+json">` -> put in `head_extra`
3. Extract `<body>` content only
4. Strip `<header class="topbar">...</header>` (site nav provides this)
5. Strip the hero-logo div and hero-divider (site nav provides branding)
6. Remove global CSS selectors from the style block: `*, *::before, *::after { ... }`, `body { ... }`, `.topbar*`, `.logo*`, `.btn-try*`
7. Build frontmatter with all required fields
8. Extract 4 hero icon SVGs from `.icon-tile` divs -> `icons:` YAML list
9. Normalize CTA links: `href="https://www.myrecipehq.com"` -> `href="/coming-soon/"`
10. Add trailing slashes to all `/blog/` and `/guides/` href values
11. Add the section padding override CSS to `head_extra`
12. Validate: zero `href="#"` placeholders, valid YAML frontmatter, all internal links resolve to real slugs

---

## Navigation

The site nav includes a "Guides" click-dropdown between FAQ and Blog. Each guide cluster gets a link in the dropdown:

```html
<li class="nav-dropdown">
  <a class="nav-dropdown-trigger" onclick="this.parentElement.classList.toggle('open'); event.stopPropagation();">Guides</a>
  <div class="nav-dropdown-menu">
    <a href="/guides/kitchen-waste/">Reduce Kitchen Waste</a>
    <!-- Add more guide clusters here -->
  </div>
</li>
```

Mobile nav has a flat link to the first/primary guide. Update `_includes/nav.html` and `_includes/mobile-nav.html` when adding new guide clusters.
