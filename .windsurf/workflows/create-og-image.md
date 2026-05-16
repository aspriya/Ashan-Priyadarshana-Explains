---
description: Design and ship a beautiful 1200x630 OG image so a lesson HTML previews nicely when shared on WhatsApp, Facebook, LinkedIn, Twitter, etc.
---

# Create OG Image

Use this workflow when the user asks for an OG / social-share / "WhatsApp preview" image for a page. The goal is a designer-quality 1200x630 PNG plus the meta tags that wire it into the page. Follow every step in order. Skip nothing.

## 0. Gather context

Before designing anything, read these so the image carries the same DNA as the page:

1. The target HTML file the user mentioned. Find its `<title>`, primary headline (`h1`, `.display`, cover slide, etc.), tagline / subhead, eyebrow text, presenter name, and any pill / chip / tag words.
2. The CSS variables / palette in the page's `<style>` block. Copy the exact hex values for background, ink, accents, and any role-coded colors. **Do not invent colors** — reuse the page's own palette so the image feels like the page.
3. The font stack. Note display font (often a serif like Fraunces, Georgia, Playfair) and the mono font (JetBrains Mono, Fira Code, etc.). Use these in the SVG so the image breathes the same typography.
4. Any reference OG image already in the repo (e.g. `STEMLink Day 1/generate-og-image.html`). If one exists, mirror its structure — it represents the established visual system.

## 1. Confirm the public URL with the user

You need an absolute URL for `og:image` — relative paths do not work for social crawlers. Ask the user (or infer from the user's hosting pattern, usually GitHub Pages) **where this page will live publicly**. The answer determines both the `og:url` and `og:image` URLs you'll embed.

Common pattern for this workspace:
- `https://aspriya.github.io/<repo>/<path>/<page>.html`

## 2. Design the SVG (1200x630)

Constraints that always apply:

- Exact dimensions: `1200 x 630` (Facebook / WhatsApp / LinkedIn standard).
- Two-zone layout: **left = words**, **right = visual**. Roughly 60/40 or 65/35 split. Never center everything — social cards read left-to-right and need a clear hierarchy.
- Left zone must contain, top to bottom:
  1. A small uppercase mono eyebrow in the brand accent color (e.g. `CODEV LABS · STEMLINK · MODULE 01`).
  2. A two-line display title in the page's serif. Make the second half *italic* and gradient-filled with the brand accent. Aim for 70–90 px font size; tighten letter-spacing (-1 to -2).
  3. A one- or two-line description in a muted ink color (`#b8ad94`-ish). Keep it under 22 words. Italicize the second half for poetry.
  4. A row of 3–5 pill-shaped tags using the page's accent colors with 13–14% alpha fills and ~55% alpha strokes. Each pill labels a key concept from the page.
  5. A subtle divider line at very low opacity (~0.08).
  6. `PRESENTED BY` mono eyebrow + presenter's full name in serif.
- Right zone holds a **single conceptual diagram** that maps to the lesson's core idea. Don't just paste a generic graphic — invent something that telegraphs *what the page is about*. Examples:
  - Multi-agent / Mafia → a ring of 8 colored agent nodes with connection lines, hidden roles encoded by color, a "village" core in the middle.
  - SDLC / AI tooling → a horizontal gradient spectrum with labeled stations.
  - Neural networks → layered nodes with weighted edges, gradient-filled.
  - Solar / energy → sun → panel → grid flow with arrows.
  Whatever you build, keep the same color palette and use ~20-24px circle nodes with a 3px stroke in the page bg color so they pop.
- Background must be the page's own bg (`#0e0d0b`, `#0b0f14`, etc.), with:
  - A diagonal gradient on the bg color (3 stops, edges darker, center slightly lighter).
  - Two radial glows in the brand accents, low opacity (~0.12–0.18), positioned diagonally opposite.
  - A subtle dot grain `<pattern>` overlay at ~0.025 opacity for texture.
- A 5–6 px vertical accent bar at `x=0` in the primary brand color — the "spine" of the card.
- Channel branding bottom-right: italic mono "Ashan Priyadarshana Explains" (or whatever the channel signature is) in muted ink.

Save the SVG into a wrapper HTML file as `generate-og-image.html` in the same directory as the target page. The wrapper:

```html
<!DOCTYPE html>
<html lang="en"><head>
<meta charset="UTF-8">
<title>Generate OG image — <page name></title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="<google fonts url matching the page>" rel="stylesheet">
<style>
  html, body { margin: 0; padding: 0; background: <page bg hex>; }
  body { width: 1200px; height: 630px; overflow: hidden; }
  svg { display: block; width: 1200px; height: 630px; }
</style>
</head><body>
<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="630" viewBox="0 0 1200 630">
  ... your design ...
</svg>
</body></html>
```

Also write a standalone `og-image.svg` next to it (same SVG, with an `@import` of the Google Fonts inside a `<defs><style>` block) — this is the editable source of truth, even if the PNG is what crawlers fetch.

## 3. Render the SVG to PNG via headless Chrome

// turbo
```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new \
  --disable-gpu \
  --hide-scrollbars \
  --no-sandbox \
  --default-background-color=00000000 \
  --window-size=1200,630 \
  --virtual-time-budget=4000 \
  --screenshot="<absolute-path>/og-image.png" \
  "file://<absolute-path>/generate-og-image.html"
```

The `--virtual-time-budget=4000` gives Google Fonts time to load before the screenshot. Then verify:

// turbo
```bash
file "<absolute-path>/og-image.png"
# Must report: PNG image data, 1200 x 630
```

## 4. Visually inspect the PNG

Read the PNG file back with the read_file tool so you can actually see the rendered image. Check for:

- Text overflow (no clipped letters at the right edge).
- Title fits on its line (Fraunces is wide — if it overflows, drop the font-size 5–10 px).
- Right-zone diagram is balanced — not cramped against the edge, not floating.
- Colors look rich, not muddy.
- Pills are aligned (use consistent `y` and incremented `transform="translate(x,y)"`).

If anything is off, edit the SVG in `generate-og-image.html`, re-render, re-inspect. Don't ship the first try blindly.

## 5. Wire the meta tags into the page

Add the following block at the top of the target page's `<head>`, immediately after the `<meta name="viewport">` line. Replace every `<...>` placeholder with the real value. Add a Twitter Card block too — same data, fewer tags.

```html
<meta name="description" content="<one-sentence description, <160 chars>">
<meta name="author" content="<author>">
<meta name="theme-color" content="<page bg hex>">
<link rel="icon" type="image/svg+xml" href="data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'><rect width='64' height='64' rx='12' fill='%23<bg-hex>'/><circle cx='32' cy='32' r='14' fill='%23<accent-hex>'/></svg>">

<!-- Open Graph / Facebook / WhatsApp / LinkedIn -->
<meta property="og:type" content="article">
<meta property="og:site_name" content="<site name>">
<meta property="og:url" content="<absolute page URL>">
<meta property="og:title" content="<title — make it punchy, include the tagline>">
<meta property="og:description" content="<sentence or two, can be slightly longer than meta description>">
<meta property="og:image" content="<absolute og-image.png URL>">
<meta property="og:image:secure_url" content="<absolute og-image.png URL>">
<meta property="og:image:type" content="image/png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="<descriptive alt for the image>">

<!-- Twitter / X -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="<title>">
<meta name="twitter:description" content="<description>">
<meta name="twitter:image" content="<absolute og-image.png URL>">
```

**Critical: URLs must be absolute**, percent-encoded, and `https://`. WhatsApp will not fetch http or relative paths. Spaces in the URL must be `%20`.

If the page exists in multiple copies (e.g. a working source folder and a public-facing folder), update **all of them** with identical tags so previews are consistent regardless of which path someone shares.

## 6. Verify by debugging crawler behavior (optional)

If the page is already live, give the user these debug URLs:

- WhatsApp uses Facebook's crawler. Test with: `https://developers.facebook.com/tools/debug/?q=<encoded page URL>`
- LinkedIn: `https://www.linkedin.com/post-inspector/`
- Twitter / X: `https://cards-dev.twitter.com/validator`

Each tool also offers a "Scrape Again" button to bust the cache after a redesign.

## 7. Commit and push

Stage every artifact created or modified — `og-image.png`, `og-image.svg`, `generate-og-image.html`, and every `*.html` page where you added meta tags. Use a clear commit message:

```
Add OG / social-share image for <page name>

- New 1200x630 og-image.png + svg + generator
- Wired into <page>.html via og:* and twitter:* meta tags
- og:image URL points at <hosting URL>
```

If the user has multiple repos involved (e.g. a `mafia-village` working repo and the main `Ashan-Priyadarshana-Explains` portal repo), commit and push to each separately. Be explicit in chat about which remotes received which commits.

## Design rules to live by

- **Never use stock images.** Build the visual from primitives in the SVG.
- **Never use more than 5 colors total.** The page palette is the palette.
- **Title should fit on two lines max.** If it doesn't, shorten the title — don't shrink it past readability.
- **The image must read at 200x100 px.** WhatsApp shows it tiny in chat — the title needs to be legible even there. Test by squinting at the rendered PNG.
- **The visual must say something specific about the lesson.** A generic geometric pattern is a wasted opportunity.
- **Match the page's mood.** A warm parchment-and-orange deck should not have a cold blue OG card. Steal the page's gradient.
