# Astro Site — Palette A Migration (Single Theme)

> **Status:** Active — supersedes [`2026-04-14-astro-dual-theme.md`](./2026-04-14-astro-dual-theme.md)
> **Strategy:** Multi-agent parallel execution (4 agents on non-overlapping file partitions)

**Goal:** Migrate `astro-site/` from its current dark-violet/space aesthetic to **single-theme Palette A (Warm Premium)** — cream `#F8F3EC`, deep espresso `#2C1810`, burnt sienna `#C65D2E`, warm taupe `#8B7355`, cream border `#E8DDD0`. No dark mode, no theme toggle, no glass morphism. Editorial premium aesthetic throughout.

**Architecture:** Flat repaint of the existing site. Tailwind 4 `@theme` block gets repointed to Palette A hex values. Glass utilities (`.glass`, `.glass-strong`, `.glass-violet`, `.glass-dark`) are converted to flat cream cards with hairline borders. Hero section's animated space scene is removed entirely and replaced with a warm editorial composition. All hardcoded violet/navy hex values across components are replaced with theme tokens.

**Tech Stack:** Astro 5.17, React 19, Tailwind 4, GSAP 3 (animation infrastructure stays), Framer Motion 12

**Logo:** Temporary placeholder using the leading isometric concept (Iso B — Stacked Cantilever) at `astro-site/public/ai-forte-logo-temp.jpg`. To be swapped when the final logo is locked.

---

## File partition (4 parallel agents)

Each agent owns a non-overlapping set of files. No two agents touch the same file. This eliminates merge conflicts.

### Agent A — Style System
**Files:** `astro-site/src/styles/global.css` (only)

Owns the full `@theme` block, glass utilities, gradient utilities, body styles, and selection styles. Repaints the entire token system to Palette A.

### Agent B — Hero Overhaul
**Files:**
- `astro-site/src/components/astro/HeroSection.astro`
- `astro-site/src/components/react/MeshGradientHero.tsx`

Removes the entire animated SVG space scene (planet, rocket, shooting star, HUD circles, glass dashboard cards). Replaces with a clean warm editorial hero: large headline, subhead, two CTA buttons, a small stats row. Removes or repurposes the GSAP timeline. Updates `MeshGradientHero` to either render a flat cream background or be removed entirely.

### Agent C — Component Sweep
**Files:**
- `astro-site/src/components/astro/AboutSection.astro`
- `astro-site/src/components/astro/ServicesSection.astro`
- `astro-site/src/components/astro/HowItWorksSection.astro`
- `astro-site/src/components/astro/CaseStudiesSection.astro`
- `astro-site/src/components/astro/TestimonialsSection.astro`
- `astro-site/src/components/astro/ROISection.astro`
- `astro-site/src/components/astro/FAQSection.astro`
- `astro-site/src/components/astro/ContactSection.astro`
- `astro-site/src/components/astro/TrustedBy.astro`
- `astro-site/src/components/react/FAQAccordion.tsx`
- `astro-site/src/components/react/ChatWidget.tsx`
- `astro-site/src/components/react/StatCounter.tsx`
- `astro-site/src/components/react/ROICalculator.tsx`
- `astro-site/src/components/react/ContactForm.tsx`
- `astro-site/src/components/react/IndustryTabs.tsx`
- `astro-site/src/components/react/MobileMenu.tsx`
- `astro-site/src/components/ui/Button.tsx`
- `astro-site/src/components/ui/Badge.tsx`
- `astro-site/src/components/ui/GlassCard.tsx`

Sweeps every section + React component for hardcoded hex values. Replaces them with Palette A theme tokens (Tailwind utility classes or `var(--color-*)`). Verifies each section reads correctly in cream + sienna + espresso.

### Agent D — Layout, Navbar, Footer, Brand Assets
**Files:**
- `astro-site/src/layouts/BaseLayout.astro`
- `astro-site/src/components/astro/Navbar.astro`
- `astro-site/src/components/astro/Footer.astro`
- `astro-site/public/` (adds new files)

Updates `BaseLayout` meta tags (title template, description, OG image reference, favicon link). Wires the new placeholder logo into Navbar and Footer. Adds the OG image to `public/`. Removes any references to the old dark theme metadata.

---

## Execution sequence

```
Phase 1 (sequential, ~10 min) — done by coordinator before agents:
  1.1 Archive WFT Images, mark dual-theme plan superseded
  1.2 Write this plan
  1.3 Copy Iso B as placeholder logo to astro-site/public/
  1.4 Commit + push to parent repo

Phase 2 (parallel, ~30 min) — 4 agents in one dispatch:
  Agent A — global.css repaint
  Agent B — Hero overhaul
  Agent C — Component sweep
  Agent D — Layout + Navbar + Footer + brand wiring

Phase 3 (sequential, ~20 min) — coordinator integration:
  3.1 Verify all 4 agents completed
  3.2 npm run build (catch any compile errors)
  3.3 npm run dev, smoke test in browser
  3.4 Fix any seams between agent outputs
  3.5 Commit in astro-site repo
  3.6 Push to astro-site origin (separate repo)

Total: ~60 min wall clock (vs ~2 hrs sequential)
```

---

## Why parallel agents work for this

The 4 file partitions have **zero file overlap.** Agent A owns global.css and only global.css. Agent B owns the two hero files only. Agent C owns 18 component files but no hero or layout files. Agent D owns layout + navbar + footer + public/ but no section components.

This means:
- No merge conflicts possible
- Each agent can build, test, and commit independently
- Parallelization gives a 3-4× speedup vs sequential
- Final integration is a smoke test, not a merge resolution

The only shared assumption is the **Palette A token names** that global.css will expose. Agents B/C/D write code that references `bg-brand-50`, `text-text-heading`, `border-border-default`, etc. — all of which Agent A will define. As long as everyone uses the same token names, the integration is clean.

---

## Palette A token reference (shared by all agents)

Every agent must use these tokens. No raw hex values in component code (except for Agent A defining them).

```css
/* Tailwind 4 @theme tokens — defined by Agent A in global.css */

--color-brand-50:  #F8F3EC   /* warm cream — page background */
--color-brand-100: #F2EBDD   /* slightly darker cream — elevated surface */
--color-brand-200: #E8DDD0   /* cream border tone */
--color-brand-300: #D9B89A   /* warm sand */
--color-brand-400: #D97845   /* hover sienna (10% lighter than 500) */
--color-brand-500: #C65D2E   /* primary accent — burnt sienna */
--color-brand-600: #A84820   /* pressed sienna (10% darker than 500) */
--color-brand-700: #8B3A1A   /* deep sienna */
--color-brand-800: #6B2A12   /* very deep sienna */
--color-brand-900: #2C1810   /* deep espresso — headings */

--color-accent-400: #E0A35C  /* warm gold light */
--color-accent-500: #C68B3E  /* warm gold mid */
--color-accent-600: #A86F28  /* warm gold deep */

--color-surface-primary:   #F8F3EC  /* page background */
--color-surface-secondary: #FEFCF8  /* elevated cream (1% lighter) */
--color-surface-tertiary:  #F2EBDD  /* slightly recessed cream */
--color-surface-deep:      #EEE5D5  /* footer background */

--color-text-heading: #2C1810  /* H1-H6 */
--color-text-body:    #4A3028  /* body paragraphs */
--color-text-muted:   #8B7355  /* warm taupe — captions, metadata */
--color-text-light:   #A89580  /* lightest text — disclaimers */

--color-border-default: rgba(44, 24, 16, 0.12)
--color-border-light:   rgba(44, 24, 16, 0.06)

/* Tailwind generates: bg-brand-50, text-brand-500, border-border-default, etc. */
```

### Glass utilities — converted to flat cream

In Palette A, glass morphism doesn't exist. Backdrop blur on a cream background looks dirty. The `.glass*` class names are kept (so existing components don't need to remove the class) but **redefined as flat cream cards with hairline borders**:

```css
.glass {
  background: var(--color-surface-secondary);
  border: 1px solid var(--color-border-default);
  box-shadow: 0 2px 16px rgba(44, 24, 16, 0.06);
  /* no backdrop-filter, no blur */
}

.glass-strong {
  background: var(--color-surface-secondary);
  border: 1px solid var(--color-border-default);
  box-shadow: 0 8px 32px rgba(44, 24, 16, 0.10);
}

.glass-violet {
  background: rgba(198, 93, 46, 0.06);
  border: 1px solid rgba(198, 93, 46, 0.20);
  box-shadow: 0 4px 20px rgba(198, 93, 46, 0.12);
}

.glass-dark {
  background: var(--color-surface-tertiary);
  border: 1px solid var(--color-border-default);
}
```

### Gradients — flatten or remove

`.gradient-text` becomes a solid sienna fill (no gradient). `.gradient-mesh-bg`, `.gradient-hero`, `.space-dots-bg` all become flat cream backgrounds.

### Typography — keep current

Space Grotesk (headings) + DM Sans (body) work fine in Palette A. No font swap needed.

---

## Per-agent briefs

Each agent gets a self-contained brief with: scope, files, exact instructions, verification step, commit message format. Briefs are in the agent dispatch message in the coordinator session — they do NOT need to read this plan to execute.

---

## Success criteria

- [ ] `astro-site/` builds without errors (`npm run build` passes)
- [ ] Dev server renders correctly (`npm run dev` opens to a warm cream site)
- [ ] No remaining hardcoded violet/navy/dark hex values anywhere in `src/`
- [ ] Hero section is no longer the space scene — it's a warm editorial hero
- [ ] All sections render in cream + sienna + espresso
- [ ] Logo (placeholder Iso B) appears in navbar, footer, and as favicon
- [ ] OG image and meta tags reference the new brand
- [ ] No FOUC, no layout shifts, no console errors
- [ ] Mobile responsive
- [ ] All commits land in `astro-site/` git repo (not the parent repo)
