# AI Forte Asset Generation Plan

**Model:** `google/gemini-3-pro-image-preview` via OpenRouter
**Skill:** `nano-banana-pro-openrouter`
**Palette:** A — Warm Premium (locked)
**Date:** 2026-04-14

## Palette reference (repeated in every prompt)

| Role | Hex | Name |
|------|-----|------|
| Background | `#F8F3EC` | Warm cream |
| Foreground | `#2C1810` | Deep espresso |
| Accent | `#C65D2E` | Burnt sienna |
| Muted | `#8B7355` | Warm taupe |
| Border | `#E8DDD0` | Cream border |

## Brand archetypes (referenced in prompts)

- Kinfolk magazine editorial layouts
- Aesop brand identity materials
- Wallpaper* magazine design features
- Ueno / Huge / Instrument agency brand books

## The 9 Assets

| # | Asset | Filename | Resolution | Aspect (described in prompt) |
|---|-------|----------|-----------|------------------------------|
| 1 | Primary logo (wordmark + icon lockup) | `resources/logo/ai-forte-logo.png` | 2K | 4:1 wide horizontal |
| 2 | Icon only (favicon / profile pic) | `resources/logo/ai-forte-icon.png` | 1K | 1:1 square |
| 3 | LinkedIn cover banner | `resources/linkedin/ai-forte-linkedin-banner.png` | 2K | 4:1 wide |
| 4 | Website OG image | `resources/og/ai-forte-og-image.png` | 1K | 16:9 widescreen |
| 5 | Social post template (reusable) | `resources/social/ai-forte-post-template.png` | 1K | 1:1 square |
| 6 | Summit announcement post | `resources/social/ai-forte-summit-announcement.png` | 1K | 16:9 widescreen |
| 7 | Digital business card cover | `resources/business-card/ai-forte-business-card.png` | 1K | 9:16 portrait |
| 8 | One-pager PDF header | `resources/one-pager/ai-forte-one-pager-header.png` | 2K | 3:1 wide banner |
| 9 | Headshot (background replacement) | `resources/headshot/ashish-headshot-warm.png` | 1K | 4:5 portrait, uses `ashish-pic.JPG` as input |

## Prompts

Each prompt follows the 5-component formula (Subject → Action → Context → Composition → Style) and locks the exact hex colors in the palette.

---

### 1. Primary Logo

```
A minimalist horizontal logo lockup for the brand "AI Forte," an AI orchestrator
agency. Wide 4:1 horizontal banner composition on warm cream paper background
hex #F8F3EC with subtle visible paper grain texture.

Left side: a precise geometric icon rendered in burnt sienna hex #C65D2E — four
small circular nodes connected by thin hairline curves forming an asymmetric
orchestration network pattern. The central node is slightly larger than the
satellites. Clean, mathematically balanced, no gradients, no glow.

Right side: the wordmark "AI Forte" in a bold condensed geometric sans-serif,
tightly tracked, the "AI" rendered in burnt sienna hex #C65D2E and "Forte"
rendered in deep espresso hex #2C1810. High letter-pressed crispness, modern
but classic proportions.

Generous whitespace around all elements. No background decoration. No
gradients. No 3D. No glow effects. No drop shadows. No additional text, logos,
or icons beyond the single icon-and-wordmark lockup.

Editorial brand identity style reminiscent of Kinfolk magazine mastheads,
Aesop brand identity materials, and Wallpaper magazine design editorial.
Commercial brand book photography, flat color, print-ready.
```

---

### 2. Icon Only (Favicon / Profile Picture)

```
A minimalist square icon mark for the brand "AI Forte," an AI orchestrator
agency. Perfect 1:1 square composition on warm cream paper background hex
#F8F3EC with subtle visible paper grain.

The icon is a precise geometric orchestration network: one slightly larger
central circular node surrounded by four smaller satellite nodes, all connected
by thin hairline curves forming an asymmetric but balanced composition. The
central node is rendered in deep espresso hex #2C1810 with a small inner core
in burnt sienna hex #C65D2E. Satellite nodes and all connecting curves are
rendered in burnt sienna hex #C65D2E, with satellite nodes at varying opacity
(0.5 to 0.9) to suggest depth.

Centered in the square with generous margin on all sides. The icon occupies
the center 60 percent of the composition.

NEVER include any text, letters, words, labels, or decorative elements. NEVER
include gradients, glow, drop shadows, or 3D effects.

Editorial brand mark style reminiscent of Aesop brand identity, Kinfolk
magazine design, and Wallpaper magazine brand marks. Flat color, print-ready,
suitable for use as a favicon, app icon, profile picture, or small accent.
```

---

### 3. LinkedIn Cover Banner

```
A professional LinkedIn cover banner for the founder of "AI Forte," an AI
orchestrator agency. Wide 4:1 horizontal banner composition, landscape
orientation. Warm cream paper background hex #F8F3EC with subtle visible paper
grain and natural fiber texture.

Left 60 percent of the composition: bold headline text rendered in deep
espresso hex #2C1810 reading "Orchestrating AI Agents" on the first line and
"on Adobe Experience Cloud" on the second line, set in a bold condensed
geometric sans-serif with tight letter-spacing. Below the headline, a smaller
subheading in warm taupe hex #8B7355 reading "AI Forte — Commerce, Marketo,
AEM, Agent Orchestrator" in a smaller regular-weight sans-serif.

Right 40 percent of the composition: a precise geometric orchestration diagram
rendered in burnt sienna hex #C65D2E — one central node with four or five
satellite nodes connected by thin hairline curves, arranged in an asymmetric
balanced pattern. Central node is filled deep espresso hex #2C1810 with a
small sienna inner core. All connections are thin hairlines.

Leave clear negative space around the center-left area for a LinkedIn profile
photo circle overlay (approximately 200 pixels from left edge, vertically
centered in the banner).

Generous whitespace. No gradients. No glow. No drop shadows. No 3D. No stock
photography. No additional icons or text beyond the headline, subheading, and
network diagram.

Editorial magazine aesthetic reminiscent of Kinfolk magazine cover layouts,
Aesop brand identity, and Wallpaper magazine editorial spreads. Print-ready
flat color, confident and warm.
```

---

### 4. Website OG Image (Open Graph / social preview)

```
A social media link preview image for the brand "AI Forte," an AI orchestrator
agency. Standard widescreen 16:9 composition, landscape orientation. Warm cream
paper background hex #F8F3EC with subtle visible paper grain.

Centered composition: at the top, a small precise orchestration icon in burnt
sienna hex #C65D2E consisting of four nodes connected by thin hairline curves.
Below the icon, the wordmark "AI Forte" in bold condensed geometric sans-serif,
the "AI" rendered in burnt sienna hex #C65D2E and "Forte" rendered in deep
espresso hex #2C1810.

Below the wordmark, a bold display headline in deep espresso hex #2C1810
reading "AI Agent Orchestration" on one line and "on Adobe Experience Cloud"
on a second line, set in a bold geometric sans-serif with tight letter-spacing.

Below the headline, a smaller tagline in warm taupe hex #8B7355 reading
"Commerce • Marketo • AEM • Agent Orchestrator".

Generous whitespace on all sides. No borders, no decorative frames, no
gradients, no glow, no 3D. Flat color, print-ready.

Editorial brand card aesthetic reminiscent of Wallpaper magazine brand pages,
Kinfolk magazine editorial features, and Aesop brand materials. Social media
link preview format, optimized for LinkedIn and Twitter.
```

---

### 5. Social Post Template (Reusable Background)

```
A reusable square social media post template background for the brand
"AI Forte," an AI orchestrator agency. Perfect 1:1 square composition.
Warm cream paper background hex #F8F3EC with subtle visible paper grain and
natural fiber texture.

Composition: a very subtle decorative frame around the edges — a thin hairline
border in cream border tone hex #E8DDD0 with small geometric corner accents
in burnt sienna hex #C65D2E. Corners feature tiny network node motifs (small
circles connected by hairlines) in sienna.

Bottom center area: a small "AI Forte" wordmark in deep espresso hex #2C1810
with the "AI" in burnt sienna hex #C65D2E, in a bold condensed geometric
sans-serif.

Center of the image: clean empty negative space suitable for overlaying
headline text and graphics in post-production. No decorative elements in the
center.

NEVER include any body text, headlines, or filler words in the center space.
The center must remain clean for text overlay. No gradients. No glow. No 3D.
No stock photography.

Editorial brand card aesthetic reminiscent of Kinfolk magazine article
openers, Aesop brand materials, and Wallpaper magazine editorial frames.
Print-ready flat color, template-ready with clean empty center.
```

---

### 6. Summit Announcement Post

```
A LinkedIn announcement post image for the brand "AI Forte" announcing
attendance at Adobe Summit 2026. Standard widescreen 16:9 composition,
landscape orientation. Warm cream paper background hex #F8F3EC with subtle
visible paper grain and natural fiber texture.

Left side of the composition: a small date badge consisting of "April 19-22,
2026" in burnt sienna hex #C65D2E within a thin hairline cream border pill
shape. Below the badge, a bold display headline in deep espresso hex #2C1810
reading "See you in Las Vegas." on the first line. Below the headline, a
smaller subheading in warm taupe hex #8B7355 reading "Let's talk agent
orchestration at Adobe Summit 2026."

Right side of the composition: a precise geometric orchestration diagram in
burnt sienna hex #C65D2E — one larger central node with four satellite nodes
connected by thin hairline curves in an asymmetric balanced pattern. Central
node filled deep espresso.

Bottom right corner: small "AI Forte" wordmark in deep espresso hex #2C1810
with "AI" in burnt sienna hex #C65D2E.

Generous whitespace. No gradients. No glow. No 3D. No stock photography of
Las Vegas or conferences.

Editorial magazine cover aesthetic reminiscent of Kinfolk magazine event
announcements, Aesop brand materials, and Wallpaper magazine editorial
spreads. Print-ready flat color.
```

---

### 7. Digital Business Card Cover

```
A premium portrait-orientation cover image for a digital business card on
Blinq or Popl for the founder of "AI Forte," an AI orchestrator agency.
Portrait 9:16 vertical composition, taller than wide. Warm cream paper
background hex #F8F3EC with subtle visible paper grain.

Top 30 percent of the composition: a large "AI Forte" wordmark in bold
condensed geometric sans-serif, the "AI" rendered in burnt sienna hex #C65D2E
and "Forte" rendered in deep espresso hex #2C1810. Below the wordmark, a
thin hairline divider in burnt sienna hex #C65D2E.

Middle 40 percent: a precise geometric orchestration diagram centered in the
composition, rendered in burnt sienna hex #C65D2E. One central node (deep
espresso filled with a small sienna inner core) surrounded by four satellite
nodes connected by thin hairline curves. Network occupies the middle band of
the composition.

Bottom 30 percent: clean empty negative space for overlaying contact details
(name, title, email) in post-production.

NEVER include names, emails, phone numbers, URLs, or contact details in the
generated image. The bottom area must remain empty for overlay.

Generous whitespace. No gradients. No glow. No 3D. No decorative borders
beyond the thin divider.

Editorial brand card aesthetic reminiscent of Aesop brand identity, Kinfolk
magazine profile layouts, and Wallpaper magazine editorial portraits.
Print-ready flat color, premium calling card feel.
```

---

### 8. One-Pager PDF Header Banner

```
A horizontal hero banner image for the top of a B2B agency one-pager PDF
titled "AI Forte — The AI Orchestrator Agency for Adobe Experience Cloud."
Wide 3:1 horizontal banner composition, landscape orientation. Warm cream
paper background hex #F8F3EC with subtle visible paper grain and natural
fiber texture.

Left 65 percent of the composition: bold display headline in deep espresso
hex #2C1810 reading "AI Agent Orchestration" on the first line and "on Adobe
Experience Cloud" on the second line, set in a bold condensed geometric
sans-serif with tight letter-spacing and modern proportions. Below the
headline, a smaller subheading in warm taupe hex #8B7355 reading "The craft
behind multi-agent systems that actually ship."

Right 35 percent of the composition: a precise geometric orchestration
diagram rendered in burnt sienna hex #C65D2E — one central node in deep
espresso with a sienna inner core, surrounded by five satellite nodes at
varying sizes connected by thin hairline curves. Composition is asymmetric
but balanced, occupying the right third of the banner.

Generous whitespace. No gradients. No glow. No drop shadows. No 3D.
No stock photography. No decorative borders or frames.

Editorial magazine cover aesthetic reminiscent of Wallpaper magazine feature
spreads, Kinfolk magazine article openers, and Aesop brand identity materials.
Print-ready flat color, magazine-grade typography, suitable for A4 or letter
size printing.
```

---

### 9. Headshot Background Replacement

```
Edit this photo of a man in his 30s wearing a white t-shirt standing in front
of a bridge. Replace the entire background with a clean warm cream paper
backdrop in warm cream hex #F8F3EC. The new background should have subtle
visible paper grain texture and very soft natural daylight directional
lighting from the upper left.

Keep all facial features, expression, skin tone, hair, sunglasses, t-shirt,
and body position completely unchanged. Preserve the original subject exactly.
Add a very subtle warm rim light on the shoulders consistent with the cream
backdrop lighting direction.

Crop to a comfortable head-and-shoulders professional portrait composition,
4:5 portrait aspect ratio, centered on the subject.

Editorial professional headshot style, warm and confident, reminiscent of
Kinfolk magazine founder portraits and Wallpaper magazine executive profile
photography. Clean, sharp, print-ready, high fidelity to the original subject.

NEVER alter the subject's face, expression, clothing, or body position.
NEVER add any text, logos, borders, or decorative elements to the image.
```

---

## Execution order

1. Run the simple ones first (logo lockup, icon, headshot edit) — these are
   compositionally straightforward and will verify the pipeline
2. Then the wide banners (LinkedIn banner, one-pager header, Summit announcement)
3. Then the template-style posts (OG image, social post template, business card)

If any generation fails or looks wrong, iterate on that specific prompt rather
than regenerating everything.

## Cost estimate

9 images at 1K-2K via OpenRouter Gemini 3 Pro Image Preview: approximately $0.50-$1.50 total.
