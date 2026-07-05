# Design Principles for Codified Website Generation
*Research compiled for the Power Design skill — the website counterpart to the 20 slide rules — July 2026*

> Scope: every rule below is **codifiable** — a number, ratio, threshold, or a rule of the form "if X then Y." Rules that resist measurement ("make it feel premium") have been refused or rewritten as concrete checks. This is the web sibling of `design-principles.md`. Where the two overlap (grid, contrast, hierarchy) the web version wins for web output — a slide is a fixed 1920×1080 frame; a page is a fluid, interactive, keyboard-navigable, indexable *system*. That difference is the whole point of this file.
>
> The slide rules answer *"is this frame beautiful and legible?"* These rules answer four questions a slide never has to: *Does it hold up from 360px to 1440px? Is it fast? Can everyone operate it? Does it convert?*

---

## TL;DR — The 20 Rules That Matter Most for Websites

1. **Mobile-first, fluid to a capped measure.** Design the 360 px column first, then let it grow. Never let content run edge-to-edge on desktop: page shell `max-width` 1200–1440 px, text column ≤ 75ch. The desktop layout is the mobile layout with room added — not a different design. [Marcotte, *Responsive Web Design*; Frost, *Atomic Design*]
2. **Breakpoints follow content, not devices.** Add a breakpoint only where the layout visibly breaks. Anchor on 640 / 768 / 1024 / 1280 as defaults; never target "iPhone" widths. Test at 320, 768, 1024, 1440. [Frost; Tailwind breakpoint system]
3. **Fluid type and space with `clamp()`.** Type and section rhythm scale continuously with the viewport — no snapping at breakpoints. Body `clamp(1rem, 0.9rem + 0.4vw, 1.125rem)`; H1 `clamp(2rem, 1.2rem + 4vw, 3.75rem)`. [Utopia — Mudford & Gilyead; MDN `clamp()`]
4. **Body ≥16 px; tap targets ≥44×44 px with ≥8 px between.** 16 px is the floor that stops iOS from zooming form inputs; 44×44 is the Apple HIG / WCAG 2.2 SC 2.5.8 minimum touch target. [Apple HIG; WCAG 2.2 §2.5.8]
5. **One primary action per view.** Exactly one filled, accent-colored CTA per screenful (≥44 px tall); everything else is secondary or ghost. Repeat *the same* CTA down a long page — don't invent new ones. [Krug, *Don't Make Me Think*; Hick's Law]
6. **The fold answers three questions in five seconds.** *What is this, who is it for, what do I do next* — all resolvable without scrolling on both a 1366×768 laptop and a 390 px phone. [NN/g; Krug 5-second test]
7. **Scan patterns: F for text, Z for heroes; body left-aligned.** Long copy is scanned in an F; landing heroes read as a Z with the CTA on the terminal. Left-align body — **never justify on the web** (no hyphenation engine → rivers). [NN/g eye-tracking 2006–2023; Butterick]
8. **Measure 45–75 characters.** Body line length 45–75ch, ideal ~66. Set `max-width: 65ch` on prose blocks; full-bleed text is a legibility bug. [Bringhurst; Butterick]
9. **Line-height ≥1.5 body / 1.0–1.2 display; rhythm on 8.** Body leading ≥1.5 is a WCAG 1.4.12 success criterion, not a taste call. Paragraph spacing ≥0.75em. Display tightens to 1.0–1.2 with −0.01 to −0.02em tracking. [WCAG 2.2 §1.4.12; Bringhurst]
10. **8-point spacing, one modular type scale.** Every margin/padding/gap ∈ {4, 8, 12, 16, 24, 32, 48, 64, 96, 128}. Sizes derive from one ratio (1.2 for text, 1.25–1.333 for display). No ad-hoc 13 px, no ad-hoc 27 px. [Material Design; Bryn Jackson, "8-Point Grid"]
11. **WCAG 2.2 AA is the floor, not the goal.** Text ≥4.5:1 (large ≥3:1); UI components, icons, and focus indicators ≥3:1 (SC 1.4.11); never encode meaning by hue alone (SC 1.4.1). Aim 7:1 (AAA) on body. [WCAG 2.2 §1.4.3 / 1.4.11 / 1.4.1]
12. **Semantic color tokens in OKLCH, not raw hex.** Reference `--bg / --fg / --accent / --muted / --border`, defined once and re-themed for dark via the *same names*. OKLCH gives perceptually even ramps and predictable contrast. [W3C Design Tokens CG; Ottosson OKLCH; next-themes]
13. **Every interactive element ships five visible states.** `default / hover / focus-visible / active / disabled`. A ≥3:1, ≥2 px `:focus-visible` ring is mandatory — hover-only affordances are invisible to keyboard and touch users. [WCAG 2.2 §2.4.11 & §2.4.13; Radix UI]
14. **Design the empty, loading, and error states — not just the happy path.** Skeletons over spinners for content-shaped waits; inline errors adjacent to the field that failed; empty states carry the primary next action instead of a dead end. [NN/g; Refactoring UI]
15. **Motion is fast, purposeful, and opt-out.** Transitions 150–300 ms, ease-out on enter; honor `prefers-reduced-motion: reduce`; no autoplay that can't be paused; nothing flashes >3×/second. [Material motion; WCAG 2.2 §2.2.2 / §2.3.1 / §2.3.3]
16. **Reserve space — protect CLS.** Always declare `width`/`height` or `aspect-ratio` on media and reserve slots for embeds/ads so nothing reflows on load. Cumulative Layout Shift < 0.1. [web.dev, Core Web Vitals]
17. **Ship against a performance budget.** LCP < 2.5 s, INP < 200 ms, CLS < 0.1 on mid-tier mobile over 4G. Hero image ≤ 200 KB, total JS ≤ 300 KB gzip, ≤ 2 font families with `font-display: swap` + `preload`. [web.dev; Google 2024 — INP replaced FID]
18. **Landmarked, keyboard-complete, exactly one `<h1>`.** Real `<header><nav><main><footer>`, a skip-link, one `<h1>`, no skipped heading levels, and a visible focus order that matches DOM order. [WCAG 2.2 §1.3.1 / §2.4.1; MDN]
19. **Forms: visible label, right input type, inline validation, fewest fields.** Every input a persistent `<label>` (placeholders are not labels), correct `type` + `autocomplete`, validate on blur with the message beside the field, and ask for the minimum fields that do the job. [Baymard Institute; NN/g; WCAG 2.2 §3.3]
20. **Ship the meta layer — the page isn't done until it shares well.** `<title>` ≤ 60ch, meta description ≤ 155ch, one Open Graph image at 1200×630, `theme-color`, a full favicon set, and JSON-LD for the page's primary entity. [Open Graph protocol; schema.org; Google Search Central]

---

## Section 1: Responsive & Fluid Layout

### Principle: Mobile-First Cascade
**Source:** Luke Wroblewski, *Mobile First* (2011); Ethan Marcotte, *Responsive Web Design* (2010).
**Rule:** Author the smallest layout as the base stylesheet; add complexity upward with `min-width` media queries. Mobile-first forces content priority — you decide what matters when you only have 360 px, then *add* for larger screens rather than hiding for smaller ones.
**Codifiable check:** Media queries use `min-width` (not `max-width`) as the default direction. Base styles carry a working single-column layout with zero media queries applied.
**Example:** `.grid { display: grid; gap: 24px; }` → `@media (min-width: 768px) { .grid { grid-template-columns: repeat(3, 1fr); } }`.

### Principle: Content-Out Breakpoints
**Source:** Brad Frost, *Atomic Design* (2016); Stephen Hay.
**Rule:** A breakpoint exists where the *content* breaks — a headline wraps badly, a card row gets too wide to scan, a nav no longer fits. Not where a popular phone happens to be. Default anchors: 640 / 768 / 1024 / 1280 px. Cap at 3–4 breakpoints for a marketing page.
**Codifiable check:** No media query is named or justified by a device ("iPhone 14"). Every breakpoint has a visible layout reason.
**Test matrix:** 320 (small phone), 390 (modern phone), 768 (tablet portrait), 1024 (tablet landscape / small laptop), 1440 (desktop). Zero horizontal scroll at every width (WCAG 1.4.10 Reflow — content reflows at 320 px / 400% zoom with no 2-axis scrolling).

### Principle: Fluid Type & Space (Utopia method)
**Source:** James Gilyead & Trys Mudford, *Utopia* (2020); CSS `clamp()`.
**Rule:** Interpolate type and spacing between a min (at ~320 px) and max (at ~1240 px) viewport so there are no jumps at breakpoints. `clamp(MIN, PREFERRED, MAX)` where `PREFERRED` mixes a `rem` base and a `vw` term.
**Codifiable:**
- Body: `clamp(1rem, 0.92rem + 0.4vw, 1.125rem)` (16 → 18 px).
- H1: `clamp(2rem, 1.1rem + 4.5vw, 3.75rem)` (32 → 60 px).
- Section padding: `clamp(3rem, 2rem + 6vw, 8rem)`.
**Guard:** Never put a raw `vw` unit on type without `clamp()` — it fails WCAG 1.4.4 (text must scale to 200%). The `rem` term inside `clamp` preserves user zoom.

### Principle: Capped Measure & Container Widths
**Source:** Bringhurst; Refactoring UI; Tailwind container scale.
**Rule:** Text is never full-viewport-wide. Page shell max-width 1200–1440 px, centered with auto margins and a gutter (`padding-inline: clamp(1rem, 5vw, 4rem)`). Prose columns capped at 65–75ch.
**Codifiable:** `.container { max-width: 1280px; margin-inline: auto; padding-inline: clamp(16px, 5vw, 64px); }`. `.prose { max-width: 68ch; }`.

### Principle: Intrinsic Layout (let the browser do the math)
**Source:** Jen Simmons, "Intrinsic Web Design" (2018); Heydon Pickering, *Every Layout*.
**Rule:** Prefer intrinsic responsive primitives over breakpoint-toggled columns:
- `grid-template-columns: repeat(auto-fit, minmax(min(100%, 18rem), 1fr))` — cards that reflow with no media query.
- `flex-wrap: wrap` + `flex: 1 1 <basis>` for toolbars.
- `clamp()` for widths as well as type.
**Slide-vs-web note:** Slides are fixed frames; a web layout that only works at the widths you happened to test is broken. Intrinsic layouts survive widths you never tried.

---

## Section 2: Visual Hierarchy & Scanning on Screen

### Principle: The Five-Second Fold
**Source:** Steve Krug; NN/g "How Long Do Users Stay on Web Pages?" (Weinreich et al.; NN/g).
**Rule:** Above the fold (no scroll) on both 1366×768 and 390×844, a first-time visitor can answer: **What is this? Who is it for? What's the next step?** If any answer requires scrolling, the hero has failed.
**Codifiable check:** Hero contains, in the first viewport: one `<h1>` value proposition (≤12 words), one supporting line (≤20 words), one primary CTA. Nav does not consume >72 px of vertical height on mobile.

### Principle: F-Pattern (text) / Z-Pattern (hero) Scanning
**Source:** NN/g eye-tracking (2006, 2017, 2023).
**Rule:** Text-dense pages are scanned in an F — front-load the first two words of headings and list items with the informative term. Sparse hero/landing sections read as a Z: logo top-left → nav/CTA top-right → diagonal to the value prop → primary CTA bottom-right.
**Codifiable:** Headings and link text are not centered on text-heavy pages; the informative word is first ("Pricing that scales" not "Simple, transparent pricing that scales"). Primary hero CTA sits on the Z terminal (lower-right of the hero band) or directly under the value prop.

### Principle: Scale-Based Emphasis (web scale)
**Source:** Refactoring UI (Wathan & Schoger); Müller-Brockmann.
**Rule:** Primary heading ≥2× body; section heading ≥1.5× body. Avoid sizes only 10–20% apart — they read as a mistake, not a level. On the web, also use *color and weight* to make secondary text recede: mute it to a `--muted` token rather than shrinking it below 16 px.
**Codifiable:** H1:body ∈ [2.5, 4.0], H2:body ∈ [1.6, 2.2], H3:body ∈ [1.25, 1.5]. Muted text = same size, lower-contrast token (still ≥4.5:1).

### Principle: One Focal Point Per Section
**Source:** Reynolds; classical composition.
**Rule:** Each full-viewport section has exactly one thing the eye lands on first — a headline, a product shot, a number, or a CTA. Squint test: one element dominates by size, color, or isolation.
**Codifiable:** The dominant element is ≥1.5× the area of the next, OR the only accent-saturated element, OR isolated by ≥48 px more whitespace than anything else in the section.

### Principle: Don't Make Me Think (structural clarity)
**Source:** Steve Krug (2000, rev. 2014).
**Rule:** Layout structure requires zero thought — only content does. Conventions exist for a reason: logo top-left links home, nav across the top or in a hamburger on mobile, primary CTA visually loudest, search where search lives. Break a convention only with a clearly better, equally learnable pattern.
**Codifiable check:** Clickable things look clickable (affordance: fill, underline on hover, cursor pointer) and non-clickable things don't. No "mystery meat" navigation (icon-only nav without labels/tooltips).

---

## Section 3: Typography on Screen

### Principle: 16 px Floor & Fluid Modular Scale
**Source:** iOS input-zoom behavior; Bringhurst; Tim Brown, *Modular Scale*.
**Rule:** Body ≥16 px always (form inputs ≥16 px too, or mobile Safari zooms on focus). Derive the scale from one ratio: 1.200 (dense/UI), 1.250 (default web), 1.333 (marketing/confident). Pair with `clamp()` for fluidity.
**Codifiable default:** base 16 px, ratio 1.25 → 16, 20, 25, 31, 39, 49, 61 → round to 16, 20, 24, 32, 40, 48, 60. Expose as `--step--1 … --step-5` custom properties.

### Principle: Line Length, Leading & Paragraph Rhythm
**Source:** Bringhurst; Butterick; WCAG 1.4.12 (Text Spacing).
**Rule:**
- Measure 45–75ch (`max-width: 65ch`).
- Body line-height ≥1.5; headings 1.1–1.25; display ≤1.1.
- Paragraph spacing ≥0.75em; letter-spacing on body 0; display −0.01 to −0.02em; ALL-CAPS +0.05 to +0.1em.
**WCAG note:** 1.4.12 requires no loss of content when users force line-height 1.5, paragraph spacing 2em, letter-spacing 0.12em, word-spacing 0.16em. Don't set fixed-height text containers that would clip under those overrides.

### Principle: Web Font Loading Strategy
**Source:** Zach Leatherman, "Comprehensive Guide to Font Loading"; web.dev.
**Rule:** ≤2 families. `font-display: swap` (or `optional` for body to avoid layout shift). `preload` the one or two critical woff2 files. Provide a metrics-matched system fallback (`size-adjust` / `ascent-override` via `@font-face`, or `font-size-adjust`) so the swap doesn't shift layout (CLS).
**Codifiable:** self-host woff2 (or use a font CDN with `preconnect`); subset to the character set used; never block first paint on a decorative display face.

### Principle: System Font Stack as a Valid Default
**Source:** GitHub / Bootstrap system stack; performance-first design.
**Rule:** When brand DNA doesn't mandate a specific typeface, the system stack (`-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`) is a legitimate, zero-latency choice. A single well-set typeface beats two poorly-paired ones.

---

## Section 4: Color, Contrast & Theming

### Principle: Semantic Token Architecture
**Source:** W3C Design Tokens Community Group; Salesforce/Jina Anne; Radix Colors.
**Rule:** Never reference raw hex in components. Define a two-tier system:
- **Primitive tokens** — the raw ramp (`--blue-500`).
- **Semantic tokens** — role-mapped (`--color-bg`, `--color-fg`, `--color-accent`, `--color-muted`, `--color-border`, `--color-focus`).
Components reference *only* semantic tokens. Dark mode remaps the semantic layer; components don't change.
**Codifiable:** A component CSS file contains zero hex literals — only `var(--color-*)`.

### Principle: OKLCH Ramps
**Source:** Björn Ottosson (OKLCH, 2020); Lea Verou; Tailwind v4 default color space.
**Rule:** Build color ramps in OKLCH, not HSL/hex. OKLCH is perceptually uniform — equal lightness steps *look* equal, and you can shift hue without lightness drift. Generate a 12-step scale (backgrounds → borders → solid → text) à la Radix.
**Codifiable:** `--accent: oklch(0.62 0.19 264);`. Hold L and C, vary H for harmonized accents; hold H, vary L for a ramp.

### Principle: WCAG 2.2 Contrast (web targets)
**Source:** WCAG 2.2 §1.4.3, §1.4.11.
**Rule:**
| Element | AA | AAA |
|---|---|---|
| Body text (<18.66 px bold / <24 px regular) | 4.5:1 | 7:1 |
| Large text (≥24 px regular / ≥18.66 px bold) | 3:1 | 4.5:1 |
| UI components, icons, focus rings, chart marks (SC 1.4.11) | 3:1 | — |
**Web note:** placeholder text, disabled-looking-but-active controls, and hover states routinely fail. Test the *actual* states, not just the resting one. Aim AAA on long-form body.

### Principle: Never Hue Alone
**Source:** WCAG 1.4.1; Brewer, *ColorBrewer*.
**Rule:** Any color-coded meaning (error/success, chart series, status dot) carries a second cue: icon, label, shape, or position. ~8% of men have red-green color-vision deficiency.
**Codifiable:** Error state = red + icon + text; success = green + check + text. Chart series = color + direct label or pattern.

### Principle: Dark Mode as a First-Class Theme
**Source:** Material 3; Apple HIG Dark Mode; next-themes.
**Rule:** Dark mode is not "invert the colors." Rules:
- Elevate surfaces with lighter neutrals, not drop shadows (shadows disappear on dark).
- Desaturate accents slightly (bright saturated hues vibrate on black).
- Body contrast on dark: target 7:1 but avoid pure `#FFF` on pure `#000` (halation) — use `oklch(0.96 …)` on `oklch(0.16 …)`.
- Respect `prefers-color-scheme` *and* provide a manual toggle that persists (localStorage) and blocks the flash of wrong theme (inline head script sets the class before paint).
**Codifiable:** `:root { --color-bg: …; } @media (prefers-color-scheme: dark) { :root { --color-bg: …; } }` plus a `[data-theme="dark"]` override for the manual switch.

### Principle: 60-30-10 on the Web
**Source:** Itten tradition; Refactoring UI.
**Rule:** 60% dominant neutral surface, 30% secondary (text, cards, borders), 10% accent (CTAs, links, active states). The accent is scarce so it *means* "act here." Flooding a page with brand color destroys the signal.

---

## Section 5: Spatial Systems & Grid

### Principle: 8-Point Spacing Scale
**Source:** Bryn Jackson (2015); Material Design.
**Rule:** All spacing ∈ multiples of 8 (4 allowed for icon-tight work): 4, 8, 12, 16, 24, 32, 48, 64, 96, 128. Expose as `--space-1 … --space-9`. Vertical rhythm between sections uses the large end (64–128); intra-component padding uses the small end (8–24).
**Codifiable:** Reject any spacing value not on the scale. No 13 px, no 27 px, no 45 px.

### Principle: 12-Column Fluid Grid + Gap
**Source:** Müller-Brockmann; Bootstrap/Material grid; CSS Grid.
**Rule:** Use a 12-column grid with a consistent `gap` (24–32 px desktop, 16 px mobile) and outer gutter. Prefer CSS Grid `grid-template-columns` and `gap` over margin math. Common spans: 4 (third), 6 (half), 8 (two-thirds), 12 (full).
**Codifiable:** `display: grid; grid-template-columns: repeat(12, 1fr); gap: clamp(16px, 2vw, 32px);` with children spanning column tracks.

### Principle: Vertical Rhythm & Section Cadence
**Source:** Bringhurst; editorial web practice.
**Rule:** Sections breathe on a consistent vertical cadence. Section padding ≥ `clamp(48px, 6vw, 128px)` top and bottom. Related blocks ≤16 px apart; unrelated ≥48 px (proximity = relationship). The gap between groups ≥2× the gap within a group.

### Principle: Consistent Radius & Elevation Tokens
**Source:** Material elevation; Refactoring UI shadows.
**Rule:** One radius scale (`--radius-sm/md/lg/full`, e.g. 6/10/16/9999) and one elevation scale (layered, low-opacity shadows — never a single harsh `0 0 10px #000`). Radius and shadow are tokens, reused, never ad-hoc per component.
**Codifiable:** Shadows use ≥2 stacked layers at ≤0.12 opacity; dark mode swaps shadow for border/surface-lightening.

---

## Section 6: Interaction, State & Feedback

### Principle: Five States for Every Interactive Element
**Source:** Material states; Radix UI; WCAG 2.4.11 (Focus Not Obscured), 2.4.13 (Focus Appearance).
**Rule:** Buttons, links, inputs, and controls each define: **default, hover, focus-visible, active, disabled**. Focus is styled with `:focus-visible` (keyboard) so mouse users don't see rings but keyboard users always do. Focus ring ≥2 px, ≥3:1 against adjacent colors, not clipped by `overflow: hidden`.
**Codifiable:** Every interactive selector has `:hover`, `:focus-visible`, `:active`, `[disabled]`/`[aria-disabled]` rules. `outline: none` without a replacement focus style is a defect.

### Principle: Touch, Pointer & Hover Parity
**Source:** Apple HIG; WCAG 2.5.8 (Target Size); `@media (hover)`.
**Rule:** Never hide essential affordances behind hover alone — touch devices have no hover. Use `@media (hover: hover)` for hover enhancements only. Tap targets ≥44×44 px with ≥8 px spacing. Increase target size on coarse pointers.
**Codifiable:** Any info revealed on `:hover` is also reachable on `:focus` and on tap (click/tap toggles it on touch).

### Principle: Empty, Loading & Error States
**Source:** NN/g; Refactoring UI; Shopify Polaris.
**Rule:** No component ships happy-path-only.
- **Loading:** skeleton screens for content-shaped waits (reduce perceived latency); spinners only for indeterminate <1 s actions. Reserve the final layout's dimensions so the skeleton doesn't shift (CLS).
- **Empty:** explain what goes here + the primary action to fill it. Never a blank void.
- **Error:** human-readable, adjacent to cause, with a recovery path. Never a raw stack trace or a top-of-page banner for a field-level error.
**Codifiable check:** every data-driven region has three designed states.

### Principle: Perceived Performance & Optimistic UI
**Source:** NN/g response-time limits (0.1 s / 1 s / 10 s — Nielsen 1993).
**Rule:** Respond to input in <100 ms (even just a pressed state). For actions <1 s, no spinner. For 1–10 s, show determinate progress. Optimistic UI (apply the change immediately, reconcile on server response) for high-confidence actions like likes/toggles.

### Principle: Motion Discipline
**Source:** Material motion; WCAG 2.2.2 (Pause/Stop/Hide), 2.3.1 (Three Flashes), 2.3.3 (Animation from Interactions).
**Rule:** Durations 150–300 ms for UI transitions (enter ~250 ms ease-out, exit ~200 ms ease-in), page/section reveals ≤500 ms. Honor `@media (prefers-reduced-motion: reduce)` — kill transforms/parallax, keep opacity. No autoplaying motion that can't be paused; nothing flashes >3×/s. Animate `transform`/`opacity` (compositor-friendly), never `top/left/width/height` (layout thrash).
**Codifiable:** a global `@media (prefers-reduced-motion: reduce) { *,*::before,*::after { animation-duration:0.01ms!important; transition-duration:0.01ms!important; scroll-behavior:auto!important; } }` reset is present.

---

## Section 7: Conversion & Landing-Page Structure

### Principle: One Primary Action Per View (Hick's Law applied)
**Source:** Hick & Hyman (1952); Krug; Cialdini (clarity of ask).
**Rule:** Each screenful has one primary CTA (filled, accent, ≥44 px), optionally one secondary (ghost/text). More than one primary = none. Repeat the *same* primary CTA at natural decision points down the page (after hero, after proof, after pricing, at the end) — consistency, not novelty.
**Codifiable:** Count filled accent buttons visible per viewport section → must be ≤1.

### Principle: Canonical Landing-Page Spine
**Source:** Synthesis — NN/g; Julian Shapiro, "How to build a landing page"; observed SaaS/DTC/service patterns (see `site-blueprint`).
**Rule:** A high-intent marketing page follows a legible spine; reorder for the archetype but keep the beats:
1. **Hero** — value prop + subhead + primary CTA + one proof/visual.
2. **Social proof** — logos, rating, or a marquee testimonial (immediately after the hero — borrow credibility before asking for attention).
3. **Problem → outcome** — the pain and the after-state.
4. **How it works** — 3 steps (Miller-friendly).
5. **Features as benefits** — each feature titled by the outcome, not the mechanism.
6. **Deeper proof** — case study, metric, testimonial with a face + name + role.
7. **Pricing** — 3 tiers, middle highlighted as default (Hick's Law: cap visible options at 3–4).
8. **FAQ / objection handling.**
9. **Final CTA** — restate the value prop + the same primary action.
10. **Footer** — nav, legal, secondary links, trust marks.
**Archetype note:** local-service pages front-load phone CTA + service area + trust badges; SaaS front-loads a demo/trial + feature trio; DTC front-loads a bestseller grid + UGC. Structure follows intent.

### Principle: CTA Design
**Source:** Refactoring UI; Baymard; contrast research.
**Rule:** Primary CTA = the loudest element in its section: filled accent, ≥4.5:1 label contrast, verb-first label describing the outcome ("Start free trial", not "Submit"). Reduce friction copy beneath it ("No card required"). One idea per button.
**Codifiable:** CTA label starts with a verb; button height ≥44 px; label ≤4 words; padding ≥16px×24px.

### Principle: Trust & Social Proof Placement
**Source:** Cialdini, *Influence* (social proof, authority); Baymard.
**Rule:** Credibility markers appear *before* the ask escalates: customer logos or a rating in/after the hero; named testimonials with photo + role near pricing; security/guarantee marks at the point of payment. Faceless quotes and vague "10,000+ users" without specifics under-convert vs. specific, attributed proof.

### Principle: Scarcity & Friction, Honestly
**Source:** Conversion practice; ethical-design constraints (avoid dark patterns — see §Contradictions).
**Rule:** Reduce steps to the goal (fewer fields, guest checkout, fewer clicks). Any urgency/scarcity must be true. No confirmshaming, no disguised ads, no forced continuity. Deceptive patterns are increasingly illegal (EU DSA, FTC) and always brand-toxic.

---

## Section 8: Forms

### Principle: Label, Type, Autocomplete
**Source:** WCAG 2.2 §1.3.5 (Identify Input Purpose), §3.3; MDN; Baymard.
**Rule:** Every field has a persistent visible `<label>` (a placeholder is not a label — it vanishes on focus and fails a11y). Use the correct `type` (`email`, `tel`, `number`, `url`) to trigger the right mobile keyboard, and `autocomplete` tokens (`email`, `given-name`, `cc-number`) so browsers can fill.
**Codifiable:** zero inputs rely on placeholder-as-label; `<label for>` or wrapping label on 100% of fields; `autocomplete` present on identity/payment fields.

### Principle: Inline Validation & Error Recovery
**Source:** Baymard checkout research; NN/g; WCAG §3.3.1/§3.3.3.
**Rule:** Validate on blur (not on every keystroke, not only on submit). Error message sits adjacent to the field, names the problem *and* the fix, and the field is marked `aria-invalid` + linked via `aria-describedby`. Never clear the user's input on error. Don't disable the submit button silently — explain what's missing.
**Codifiable:** error text within 8–16 px of its field; programmatic association present; input values preserved across a failed submit.

### Principle: Minimum Fields & Field Grouping
**Source:** Baymard ("average checkout has 11.8 fields; can be ~7"); NN/g.
**Rule:** Ask for the fewest fields that accomplish the task; every field has a cost in conversion. Group related fields (proximity, `<fieldset>`/`<legend>`), single-column layout (multi-column forms slow completion and cause skipped fields). One primary action per form.
**Codifiable:** forms are single-column; optional fields marked "(optional)" rather than starring required ones; multi-step forms show step N of M + a progress indicator.

### Principle: Mobile Form Ergonomics
**Source:** Apple HIG; Baymard mobile.
**Rule:** Inputs ≥16 px font (no zoom), ≥44 px tall; correct `inputmode`; large tap-friendly selects/radios; primary submit reachable in the thumb zone; avoid fixed elements that cover fields when the keyboard opens.

---

## Section 9: Navigation & Information Architecture

### Principle: Predictable Global Nav
**Source:** Krug; NN/g navigation research.
**Rule:** Logo top-left → home. Primary nav ≤7 top-level items (Miller). Current location is indicated (active state). On mobile, collapse to a labeled control (a "Menu" text or a hamburger *with* a label/aria-label); the toggle is ≥44 px and keyboard-operable, and the opened menu traps focus and closes on Esc.
**Codifiable:** `<nav aria-label>`, `aria-current="page"` on the active item, hamburger has `aria-expanded` + `aria-controls`.

### Principle: Findability — Search, Breadcrumbs, Footer
**Source:** NN/g IA; Rosenfeld & Morville, *Information Architecture*.
**Rule:** For content-heavy sites: provide search, breadcrumbs for depth >2, and a fat footer as a sitemap. Every page reachable in ≤3 clicks from home. No orphan pages.

### Principle: Skip Link & Keyboard Path
**Source:** WCAG 2.2 §2.4.1 (Bypass Blocks), §2.1.1 (Keyboard).
**Rule:** A visible-on-focus "Skip to content" link is the first focusable element. The entire site is operable by keyboard in a logical order; no keyboard traps; focus is never hidden behind sticky headers (SC 2.4.11).
**Codifiable:** `Tab` order matches visual order; `:focus` never disappears under a sticky bar (add `scroll-margin-top`).

### Principle: Sticky Headers, Sanely
**Source:** NN/g sticky-nav studies.
**Rule:** A sticky header may consume ≤10–12% of viewport height and must shrink or hide on scroll-down / reveal on scroll-up if it's tall. Anchor targets get `scroll-margin-top` equal to the sticky height so headings aren't hidden under it.

---

## Section 10: Performance (Core Web Vitals as a Design Constraint)

### Principle: The Three Core Web Vitals
**Source:** Google web.dev; 2024 update (INP replaced FID as a Core Web Vital in March 2024).
**Rule (75th-percentile, mobile):**
| Metric | Good | Needs work | Poor |
|---|---|---|---|
| **LCP** (Largest Contentful Paint) | ≤2.5 s | ≤4 s | >4 s |
| **INP** (Interaction to Next Paint) | ≤200 ms | ≤500 ms | >500 ms |
| **CLS** (Cumulative Layout Shift) | ≤0.1 | ≤0.25 | >0.25 |
**Design implications:** LCP is usually the hero image or headline — preload it, don't lazy-load it, and don't gate it behind JS. INP is hurt by heavy main-thread JS — ship less. CLS is caused by unsized media, injected banners, and late web fonts — reserve space and match font metrics.

### Principle: Asset Budgets
**Source:** web.dev performance budgets; Addy Osmani, "The Cost of JavaScript."
**Rule:** Per page, on a mid-tier mobile / 4G target:
- Hero image ≤200 KB; other images ≤150 KB each; serve AVIF/WebP with `srcset`/`sizes`.
- Total JS ≤300 KB gzip (ideally ≪); defer/async non-critical scripts; no render-blocking third-party tags.
- Fonts: ≤2 families, woff2, subset, `preload` critical + `font-display: swap`.
- Total transfer target ≤1–1.5 MB for a marketing page.
**Codifiable:** every `<img>` has `width`+`height` (or `aspect-ratio`), `loading="lazy"` below the fold + `fetchpriority="high"` on the LCP image, `decoding="async"`.

### Principle: Critical Rendering Path
**Source:** web.dev; Ilya Grigorik, *High Performance Browser Networking*.
**Rule:** Inline critical CSS for above-the-fold; defer the rest. `preconnect` to required origins (fonts, CDN). Avoid layout-triggering work on load. Prefer static HTML / server rendering for content pages; hydrate only what needs interactivity (islands). A page that renders meaningful content without JS is faster and more resilient.

---

## Section 11: Accessibility (WCAG 2.2, operational)

### Principle: Semantic Structure & Landmarks
**Source:** WCAG 2.2 §1.3.1; WAI-ARIA Authoring Practices; MDN.
**Rule:** Use real elements: `<header> <nav> <main> <aside> <footer>`, `<button>` for actions, `<a>` for navigation (never a `<div>` with an onclick as a button). Exactly one `<h1>` per page; headings nest without skipping levels; lists are `<ul>/<ol>`; landmarks let screen-reader users jump.
**Codifiable:** one `<h1>`; no heading level skipped; interactive controls are native elements or have correct `role` + keyboard handlers.

### Principle: Names, Roles, Values (ARIA only when needed)
**Source:** WAI-ARIA; "No ARIA is better than bad ARIA."
**Rule:** Prefer native HTML semantics; add ARIA only to fill gaps. Every control has an accessible name (visible label, `aria-label`, or `aria-labelledby`). Custom widgets implement the ARIA pattern *and* its keyboard interactions (menu, dialog, tabs, combobox). Icon-only buttons get an `aria-label`.
**Codifiable:** no interactive element has an empty accessible name; modals use `role="dialog"` + `aria-modal="true"` + focus trap + Esc-to-close + focus return.

### Principle: Live Regions & Dynamic Content
**Source:** WCAG §4.1.3 (Status Messages); ARIA live.
**Rule:** Content that appears without a page reload (toasts, form errors, cart count, search results count) is announced via `aria-live="polite"` (or `assertive` for errors) so non-visual users know it changed.

### Principle: Reduced Motion, Contrast, Zoom, Reflow
**Source:** WCAG 2.2 §1.4.4, §1.4.10, §1.4.12, §2.3.3.
**Rule:** Text scales to 200% without loss (no fixed px on type that ignores zoom — use rem). Content reflows at 320 px / 400% zoom with no two-axis scroll. Respect reduced-motion. Meet text-spacing overrides (§1.4.12) without clipping.

---

## Section 12: Semantic HTML, SEO & Social

### Principle: The Document Head Contract
**Source:** Google Search Central; Open Graph protocol; Twitter/X Cards.
**Rule:** Every page ships:
- `<title>` ≤60 characters, unique, primary-keyword-first.
- `<meta name="description">` ≤155 characters (compelling, not keyword soup).
- Canonical URL, `lang` on `<html>`, `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- Open Graph: `og:title`, `og:description`, `og:image` (1200×630, <5 MB), `og:type`, `og:url`; Twitter card tags.
- `theme-color`, full favicon set (ICO + PNG + Apple touch + maskable).
**Codifiable:** a page is "not done" until it renders a correct link preview when pasted into Slack/iMessage/X.

### Principle: Structured Data
**Source:** schema.org; Google rich-results guidelines.
**Rule:** Add JSON-LD for the page's primary entity: `Organization`/`WebSite` on the home page, `Product` + `Offer` + `AggregateRating` on product pages, `Article` on posts, `BreadcrumbList` for depth, `FAQPage` for FAQs. Structured data drives rich results and is a low-cost, high-leverage add.

### Principle: Crawlable, Indexable, Shareable
**Source:** Google Search Central; Core Web Vitals as a ranking signal.
**Rule:** Meaningful content in the initial HTML (don't hide the value prop behind client-only JS); descriptive `alt` on informative images (empty `alt=""` on decorative ones); semantic headings; a sitemap and sensible `robots`. Mobile-friendliness and CWV are ranking inputs — the performance and responsive rules above *are* SEO.

---

## Section 13: Resolved Contradictions

| Conflict | Resolution |
|---|---|
| **Rich, animated, "premium" feel** vs. **performance budget** | Budget wins by default. Achieve premium with type, spacing, and one or two considered motions — not heavy libraries. Animate `transform`/`opacity`; lazy-load below-fold; never ship 500 KB of JS for a marketing page. |
| **Brand accent everywhere** vs. **60-30-10 / single-accent** | Accent stays scarce (≤10%) so CTAs mean something. Use brand-derived neutrals for surfaces; reserve full-saturation brand for action. |
| **Brand color** vs. **WCAG contrast** | WCAG wins for text and focus. Preserve the exact brand hue for large non-text/brand moments; use a contrast-corrected shade (same hue, adjusted L in OKLCH) for text and UI. |
| **Conversion urgency** vs. **ethical design** | No dark patterns. Reduce genuine friction (fewer fields, guest checkout); any scarcity must be real. Deceptive patterns are brand-toxic and increasingly illegal (FTC, EU DSA). |
| **Designer's fixed-pixel comp** vs. **fluid/zoomable web** | The web is fluid by default; a pixel-perfect desktop comp is a suggestion, not a spec. Use rem + clamp + intrinsic layout so it survives zoom, translation, and widths nobody tested. |
| **Placeholder-as-label (clean look)** vs. **usability/a11y** | Persistent labels win. Floating labels are an acceptable compromise; placeholder-only is a defect. |
| **Hamburger everywhere (tidy)** vs. **discoverability** | On desktop, show the nav — hiding primary nav behind a hamburger on wide screens measurably reduces engagement. Collapse only when space demands it. |
| **Autoplay hero video (impact)** vs. **motion/perf/a11y** | Muted, short, `prefers-reduced-motion`-aware, and never the LCP-blocking element. Provide a poster; pause control if >5 s. |

---

## Appendix A: Numbers Cheat Sheet

| Category | Variable | Value |
|---|---|---|
| Layout | Test widths | 320, 390, 768, 1024, 1440 px |
| Layout | Default breakpoints | 640 / 768 / 1024 / 1280 px |
| Layout | Page shell max-width | 1200–1440 px |
| Layout | Reflow (WCAG 1.4.10) | no 2-axis scroll at 320 px / 400% zoom |
| Type | Body min | 16 px (inputs 16 px too) |
| Type | Body fluid | clamp(1rem, 0.92rem + 0.4vw, 1.125rem) |
| Type | H1 fluid | clamp(2rem, 1.1rem + 4.5vw, 3.75rem) |
| Type | Measure | 45–75ch (max-width 65ch) |
| Type | Body line-height | ≥1.5 (WCAG 1.4.12) |
| Type | Display line-height | 1.0–1.2 |
| Type | Paragraph spacing | ≥0.75em |
| Type | Families | ≤2, woff2, font-display: swap |
| Type | Default scale ratio | 1.25 (web); 1.333 (marketing) |
| Spacing | 8-pt scale | 4, 8, 12, 16, 24, 32, 48, 64, 96, 128 |
| Spacing | Related / unrelated gap | ≤16 px / ≥48 px |
| Spacing | Section padding (y) | clamp(48px, 6vw, 128px) |
| Grid | Columns / gap | 12 / clamp(16px, 2vw, 32px) |
| Color | Split | 60-30-10 |
| Color | Accent coverage | ≤10% |
| Color | Body contrast (AA / AAA) | 4.5:1 / 7:1 |
| Color | Large text (AA / AAA) | 3:1 / 4.5:1 |
| Color | UI / focus / icons (SC 1.4.11) | ≥3:1 |
| Color | Ramp space | OKLCH, 12 steps |
| Touch | Target size | ≥44×44 px, ≥8 px apart |
| States | Per interactive element | default / hover / focus-visible / active / disabled |
| States | Focus ring | ≥2 px, ≥3:1 contrast |
| Motion | UI transition | 150–300 ms |
| Motion | Section reveal | ≤500 ms |
| Motion | Flashes/sec max | <3 |
| Motion | Animate only | transform, opacity |
| Perf | LCP / INP / CLS | <2.5 s / <200 ms / <0.1 |
| Perf | Hero image | ≤200 KB (AVIF/WebP) |
| Perf | Total JS | ≤300 KB gzip |
| Perf | Total transfer (marketing) | ≤1–1.5 MB |
| Conversion | Primary CTAs per viewport | ≤1 |
| Conversion | Pricing tiers visible | 3 (middle default), ≤4 |
| Conversion | "How it works" steps | 3 |
| Forms | Layout | single column |
| Forms | Labels | persistent, visible, associated |
| Forms | Validation | on blur, inline, adjacent, preserves input |
| Forms | Fields | fewest that do the job |
| Nav | Top-level items | ≤7 |
| Nav | Depth to any page | ≤3 clicks |
| Nav | Sticky header height | ≤10–12% viewport |
| SEO | `<title>` / description | ≤60ch / ≤155ch |
| SEO | OG image | 1200×630 |
| A11y | `<h1>` per page | exactly 1 |
| A11y | Text zoom | 200% no loss |
| A11y | Standard | WCAG 2.2 AA (floor) |

---

## Appendix B: Sources

**Foundational books**
- Ethan Marcotte — *Responsive Web Design* (2010, 2nd ed. 2014).
- Luke Wroblewski — *Mobile First* (2011).
- Brad Frost — *Atomic Design* (2016).
- Steve Krug — *Don't Make Me Think* (2000, rev. 2014).
- Robert Bringhurst — *The Elements of Typographic Style* (1992, 2019).
- Matthew Butterick — *Practical Typography* (practicaltypography.com).
- Josef Müller-Brockmann — *Grid Systems in Graphic Design* (1981).
- Adam Wathan & Steve Schoger — *Refactoring UI* (2018).
- Louis Rosenfeld & Peter Morville — *Information Architecture for the World Wide Web* (4th ed. 2015).
- Robert Cialdini — *Influence* (1984, rev. 2021).
- Ilya Grigorik — *High Performance Browser Networking* (2013).
- Heydon Pickering & Andy Bell — *Every Layout* (every-layout.dev).

**Standards & guidelines**
- W3C — WCAG 2.2 (2023): w3.org/TR/WCAG22 (esp. 1.4.1, 1.4.3, 1.4.4, 1.4.10, 1.4.11, 1.4.12, 2.1.1, 2.2.2, 2.3.1, 2.3.3, 2.4.1, 2.4.11, 2.4.13, 2.5.8, 3.3, 4.1.3).
- W3C — Design Tokens Community Group: w3.org/community/design-tokens.
- W3C — WAI-ARIA Authoring Practices Guide: w3.org/WAI/ARIA/apg.
- Apple — Human Interface Guidelines: developer.apple.com/design/human-interface-guidelines.
- Google — Material Design 3: m3.material.io.
- Google — web.dev Core Web Vitals & Search Central: web.dev/vitals, developers.google.com/search.
- Open Graph protocol: ogp.me · schema.org.

**Research, articles & tools**
- Nielsen Norman Group — F-Pattern (2006, 2017, 2023); response-time limits; form usability; sticky-nav studies.
- Baymard Institute — checkout & form UX research (baymard.com).
- Björn Ottosson — "OKLab / OKLCH" (2020); Lea Verou — LCH/OKLCH color.
- Trys Mudford & James Gilyead — Utopia fluid type & space (utopia.fyi).
- Bryn Jackson — "The 8-Point Grid" (Spec FM, 2015).
- Zach Leatherman — "A Comprehensive Guide to Font Loading Strategies."
- Addy Osmani — "The Cost of JavaScript."
- Jen Simmons — "Intrinsic Web Design" (2018).
- Cynthia Brewer — ColorBrewer (colorbrewer2.org).
- Julian Shapiro — "How to build a high-converting landing page."

---

*End of report. 13 sections, 20-rule cheat sheet, ~90 numeric values in Appendix A. The web sibling of `design-principles.md` — same rigor, four new questions: does it hold up fluid, is it fast, can everyone use it, does it convert.*
