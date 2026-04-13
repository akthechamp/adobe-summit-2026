# Palette Decision — AI Forte Brand Direction

**Date:** 2026-04-14
**Status:** LOCKED — Palette A (Warm Premium)
**Decided by:** Ashish Kumar
**Context:** Adobe Summit 2026 prep, AI Forte brand launch

---

## The Decision

**Primary palette: Option A — Warm Premium**

| Role | Hex | Name |
|------|-----|------|
| Background (primary) | `#F8F3EC` | Warm cream |
| Foreground text | `#2C1810` | Deep espresso |
| Primary accent | `#C65D2E` | Burnt sienna |
| Muted / secondary text | `#8B7355` | Warm taupe |
| Border / subtle surface | `#E8DDD0` | Cream border |

**Secondary note — hybrid treatment for digital-only surfaces:**
Palette E (Aurora Glass) is kept as a **tactical flourish** for digital-only moments — specifically for 3D isometric illustrations on the astro-site hero section. The A palette wraps the full brand identity (business card, one-pager, LinkedIn, Summit collateral, print) and E appears only in a single digital showcase moment if it makes sense. This is an escape hatch, not a commitment.

---

## Options Considered

Five palette directions were explored via a side-by-side HTML preview ([`preview.html`](./preview.html)) that rendered the same AI Forte mockup (wordmark, Summit badge, headline, CTA buttons, card component, stats row, typography sample) in each palette:

| Option | Name | Archetype References | Verdict |
|--------|------|---------------------|---------|
| **A** | Warm Premium | Kinfolk, Aesop, Ueno, Huge | ✅ **LOCKED** |
| B | Monochrome + Signal Green | Linear, Vercel, Anthropic, Palantir | Rejected |
| C | Adobe-Adjacent | Architectural Digest + Adobe cues | Rejected |
| D | Graphite + Acid Lime | Figma dark, Raycast, Arc browser | Rejected |
| E | Aurora Glass | Linear, Framer, Apple Vision Pro | Rejected as primary (retained as hybrid flourish) |

---

## Decision Criteria

Five axes were evaluated:

### 1. Sea-of-sameness test
Walking the Venetian on Day 1, 200+ booths will be dark backgrounds with neon/violet accents — the default visual language of every AI startup in 2026.
- **A wins.** A warm palette is the one visually distinct brand on the floor. Eyes go to it. A prospect pauses. That 2-second pause is what collateral exists for.
- **E, B, D lose.** Indistinguishable from 80% of booths at 3-second scan distance.

### 2. Adobe theme alignment
Summit 2026's entire narrative is agentic AI. Adobe is pushing Agent Orchestrator, Brand Concierge, Agentic Web.
- **E wins here.** Visually harmonizes with Adobe's marketing.
- **A loses here.** Deliberately clashes with the mothership.
- **Weight:** Lower than sea-of-sameness, because clashing is memorable; harmonizing is invisible.

### 3. Audience psychology (SMB/mid-market buyers)
Real prospects at Summit are marketing ops leaders, VP growth, ecommerce directors, CMOs — not designers, not Linear power users.
- **A wins.** Warm premium = "craftspeople, boutique consultancy, lower-risk" → predisposes trust.
- **E, B, D lose.** Dark + neon = "another AI startup, higher-risk, probably VC-funded and not my vendor" → predisposes skepticism.
- **Mid-market buyers are risk-averse.** Warm reads lower-risk. This is the biggest weight in the decision.

### 4. Asset durability (across 9 final deliverables)

| Asset | A | E |
|-------|---|---|
| Business card (print CMYK) | ✅ Flat colors print perfectly | ❌ Gradients + glow don't survive CMYK |
| One-pager PDF | ✅ Editorial, print-ready | ❌ Glass depth lost in print |
| LinkedIn banner (digital) | ✅ Distinctive in feed scroll | ⚠️ Blends with tech banners |
| Digital business card | ✅ Strong | ✅ Strong |
| Astro-site (web-only) | ✅ Works | ✅ Arguably better for web |
| Isometric/3D renders | ⚠️ Sepia-metal 3D is possible but less trend-aligned | ✅ Violet/mint 3D is peak 2026 |

A wins or ties 5/6 categories. A loses only on the isometric/3D aesthetic — which is addressed via the hybrid escape hatch.

### 5. Memorability after 3 days
After 3 days of staring at dark UIs under Vegas LED lighting, which brand is remembered?
- **A wins.** The one warm brand in a sea of dark sticks in memory.

---

## What We Gave Up

By choosing A, we explicitly walk away from:

1. **The "cutting-edge agent-native" visual signal** — E reads as future-forward, A reads as classic-premium.
2. **Peak-2026 trend alignment** — E is what every design-literate founder recognizes as "on-trend."
3. **Beautiful violet/mint isometric 3D renders** — the standard "agentic AI marketing" aesthetic.
4. **Harmony with Adobe's own brand energy** — E plays well with Adobe's own 2026 materials.

**Mitigation:** The hybrid note above — E is retained as a tactical flourish for digital-only 3D illustration moments on the astro-site. If it makes sense for one hero illustration, use it. If not, don't force it.

---

## Why Not The Others (B, C, D)

- **B — Monochrome + Signal Green.** Cleanest minimalism of all five, but the sea-of-sameness problem is worse than E. Green-on-black is very 2023 crypto/dev startup. Risks "we're just another dev tool."
- **C — Adobe-Adjacent.** Echoing Adobe's red is a double-edged sword — too much and it looks like we're impersonating Adobe. Rejected as too risky for a brand that's not actually part of Adobe.
- **D — Graphite + Acid Lime.** Same dark + neon trap as B and E, with an accent color (acid lime) that reads as "developer tool" more than "consultancy." Niche audience fit.

---

## Supporting Files

All preserved in this directory:

| File | Purpose |
|------|---------|
| `preview.html` | Live side-by-side preview of all 5 palettes in the same AI Forte mockup — open in browser to re-verify the decision anytime |
| `README.md` | Original instructions for generating samples (now historical — decision is made) |
| `prompt-a-warm-premium.txt` | Gemini prompt for A (unused in final decision but kept as reference for future asset generation) |
| `prompt-b-monochrome-green.txt` | Gemini prompt for B |
| `prompt-c-adobe-adjacent.txt` | Gemini prompt for C |
| `prompt-d-graphite-lime.txt` | Gemini prompt for D |
| `DECISION.md` | This file |

---

## Next Steps

1. Lock palette A in the brand system documentation
2. Update the existing resources (`resources/logo/`, `resources/linkedin/`, etc.) to use A's palette
3. Generate the 9 final brand assets in palette A:
   - Logo (primary wordmark + icon-only)
   - LinkedIn banner (1584×396)
   - OG image for astro-site (1200×630)
   - Social post template (1080×1080)
   - Summit announcement post (1200×628)
   - Digital business card cover (1080×1920)
   - One-pager PDF header (1920×640) — or full print-ready one-pager
   - Headshot background replacement (from `ashish-pic.JPG`)
4. Update `astro-site/` theme colors to match palette A
5. Consider whether the hybrid E flourish makes sense for one astro-site hero illustration — defer decision until that section is being built
