# Extract a brand — the Firecrawl recipe

Power Design extracts a brand's design DNA from any URL using Firecrawl's `branding` format. The result is a `brand-style.md` file you can drop into `brands/<slug>/` and reference forever.

---

## What you need

1. **Firecrawl API key** — get one at [firecrawl.dev](https://firecrawl.dev). Free tier covers ~500 scrapes/month.
2. **A target URL** — any production homepage. Marketing pages work better than dashboards (more brand DNA, less app chrome).

---

## The one-shot scrape

Single API call. Returns colors, typography, logo, voice, components — already structured.

```bash
curl -sX POST https://api.firecrawl.dev/v1/scrape \
  -H "Authorization: Bearer $FIRECRAWL_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://glaido.com",
    "formats": ["branding", "screenshot", "rawHtml", "links"]
  }' | jq .data.branding
```

The `branding` field returns something like:

```json
{
  "colorScheme": "dark",
  "colors": {
    "primary":     "#BFF549",
    "background":  "#0D0D0D",
    "textPrimary": "#FFFFFF",
    "link":        "#BFF549"
  },
  "fonts": [{ "family": "Aspekta" }],
  "typography": {
    "fontStacks": { "heading": ["Aspekta", "ui-sans-serif", "..."] },
    "fontSizes":  { "h1": "76px", "h2": "52px", "body": "14px" }
  },
  "components": {
    "buttonPrimary": { "background": "#BFF549", "textColor": "#000000", "borderRadius": "2px" }
  },
  "images": {
    "logo":    "<inline SVG or data URI>",
    "favicon": "https://glaido.com/favicon.ico",
    "ogImage": "https://glaido.com/og/default.png"
  },
  "personality": { "tone": "modern", "energy": "high" },
  "designSystem": { "framework": "tailwind" },
  "confidence": { "overall": 0.925 }
}
```

That's the gold. You also get a screenshot URL, the full rawHtml, and a flat list of links for free.

---

## Convert it into a `brand-style.md` file

Use `brands/_template.md` as the schema. Fill in:

- **Frontmatter** — `brand`, `slug`, `website`, `extracted_via: Firecrawl`
- **Colors table** — the `branding.colors` map
- **Typography** — `branding.typography.fontStacks` + `fontSizes`
- **Spacing & shape** — derive from `branding.spacing.borderRadius` and `components`
- **Buttons** — `branding.components.buttonPrimary` + `buttonSecondary`
- **Logo** — extract the inline SVG from `branding.images.logo` and save as `brands/<slug>/logo.svg`
- **Voice samples** — pull 5–10 short headlines from the rawHtml (`<h1>`, `<h2>`, hero copy)
- **Quick reference** — a CSS variables block so Claude can drop tokens straight into output

---

## Common gotcha — white-fill SVG logos

When sites use single-color SVG logos via `<img>`, they often hardcode `fill="#FFFFFF"` so they show on their dark site. When you embed those in slides on a different background, white-on-white = invisible.

**Fix once when extracting:**

```bash
# replace white fills with the brand's primary color
sed -i '' 's/fill="#FFFFFF"/fill="#BFF549"/g' brands/<slug>/logo.svg
```

Or use `currentColor` and let CSS handle it.

---

## Fast scan — what you actually need

If you're in a hurry, the minimum viable extract is just:

| Field | From `branding` |
|---|---|
| Background | `colors.background` |
| Foreground | `colors.textPrimary` |
| Accent | `colors.primary` (or `colors.secondary` if primary is the bg) |
| Display font | `fonts[0].family` |
| Border radius | `spacing.borderRadius` |
| Voice sample | 1–2 headlines from rawHtml |

These six values + the 20 design rules in `principles/design-principles.md` are enough for Claude to compose a brand-coherent deck.

---

## Live examples in this repo

- `brands/glaido/brand-style.md` — extracted live from `glaido.com` (dark + lime + Aspekta)
- `brands/grind/brand-style.md` — extracted live from `grind.co.uk` (light + pink + Fraunces)

Two opposite brands, one extraction recipe.
