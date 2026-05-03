---
brand: Glaido
url: https://glaido.com
tagline: "Type with your voice (World's fastest dictation)"
description: "Speak naturally. Get clean, ready-to-send text in any app. Save 20+ hours a month."
extracted_via: Firecrawl branding format
extraction_confidence: 0.925
extracted_on: 2026-05-03
---

# Glaido — Brand Style

## Colors

| Role         | Hex       | Notes                              |
|--------------|-----------|------------------------------------|
| Background   | `#0D0D0D` | Near-black, primary canvas         |
| Primary      | `#BFF549` | Lime — the brand mark              |
| Accent       | `#BFF549` | Same as primary, single-accent system |
| Text Primary | `#FFFFFF` | High-contrast white on dark        |
| Text Muted   | `#B6B6B6` | Secondary copy / muted UI          |
| Border       | `#252525` | Hairline borders, low-contrast     |
| Link         | `#BFF549` | Links use the lime accent          |

**Color scheme:** dark mode only.
**Single accent system** — every CTA, link, and brand mark uses the same lime. Never introduce a second accent.

## Typography

- **Family:** Aspekta (single typeface for headings, body, paragraphs)
- **Stack:** `Aspekta, ui-sans-serif, system-ui, sans-serif`

| Role  | Size  |
|-------|-------|
| H1    | 76px  |
| H2    | 52px  |
| Body  | 14px  |

Heavy size jump between display and body — display copy dominates, body stays small. Don't introduce intermediate sizes unless required.

## Spacing & Shape

- **Base grid unit:** 4px
- **Border radius (general):** 0px (sharp corners)
- **Border radius (buttons):** 2px (very subtle softness, almost square)
- **Shadows:** none — flat surfaces only
- **Framework:** Tailwind CSS

## Buttons

**Primary**
- Background: `#BFF549` (lime)
- Text: `#000000` (black on lime — high contrast)
- Border-radius: 2px
- Shadow: none
- Example label: *"Try Glaido free"*

**Secondary**
- Background: transparent
- Text: `#B6B6B6`
- Border: 1px `#252525`
- Border-radius: 2px
- Shadow: none
- Example label: *"Get started"*

## Logo

- **Wordmark:** `logos/logo-wordmark.svg` — 348×82 viewBox, white "Glaido" word + lime mark on the left
- **Favicon:** `icons/favicon.ico`
- **OG image:** `logos/og-image.png` (1200×630)
- **Brand pattern:** `logos/brand-pattern.svg` — repeating background pattern

**Usage rules**
- Logo always appears on the dark background `#0D0D0D` or transparent
- Never recolor the white wordmark; never replace the lime mark
- Maintain clear-space equal to the height of the lime mark on all sides

## Voice & Personality

- **Tone:** modern
- **Energy:** high
- **Audience:** tech-savvy individuals looking for efficient dictation solutions

## Integration Logos (3rd-party brand marks)

Already downloaded to `logos/integration-*`:

| File                              | Brand       |
|-----------------------------------|-------------|
| `integration-claude.svg`          | Anthropic Claude |
| `integration-cursor.svg`          | Cursor      |
| `integration-notion.png`          | Notion      |
| `integration-github.png`          | GitHub      |
| `integration-gmail.png`           | Gmail       |
| `integration-perplexity.png`      | Perplexity  |
| `integration-telegram.png`        | Telegram    |
| `integration-whatsapp.png`        | WhatsApp    |
| `integration-app7.png` … `app12.png` | Unlabeled — inspect to identify |

Use these on integration / "works with" sections. They're not Glaido-owned marks — keep their original colors.

## Asset Inventory

```
glaido-brand/
├── brand-style.md            ← this file
├── logos/
│   ├── logo-wordmark.svg     ← primary logo
│   ├── og-image.png          ← social share
│   ├── brand-pattern.svg     ← repeating background pattern
│   ├── pricing-badge.png
│   └── integration-*.{svg,png}  ← 12 third-party marks
└── icons/
    ├── favicon.ico
    └── inline-svg-{00..26}.svg   ← 27 UI icons extracted from page
                                    (00 and 26 are duplicate wordmarks; 17–24 are repeated small icons)
```

## Quick Reference (for Claude)

When asked to "use the Glaido style," default to:

```css
:root {
  --bg:        #0D0D0D;
  --fg:        #FFFFFF;
  --muted:     #B6B6B6;
  --accent:    #BFF549;
  --border:    #252525;
  --radius:    2px;
  --grid:      4px;
}
body { font-family: 'Aspekta', ui-sans-serif, system-ui, sans-serif; }
h1   { font-size: 76px; line-height: 1.05; letter-spacing: -0.02em; }
h2   { font-size: 52px; line-height: 1.1;  letter-spacing: -0.01em; }
.btn { background: var(--accent); color: #000; border-radius: var(--radius); }
```

Single accent. Sharp corners. Flat surfaces. No shadows. Big display type, small body. Always dark.

---

## Reference

**Website:** [https://glaido.com](https://glaido.com)

Extracted live via Power Design's Firecrawl recipe — see lib/extract-brand.md.
