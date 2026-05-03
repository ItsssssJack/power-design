---
brand: Grind
url: https://grind.co.uk
tagline: "Better Coffee, Made by London®."
description: "A coffee company that lives in London. From a café in Shoreditch to homes all over the world. On a mission to change the way we drink coffee for the better."
extracted_via: Firecrawl branding format
extraction_confidence: 0.925
extracted_on: 2026-05-03
---

# Grind — Brand Style

## Colors

| Role         | Hex       | Notes                              |
|--------------|-----------|------------------------------------|
| Background   | `#F6DBDF` | Soft pink — Grind's signature canvas |
| Primary      | `#2D2926` | Warm near-black — text + dark buttons |
| Secondary    | `#E2255E` | Hot pink — accent / CTA highlight  |
| Link         | `#52B57A` | Green — links only                 |
| Text Primary | `#2D2926` | Same as primary, ~11:1 on pink bg (AAA) |
| Theme dark   | `#2D2926` | Used in some sections              |
| Surface alt  | `#F2EFEE` | Cream — secondary button bg        |

**Color scheme:** light mode. The soft pink `#F6DBDF` is the iconic ground.
**One accent rule:** for emphasis use `#E2255E` (hot pink). Reserve `#52B57A` for links only.

## Typography

- **Display (headings):** Argent CF — wedge/contrast serif. *Free substitute: Fraunces (variable, optical sizing).*
- **Body:** Apercu Pro — geometric sans. *Free substitute: Inter.*

| Role  | Size  |
|-------|-------|
| H1    | 80px  |
| H2    | 28px  |
| Body  | 17px  |

Big jump from H1 to H2 (3×) — display dominates, secondary headers small. Body is generous for editorial reading.

## Spacing & Shape

- **Base grid unit:** 4px
- **Border radius (general):** 6px (subtle softness)
- **Border radius (buttons):** 4px
- **Shadows:** none — flat surfaces
- **Framework:** Bootstrap-based

## Buttons

**Primary** — Background `#2D2926` · Text `#FFFFFF` · Border-radius 4px · Shadow none · Example: *"Shop Now"*
**Secondary** — Background `#F2EFEE` (cream) · Text `#2D2926` · Border-radius 4px · Shadow none · Example: *"Learn More"*

## Logo

- **Wordmark:** `logos/logo-wordmark.svg` — 788×417 viewBox, "GRIND" set in heavy display, fill `#2D2926`
- **Favicon:** `logos/favicon.png`
- **Source backup:** `logos/logo-black-source.svg` (Grind's own CDN copy)

**Usage rules**
- Logo always in `#2D2926` (warm near-black)
- Sits on the pink `#F6DBDF` ground or white
- Generous clear-space — Grind's wordmark is the brand; let it breathe

## Voice & Personality

- **Tone:** modern, slightly editorial, ironic-confident
- **Energy:** medium — premium and considered, not loud
- **Audience:** eco-conscious coffee drinkers, design-aware urbanites
- **Brand pillars:** sustainability (B Corp), London origin, café-grade at home

## Voice samples (from grind.co.uk)

- "Better Coffee, Made by London®."
- "A Coffee Company that Lives in London."
- "From a café in Shoreditch to homes all over the world."
- "This is better coffee."
- "Make your kitchen your own personal Grind café."
- "It's official. And it's a big deal. Grind is now a B Corp."
- "Reasons to buy Grind? We could name a few."

Pattern: short. Confident. ® where it earns it. London first. Sustainability without preaching.

## Brand Facts (for slide content)

- **300,000+ customers** making sustainable coffee at home
- **B Corp certified** (recently)
- **Founded ~2011**, Shoreditch café
- **21,525 kg ocean-bound plastic recovered in 2024**
- Press: Vogue, FT, Stylist, Bloomberg, Eater, The Guardian, GQ, Evening Standard
- Trustpilot: 4.1 / 5 from 12,664 reviews

## Asset Inventory

```
grind-brand/
├── brand-style.md
├── logos/
│   ├── logo-wordmark.svg     ← primary logo (extracted from data URI)
│   ├── logo-black-source.svg ← Grind's CDN copy (backup)
│   └── favicon.png
└── images/
    ├── product-packaging.jpg
    ├── product-pods-tin.jpg
    ├── product-seasonal.png
    └── product-tin-pods.png
```

## Quick Reference (for Claude)

```css
:root {
  --bg:        #F6DBDF;   /* soft pink ground */
  --fg:        #2D2926;   /* warm near-black */
  --muted:     #6B6562;   /* derived muted text */
  --accent:    #E2255E;   /* hot pink — emphasis only */
  --link:      #52B57A;   /* green — links only */
  --surface:   #FFFFFF;
  --surface-alt: #F2EFEE;
  --radius:    6px;
  --radius-btn: 4px;
  --grid:      4px;
}
body {
  font-family: 'Apercu Pro', 'Inter', ui-sans-serif, system-ui, sans-serif;
  background: var(--bg);
  color: var(--fg);
}
h1, h2, h3 {
  font-family: 'argent-cf', 'Fraunces', Georgia, serif;
  letter-spacing: -0.01em;
}
h1 { font-size: 80px; line-height: 1.05; }
.btn-primary { background: var(--fg); color: #fff; border-radius: var(--radius-btn); }
```

Soft pink ground. Warm near-black type. Editorial serif display. One hot-pink accent. Generous breathing room. Always sustainable, always London.

---

## Reference

**Website:** [https://grind.co.uk](https://grind.co.uk)

Extracted live via Power Design's Firecrawl recipe — see lib/extract-brand.md.
