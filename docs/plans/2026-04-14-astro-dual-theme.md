# Astro Site — Dual Theme Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a light/dark theme system to `astro-site/` where light mode uses Palette A (Warm Premium) and dark mode uses Palette E (Aurora Glass), with a user-facing toggle and persistent preference.

**Architecture:** Two-layer CSS variable system. Base layer defines `--theme-*` variables on `:root` (light default) and `[data-theme="dark"]` (dark overrides). Tailwind 4's `@theme` block references those variables so all generated utility classes resolve at runtime. A small React toggle component flips the `data-theme` attribute on `<html>` and persists to `localStorage`. Blocking script in `<head>` reads preference before paint to prevent FOUC.

**Tech Stack:** Astro 5.17, React 19, Tailwind 4, TypeScript, GSAP 3, Framer Motion 12 (already installed — no new deps)

**Status:** Plan only — **not ready to execute** until these decisions are made:

1. **Hero visual treatment** (blocks Task 6)
2. **Default theme on first visit** (blocks Task 4)
3. **Typography strategy** (blocks Task 3)
4. **Theme transition style** (blocks Task 4)

See "Open Decisions" section below for details.

---

## Context

### Current state of `astro-site/`

- **Astro 5 + React 19 + Tailwind 4** — all modern
- **Theme system is in `src/styles/global.css`** using Tailwind 4's `@theme` directive — currently hardcoded to a single dark violet/space aesthetic (coincidentally close to Palette E)
- **Typography:** Space Grotesk (headings) + DM Sans (body) via CSS custom properties
- **Glass utilities baked in:** `.glass`, `.glass-strong`, `.glass-violet`, `.glass-dark` — all use `backdrop-filter: blur()`
- **Hero section (`HeroSection.astro`)** has an animated SVG "space scene" — planet, rocket, shooting star, HUD circles, glass dashboard cards — with hardcoded violet hex values (`#7c3aed`, `#a78bfa`, `#818cf8`) and GSAP timeline animations
- **MeshGradientHero (React)** renders a WebGL-like mesh gradient background — also hardcoded to violet/navy
- **Other sections** (About, Services, HowItWorks, CaseStudies, Testimonials, ROI, FAQ, Contact, Footer) use Tailwind utility classes that reference theme tokens (`bg-brand-50`, `text-text-heading`, `glass-strong`, etc.) — these will swap cleanly once the tokens swap

### The two palettes

Values from `resources/brand-system.md` (Palette A locked) and `resources/palette-samples/DECISION.md` (Palette E hex reference).

**Palette A — Warm Premium (light default)**
```
Background          #F8F3EC   warm cream
Foreground          #2C1810   deep espresso
Primary accent      #C65D2E   burnt sienna
Muted text          #8B7355   warm taupe
Border              #E8DDD0   cream border
Elevated surface    #FEFCF8   1% lighter than cream
Hover sienna        #D97845   10% lighter accent
Pressed sienna      #A84820   10% darker accent
```

**Palette E — Aurora Glass (dark)**
```
Background          #0B0F1F   aurora navy
Elevated surface    #0E1329   slightly lighter navy
Foreground          #F1F3FA   lunar white
Muted text          #8B90A8   cool muted grey
Primary accent      #7C5CFF   electric violet
Secondary accent    #6BFFCB   soft mint
Border              rgba(255,255,255,0.1)
Glass surface       rgba(255,255,255,0.06) + backdrop-blur(20px)
Glow shadow         0 4px 24px rgba(124,92,255,0.45)
```

### Why these two palettes clash in one component

Light mode is **flat color, no blur, no glow, editorial restraint.** Dark mode is **glass morphism, radial gradients, violet/mint glow, liquid aesthetic.** These aren't just different colors — they're different visual languages. Specifically:

- **Cards:** Light = flat cream with hairline borders. Dark = frosted glass with backdrop-blur and inset highlight.
- **Buttons:** Light = solid sienna fill. Dark = violet gradient with glow shadow.
- **Background:** Light = flat cream (no gradients). Dark = radial aurora gradients from violet + mint glows.
- **Hero:** Light = ??? (open decision). Dark = animated space scene with GSAP.

The implementation has to handle both systems gracefully — not just swap color values.

---

## Open Decisions

### Decision 1: Hero visual treatment

**Option A — Dark band always.** Hero stays dark-mode-only (keeps current space scene + glass dashboard cards), rendered as an intentional dark band at the top of a light-theme page. Pattern used by Stripe, Linear marketing pages. Simplest path.

**Option B — Two hero components.** Build `HeroSectionLight.astro` alongside existing `HeroSection.astro`. Light version shows an editorial warm orchestration diagram (animated or static) in sienna on cream. BaseLayout or index.astro conditionally renders based on theme.

**Recommendation:** Option A for v1, upgrade to Option B later if needed. Saves ~60-90 min and is a legitimate design pattern.

**This plan assumes Option A** and calls out every place where Option B would diverge. If Option B is chosen, add Task 6b (Build light hero component) — ~90 min.

### Decision 2: Default theme on first visit

- **2a. Respect `prefers-color-scheme`** — OS-level preference wins. Accessible, user-respecting.
- **2b. Light default** — Palette A is the locked brand identity; light is the flagship aesthetic. Dark is optional.
- **2c. Dark default** — matches the current site state; smooth upgrade path.

**Recommendation:** 2a (respect OS preference, fall back to light if unknown).

### Decision 3: Typography strategy

- **3a. Keep Space Grotesk (headings) + DM Sans (body)** — current state, works in both themes, no visual disruption. `brand-system.md` specifies Inter but that was written before the dual-theme idea; typography is separate from palette.
- **3b. Switch to Inter for both themes** — aligns with `brand-system.md`. Requires updating `global.css` font vars and removing Space Grotesk/DM Sans font loading.
- **3c. Theme-swap fonts** — Inter in light, Space Grotesk in dark. Maximum differentiation between modes.

**Recommendation:** 3a (keep current fonts). Font swapping per theme is flashy but adds layout shift on toggle and complicates FOUC prevention.

### Decision 4: Theme transition style

- **4a. Instant (no animation)** — safest, accessible, no layout-shift risk
- **4b. 200ms color fade** — `transition: background-color 200ms, color 200ms, border-color 200ms, fill 200ms, stroke 200ms` on `*`. Fancier, slightly more complex to get right (some properties shouldn't animate)
- **4c. 200ms fade + respect `prefers-reduced-motion`** — 4b with safety

**Recommendation:** 4c.

---

## File Structure

### New files

| Path | Responsibility |
|------|----------------|
| `src/components/react/ThemeToggle.tsx` | Client-side toggle button with sun/moon icon, wires to `localStorage` and `data-theme` attribute |
| `src/lib/theme-init.ts` | Tiny inline script (stringified) that runs in `<head>` before paint to read preference and set `data-theme` — prevents FOUC |

### Modified files

| Path | What changes |
|------|--------------|
| `src/styles/global.css` | Rewrite `@theme` block to reference `var(--theme-*)` tokens. Add `:root` and `[data-theme="dark"]` blocks defining those tokens. Add theme-aware variants of `.glass*` utilities. Add transition rules (if 4b/4c chosen) |
| `src/layouts/BaseLayout.astro` | Inject FOUC-prevention script in `<head>`. Add `<html lang="en" data-theme="...">` (initial attribute set by script) |
| `src/components/astro/Navbar.astro` | Mount `<ThemeToggle client:load />` in the right side of the navbar |
| `src/components/astro/HeroSection.astro` | Wrap in conditional rendering or apply dark-only styling (Option A). SVG planet scene keeps its hardcoded colors. Glass dashboard cards use theme-aware variants where possible |
| `src/components/react/MeshGradientHero.tsx` | Audit for hardcoded hex values. If Option A: no change (stays dark). If Option B: conditional rendering per theme |
| `src/components/astro/AboutSection.astro` | Audit for hardcoded hex values — replace with CSS variable references |
| `src/components/astro/ServicesSection.astro` | Audit for hardcoded hex values |
| `src/components/astro/HowItWorksSection.astro` | Audit for hardcoded hex values |
| `src/components/astro/CaseStudiesSection.astro` | Audit for hardcoded hex values |
| `src/components/astro/TestimonialsSection.astro` | Audit for hardcoded hex values |
| `src/components/astro/ROISection.astro` | Audit for hardcoded hex values |
| `src/components/astro/FAQSection.astro` | Audit for hardcoded hex values |
| `src/components/astro/ContactSection.astro` | Audit for hardcoded hex values |
| `src/components/astro/Footer.astro` | Audit for hardcoded hex values |
| `src/components/astro/TrustedBy.astro` | Audit for hardcoded hex values |
| `src/components/react/FAQAccordion.tsx` | Audit for hardcoded hex values |
| `src/components/react/ChatWidget.tsx` | Audit for hardcoded hex values |
| `src/components/react/StatCounter.tsx` | Audit — likely fine if using Tailwind classes |
| `src/components/react/ROICalculator.tsx` | Audit for hardcoded hex values |
| `src/components/react/ContactForm.tsx` | Audit for hardcoded hex values |
| `src/components/react/IndustryTabs.tsx` | Audit for hardcoded hex values |
| `src/components/react/MobileMenu.tsx` | Audit for hardcoded hex values |
| `src/components/ui/Button.tsx` | Ensure uses theme tokens, not raw hex |
| `src/components/ui/Badge.tsx` | Ensure uses theme tokens |
| `src/components/ui/GlassCard.tsx` | Handles the glass/flat card split per theme |

### Files NOT touched

- `src/data/*.ts` — typed data files, no visual changes needed
- `src/lib/animations.ts` + `src/lib/gsap-init.ts` — animation logic, unrelated to theme
- `src/hooks/useMousePosition.ts` — unrelated

---

## Tasks

### Task 1: Audit hardcoded hex values

**Files:**
- Read-only audit pass across all components in `src/components/`

- [ ] **Step 1: Grep for hardcoded hex values**

  Run from `astro-site/`:
  ```bash
  grep -rn --include="*.astro" --include="*.tsx" --include="*.ts" -E "#[0-9a-fA-F]{3,8}\b" src/components/ src/layouts/ | tee ../../docs/plans/astro-hex-audit.txt
  ```

  Expected: tens to hundreds of matches. Most will be in `HeroSection.astro` (the space scene SVG), `MeshGradientHero.tsx` (gradient stops), and any component using inline SVGs.

- [ ] **Step 2: Categorize each match**

  Open `docs/plans/astro-hex-audit.txt`. For each match, label one of:
  - **T** = theme-swappable (semantic color — body text, background, accent) — must become a CSS variable
  - **D** = dark-only (space scene, violet glows, meant to stay dark even in light mode) — leave as-is if Option A for Hero, otherwise needs a light-mode counterpart
  - **U** = universal (neutrals like pure white on a photo, brand-external logos) — leave as-is

  Commit the annotated file:
  ```bash
  cd "../.." && git add docs/plans/astro-hex-audit.txt
  git commit -m "docs: astro hex value audit for dual-theme implementation"
  ```

---

### Task 2: Set up theme token CSS variable system

**Files:**
- Modify: `astro-site/src/styles/global.css`

- [ ] **Step 1: Replace the `@theme` block**

  Find the current `@theme { ... }` block at the top of `src/styles/global.css`. Replace the color definitions inside it with `var(--theme-*)` references:

  ```css
  @theme {
    /* Primary Palette — references runtime CSS variables */
    --color-brand-50: var(--theme-brand-50);
    --color-brand-100: var(--theme-brand-100);
    --color-brand-200: var(--theme-brand-200);
    --color-brand-300: var(--theme-brand-300);
    --color-brand-400: var(--theme-brand-400);
    --color-brand-500: var(--theme-brand-500);
    --color-brand-600: var(--theme-brand-600);
    --color-brand-700: var(--theme-brand-700);
    --color-brand-800: var(--theme-brand-800);
    --color-brand-900: var(--theme-brand-900);

    /* Accent — references runtime */
    --color-accent-400: var(--theme-accent-400);
    --color-accent-500: var(--theme-accent-500);
    --color-accent-600: var(--theme-accent-600);

    /* Surfaces */
    --color-surface-primary: var(--theme-surface-primary);
    --color-surface-secondary: var(--theme-surface-secondary);
    --color-surface-tertiary: var(--theme-surface-tertiary);
    --color-surface-deep: var(--theme-surface-deep);

    /* Text */
    --color-text-heading: var(--theme-text-heading);
    --color-text-body: var(--theme-text-body);
    --color-text-muted: var(--theme-text-muted);
    --color-text-light: var(--theme-text-light);

    /* Borders */
    --color-border-default: var(--theme-border-default);
    --color-border-light: var(--theme-border-light);

    /* Typography — theme-agnostic */
    --font-heading: 'Space Grotesk', ui-sans-serif, system-ui, sans-serif;
    --font-sans: 'DM Sans', ui-sans-serif, system-ui, -apple-system, sans-serif;

    /* Spacing — theme-agnostic */
    --spacing-18: 4.5rem;
    --spacing-22: 5.5rem;
    --spacing-30: 7.5rem;

    /* Shadows — reference runtime variables for theme-specific glow */
    --shadow-glass: var(--theme-shadow-glass);
    --shadow-glass-lg: var(--theme-shadow-glass-lg);
    --shadow-glass-violet: var(--theme-shadow-glass-violet);
    --shadow-glow: var(--theme-shadow-glow);
    --shadow-glow-lg: var(--theme-shadow-glow-lg);
    --shadow-elevated: var(--theme-shadow-elevated);

    /* Animations — theme-agnostic */
    --animate-float: float 6s ease-in-out infinite;
    --animate-float-delayed: float 6s ease-in-out 2s infinite;
    --animate-marquee: marquee 40s linear infinite;
    --animate-mesh: meshShift 10s ease infinite;
    --animate-pulse-glow: pulseGlow 3s ease-in-out infinite;

    /* Easing — theme-agnostic */
    --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
  }
  ```

- [ ] **Step 2: Add light theme (`:root`) token definitions**

  Below the `@theme` block, add:

  ```css
  /* ===== Light Theme — Palette A (Warm Premium) ===== */

  :root {
    /* Brand scale — warm cream to deep espresso with sienna accent mid */
    --theme-brand-50:  #F8F3EC;
    --theme-brand-100: #F2EBDD;
    --theme-brand-200: #E8DDD0;
    --theme-brand-300: #D9B89A;
    --theme-brand-400: #D97845;
    --theme-brand-500: #C65D2E;
    --theme-brand-600: #A84820;
    --theme-brand-700: #8B3A1A;
    --theme-brand-800: #6B2A12;
    --theme-brand-900: #2C1810;

    /* Accent — warmer gold for secondary actions in light */
    --theme-accent-400: #E0A35C;
    --theme-accent-500: #C68B3E;
    --theme-accent-600: #A86F28;

    /* Surfaces — layered creams */
    --theme-surface-primary:   #F8F3EC;
    --theme-surface-secondary: #FEFCF8;
    --theme-surface-tertiary:  #F2EBDD;
    --theme-surface-deep:      #EEE5D5;

    /* Text — espresso hierarchy */
    --theme-text-heading: #2C1810;
    --theme-text-body:    #4A3028;
    --theme-text-muted:   #8B7355;
    --theme-text-light:   #A89580;

    /* Borders — hairline cream */
    --theme-border-default: rgba(44, 24, 16, 0.12);
    --theme-border-light:   rgba(44, 24, 16, 0.06);

    /* Shadows — flat, warm, no glow */
    --theme-shadow-glass:        0 2px 16px rgba(44, 24, 16, 0.06);
    --theme-shadow-glass-lg:     0 8px 32px rgba(44, 24, 16, 0.08);
    --theme-shadow-glass-violet: 0 4px 20px rgba(198, 93, 46, 0.12);
    --theme-shadow-glow:         0 0 0 rgba(0, 0, 0, 0);
    --theme-shadow-glow-lg:      0 0 0 rgba(0, 0, 0, 0);
    --theme-shadow-elevated:     0 12px 40px -12px rgba(44, 24, 16, 0.15);
  }
  ```

- [ ] **Step 3: Add dark theme (`[data-theme="dark"]`) token overrides**

  Below the `:root` block, add:

  ```css
  /* ===== Dark Theme — Palette E (Aurora Glass) ===== */

  [data-theme="dark"] {
    /* Brand scale — aurora navy to electric violet */
    --theme-brand-50:  #0E1329;
    --theme-brand-100: #131A35;
    --theme-brand-200: #1B2544;
    --theme-brand-300: #C4B5FD;
    --theme-brand-400: #A78BFA;
    --theme-brand-500: #7C5CFF;
    --theme-brand-600: #6B4BE8;
    --theme-brand-700: #5B3ED0;
    --theme-brand-800: #4C34B2;
    --theme-brand-900: #0B0F1F;

    /* Accent — mint secondary */
    --theme-accent-400: #6BFFCB;
    --theme-accent-500: #3EE8A8;
    --theme-accent-600: #2ACC8A;

    /* Surfaces — deep space layers */
    --theme-surface-primary:   #0B0F1F;
    --theme-surface-secondary: #0E1329;
    --theme-surface-tertiary:  #131A35;
    --theme-surface-deep:      #06080F;

    /* Text — cool lunar white hierarchy */
    --theme-text-heading: #F1F3FA;
    --theme-text-body:    #CBD5E1;
    --theme-text-muted:   #8B90A8;
    --theme-text-light:   #64758B;

    /* Borders — subtle glow edges */
    --theme-border-default: rgba(255, 255, 255, 0.10);
    --theme-border-light:   rgba(255, 255, 255, 0.05);

    /* Shadows — violet glows */
    --theme-shadow-glass:        0 4px 30px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.04);
    --theme-shadow-glass-lg:     0 8px 40px rgba(0, 0, 0, 0.4), inset 0 1px 0 rgba(255, 255, 255, 0.05);
    --theme-shadow-glass-violet: 0 8px 40px rgba(124, 92, 255, 0.25), inset 0 1px 0 rgba(255, 255, 255, 0.04);
    --theme-shadow-glow:         0 0 40px rgba(124, 92, 255, 0.25);
    --theme-shadow-glow-lg:      0 0 80px rgba(124, 92, 255, 0.3);
    --theme-shadow-elevated:     0 20px 60px -12px rgba(0, 0, 0, 0.5);
  }
  ```

- [ ] **Step 4: Replace glass utility classes with theme-aware versions**

  Find the `/* ===== Glass Utility Classes — Dark Space ===== */` block. Replace with:

  ```css
  /* ===== Glass Utility Classes — Theme-aware ===== */

  .glass {
    background: var(--theme-glass-bg);
    backdrop-filter: var(--theme-glass-blur);
    -webkit-backdrop-filter: var(--theme-glass-blur);
    border: 1px solid var(--theme-glass-border);
    box-shadow: var(--theme-shadow-glass);
  }

  .glass-strong {
    background: var(--theme-glass-strong-bg);
    backdrop-filter: var(--theme-glass-strong-blur);
    -webkit-backdrop-filter: var(--theme-glass-strong-blur);
    border: 1px solid var(--theme-glass-strong-border);
    box-shadow: var(--theme-shadow-glass-lg);
  }

  .glass-violet {
    background: var(--theme-glass-accent-bg);
    backdrop-filter: var(--theme-glass-blur);
    -webkit-backdrop-filter: var(--theme-glass-blur);
    border: 1px solid var(--theme-glass-accent-border);
    box-shadow: var(--theme-shadow-glass-violet);
  }

  .glass-dark {
    background: var(--theme-glass-solid-bg);
    backdrop-filter: var(--theme-glass-strong-blur);
    -webkit-backdrop-filter: var(--theme-glass-strong-blur);
    border: 1px solid var(--theme-glass-strong-border);
  }
  ```

  Then add the new `--theme-glass-*` variables to the `:root` block:

  ```css
  /* (append inside :root) */
  --theme-glass-bg: #FEFCF8;
  --theme-glass-strong-bg: #F2EBDD;
  --theme-glass-accent-bg: rgba(198, 93, 46, 0.06);
  --theme-glass-solid-bg: #F8F3EC;
  --theme-glass-blur: none;
  --theme-glass-strong-blur: none;
  --theme-glass-border: rgba(44, 24, 16, 0.08);
  --theme-glass-strong-border: rgba(44, 24, 16, 0.12);
  --theme-glass-accent-border: rgba(198, 93, 46, 0.2);
  ```

  And to the `[data-theme="dark"]` block:

  ```css
  /* (append inside [data-theme="dark"]) */
  --theme-glass-bg: rgba(255, 255, 255, 0.04);
  --theme-glass-strong-bg: rgba(255, 255, 255, 0.06);
  --theme-glass-accent-bg: rgba(124, 92, 255, 0.10);
  --theme-glass-solid-bg: rgba(6, 6, 10, 0.85);
  --theme-glass-blur: blur(16px);
  --theme-glass-strong-blur: blur(20px);
  --theme-glass-border: rgba(255, 255, 255, 0.06);
  --theme-glass-strong-border: rgba(255, 255, 255, 0.10);
  --theme-glass-accent-border: rgba(124, 92, 255, 0.18);
  ```

  **Result:** In light mode, `.glass` renders as a flat cream card with hairline border and a soft warm shadow — no backdrop blur. In dark mode, it renders as frosted glass with blur and subtle inset highlight.

- [ ] **Step 5: Update `body` and `::selection` to use theme tokens**

  Find the `body { ... }` block and change `background:` to use the theme token:

  ```css
  body {
    font-family: var(--font-sans);
    color: var(--color-text-body);
    background: var(--color-surface-primary);
    overflow-x: hidden;
  }

  ::selection {
    background: var(--color-brand-500);
    color: var(--theme-surface-primary);
  }
  ```

- [ ] **Step 6: Update gradient utilities for both themes**

  Find `.gradient-text`, `.gradient-mesh-bg`, `.gradient-hero`, and `.space-dots-bg`. These are currently dark-mode specific. Wrap dark-mode-only variants inside `[data-theme="dark"]` selector and provide light-mode alternatives:

  ```css
  /* Gradient text — theme-aware */
  .gradient-text {
    background: linear-gradient(135deg, var(--color-brand-500) 0%, var(--color-brand-600) 50%, var(--color-brand-400) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  [data-theme="dark"] .gradient-text {
    background: linear-gradient(135deg, var(--color-brand-400) 0%, #818cf8 50%, var(--color-brand-300) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  /* Mesh background — dark only */
  .gradient-mesh-bg {
    background: var(--color-surface-primary);
  }

  [data-theme="dark"] .gradient-mesh-bg {
    background:
      radial-gradient(ellipse 60% 50% at 20% 30%, rgba(124, 92, 255, 0.12) 0%, transparent 70%),
      radial-gradient(ellipse 50% 60% at 80% 20%, rgba(107, 255, 203, 0.08) 0%, transparent 70%),
      radial-gradient(ellipse 40% 50% at 50% 80%, rgba(59, 130, 246, 0.06) 0%, transparent 70%),
      var(--color-surface-primary);
  }

  /* Hero gradient — dark only, flat in light */
  .gradient-hero {
    background: var(--color-surface-primary);
  }

  [data-theme="dark"] .gradient-hero {
    background:
      radial-gradient(ellipse 80% 60% at 30% 20%, rgba(124, 92, 255, 0.15) 0%, transparent 60%),
      radial-gradient(ellipse 60% 50% at 70% 40%, rgba(107, 255, 203, 0.10) 0%, transparent 60%),
      radial-gradient(ellipse 50% 40% at 50% 90%, rgba(59, 130, 246, 0.08) 0%, transparent 60%),
      linear-gradient(180deg, #0d0c14 0%, var(--color-surface-primary) 100%);
  }

  /* Starfield — dark only */
  .space-dots-bg {
    background-image: none;
  }

  [data-theme="dark"] .space-dots-bg {
    background-image:
      radial-gradient(1px 1px at 10% 20%, rgba(255,255,255,0.15) 0%, transparent 100%),
      radial-gradient(1px 1px at 30% 60%, rgba(255,255,255,0.1) 0%, transparent 100%),
      radial-gradient(1px 1px at 50% 10%, rgba(255,255,255,0.12) 0%, transparent 100%),
      radial-gradient(1px 1px at 70% 80%, rgba(255,255,255,0.08) 0%, transparent 100%),
      radial-gradient(1px 1px at 90% 40%, rgba(255,255,255,0.1) 0%, transparent 100%),
      radial-gradient(1.5px 1.5px at 25% 85%, rgba(167,139,250,0.15) 0%, transparent 100%),
      radial-gradient(1.5px 1.5px at 75% 25%, rgba(129,140,248,0.12) 0%, transparent 100%);
  }
  ```

- [ ] **Step 7: Add transition rules (if Decision 4 = 4b or 4c)**

  If 4c chosen, add below the `:root` block:

  ```css
  /* Smooth theme transitions — respect reduced motion */
  @media (prefers-reduced-motion: no-preference) {
    *, *::before, *::after {
      transition-property: background-color, color, border-color, fill, stroke, box-shadow;
      transition-duration: 200ms;
      transition-timing-function: cubic-bezier(0.16, 1, 0.3, 1);
    }
  }
  ```

  If 4a (instant) chosen, skip this step.

- [ ] **Step 8: Run dev server and verify light mode renders**

  ```bash
  cd astro-site && npm run dev
  ```

  Open `http://localhost:4321`. The page will render with **no theme attribute set**, defaulting to `:root` (light mode). Expected:
  - Background is warm cream `#F8F3EC`
  - Text is deep espresso
  - Buttons currently styled via Tailwind utilities will now reference sienna
  - Hero section will look broken (still has hardcoded violet) — that's expected, fixed in Task 6
  - Most sections will swap cleanly

  Kill the dev server (Ctrl+C).

- [ ] **Step 9: Manually test dark mode**

  In the browser devtools (Elements panel), find `<html>` and add `data-theme="dark"` attribute. Verify the page snaps back to the original dark aesthetic.

  Remove the attribute. Verify it goes back to light mode.

- [ ] **Step 10: Commit**

  ```bash
  cd astro-site
  git add src/styles/global.css
  git commit -m "feat(theme): dual palette CSS variable system (A light, E dark)"
  ```

---

### Task 3: Typography decision (Decision 3)

**Files:** `src/styles/global.css` (already open from Task 2 if keeping the session)

- [ ] **Step 1: Implement based on Decision 3 choice**

  **If 3a (keep current):** No changes. Skip to Step 2.

  **If 3b (switch to Inter):**
  - Add to `src/layouts/BaseLayout.astro` `<head>`:
    ```html
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
    ```
  - Remove any existing Space Grotesk / DM Sans `<link>` tags
  - In `global.css` `@theme` block, update:
    ```css
    --font-heading: 'Inter', ui-sans-serif, system-ui, sans-serif;
    --font-sans: 'Inter', ui-sans-serif, system-ui, -apple-system, sans-serif;
    ```

  **If 3c (theme-swap fonts):**
  - Add both font links as in 3b, plus keep Space Grotesk
  - Add font variables to both theme blocks:
    ```css
    :root {
      /* ... existing ... */
      --theme-font-heading: 'Inter', ui-sans-serif, system-ui, sans-serif;
      --theme-font-sans: 'Inter', ui-sans-serif, system-ui, -apple-system, sans-serif;
    }

    [data-theme="dark"] {
      /* ... existing ... */
      --theme-font-heading: 'Space Grotesk', ui-sans-serif, system-ui, sans-serif;
      --theme-font-sans: 'DM Sans', ui-sans-serif, system-ui, -apple-system, sans-serif;
    }
    ```
  - Update `@theme` block:
    ```css
    --font-heading: var(--theme-font-heading);
    --font-sans: var(--theme-font-sans);
    ```

- [ ] **Step 2: Test and commit**

  Run `npm run dev`, verify typography is correct in both themes.

  ```bash
  git add src/styles/global.css src/layouts/BaseLayout.astro
  git commit -m "feat(theme): apply typography strategy [3a|3b|3c]"
  ```

---

### Task 4: Theme init script and toggle component

**Files:**
- Create: `astro-site/src/lib/theme-init.ts`
- Create: `astro-site/src/components/react/ThemeToggle.tsx`
- Modify: `astro-site/src/layouts/BaseLayout.astro`
- Modify: `astro-site/src/components/astro/Navbar.astro`

- [ ] **Step 1: Create `src/lib/theme-init.ts`**

  Full file content:

  ```typescript
  // Exported as a string to be injected inline into <head> before any CSS/JS loads.
  // Must be synchronous and self-contained — no imports.
  // Runs before first paint to prevent FOUC (flash of unstyled content).

  export const themeInitScript = `
    (function () {
      try {
        var stored = localStorage.getItem('ai-forte-theme');
        var theme;
        if (stored === 'light' || stored === 'dark') {
          theme = stored;
        } else {
          // Decision 2 default — see docs/plans/2026-04-14-astro-dual-theme.md
          // Replace this block based on Decision 2 choice:
          // 2a (respect OS): use matchMedia
          // 2b (light default): theme = 'light'
          // 2c (dark default): theme = 'dark'
          var prefersDark = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
          theme = prefersDark ? 'dark' : 'light';
        }
        document.documentElement.setAttribute('data-theme', theme);
      } catch (e) {
        document.documentElement.setAttribute('data-theme', 'light');
      }
    })();
  `.trim();
  ```

- [ ] **Step 2: Inject the init script into `BaseLayout.astro`**

  Open `src/layouts/BaseLayout.astro`. At the top of the frontmatter (inside `---` fences), add:

  ```astro
  import { themeInitScript } from '../lib/theme-init';
  ```

  In the `<head>` element of the template (look for existing `<head>`), add this as the **first child** of `<head>` (before any `<link>` or `<style>` tags):

  ```astro
  <script is:inline set:html={themeInitScript}></script>
  ```

  `is:inline` ensures Astro doesn't process/bundle the script — it emits it raw. `set:html` injects the string without escaping.

- [ ] **Step 3: Create `src/components/react/ThemeToggle.tsx`**

  Full file content:

  ```tsx
  import { useEffect, useState } from 'react';

  type Theme = 'light' | 'dark';

  export default function ThemeToggle() {
    // Initial state matches what theme-init.ts set on <html>, avoiding hydration mismatch
    const [theme, setTheme] = useState<Theme>(() => {
      if (typeof document === 'undefined') return 'light';
      return (document.documentElement.getAttribute('data-theme') as Theme) || 'light';
    });

    // Sync state changes back to DOM + localStorage
    useEffect(() => {
      document.documentElement.setAttribute('data-theme', theme);
      localStorage.setItem('ai-forte-theme', theme);
    }, [theme]);

    // Optional: listen for OS theme changes if user hasn't explicitly chosen
    useEffect(() => {
      const mq = window.matchMedia('(prefers-color-scheme: dark)');
      const handler = (e: MediaQueryListEvent) => {
        if (!localStorage.getItem('ai-forte-theme')) {
          setTheme(e.matches ? 'dark' : 'light');
        }
      };
      mq.addEventListener('change', handler);
      return () => mq.removeEventListener('change', handler);
    }, []);

    const toggle = () => setTheme(t => (t === 'light' ? 'dark' : 'light'));

    return (
      <button
        type="button"
        onClick={toggle}
        aria-label={theme === 'light' ? 'Switch to dark theme' : 'Switch to light theme'}
        className="inline-flex items-center justify-center w-9 h-9 rounded-lg border border-border-default hover:bg-surface-secondary transition-colors"
      >
        {theme === 'light' ? (
          /* Moon icon — shown in light mode, click to go dark */
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className="text-text-body">
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
          </svg>
        ) : (
          /* Sun icon — shown in dark mode, click to go light */
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className="text-text-body">
            <circle cx="12" cy="12" r="4" />
            <path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M6.34 17.66l-1.41 1.41M19.07 4.93l-1.41 1.41" />
          </svg>
        )}
      </button>
    );
  }
  ```

- [ ] **Step 4: Mount the toggle in `Navbar.astro`**

  Open `src/components/astro/Navbar.astro`. At the top of the frontmatter, add the import:

  ```astro
  import ThemeToggle from '../react/ThemeToggle';
  ```

  In the nav template, find the right side of the navbar (likely where CTA buttons or links live). Add the toggle before the primary CTA:

  ```astro
  <ThemeToggle client:load />
  ```

  `client:load` tells Astro to hydrate the component immediately on page load (needed because the toggle is interactive from the moment the page renders).

- [ ] **Step 5: Run dev server and test the full flow**

  ```bash
  cd astro-site && npm run dev
  ```

  Open `http://localhost:4321`. Expected:
  1. Page loads in whichever theme Decision 2 dictates (no FOUC — should not flash light then dark)
  2. Theme toggle button visible in navbar
  3. Click the toggle → theme swaps immediately
  4. Refresh the page → preference persists
  5. Open DevTools → Application → Local Storage → verify `ai-forte-theme` key exists

- [ ] **Step 6: Commit**

  ```bash
  git add src/lib/theme-init.ts \
          src/components/react/ThemeToggle.tsx \
          src/layouts/BaseLayout.astro \
          src/components/astro/Navbar.astro
  git commit -m "feat(theme): add theme toggle, FOUC prevention, localStorage persistence"
  ```

---

### Task 5: Component sweep — replace hardcoded hex with theme tokens

**Files:** All components flagged with label **T** in the Task 1 audit file.

For each component, replace hardcoded hex values with Tailwind utility classes that reference theme tokens, OR inline CSS using `var(--color-*)`.

- [ ] **Step 1: Start with `About`, `Services`, `HowItWorks`**

  Open `docs/plans/astro-hex-audit.txt` and filter to these three files. For each **T**-labeled match, open the file, find the hex value, replace with the appropriate token:

  | Hardcoded | Token replacement |
  |-----------|-------------------|
  | Any `#0B0B10`, `#0F0E1A`, `#151425` | `bg-surface-primary` / `bg-surface-secondary` / `bg-surface-tertiary` or `var(--color-surface-*)` |
  | Any `#F8FAFC`, `#E8DDD0` | `text-text-heading` or `var(--color-text-heading)` |
  | Any `#CBD5E1`, `#94A3B8` | `text-text-body` / `text-text-muted` |
  | Any `#7c3aed`, `#a78bfa`, `#C65D2E` | `text-brand-500` / `bg-brand-500` / `border-brand-500` or `var(--color-brand-*)` |
  | Any rgba white/black | `var(--color-border-default)` / `var(--color-border-light)` |

- [ ] **Step 2: Verify in browser**

  `npm run dev` → visit the page → scroll through About/Services/HowItWorks in BOTH themes. Every text, background, border, and accent should swap cleanly when you click the theme toggle.

- [ ] **Step 3: Commit**

  ```bash
  git add src/components/astro/AboutSection.astro \
          src/components/astro/ServicesSection.astro \
          src/components/astro/HowItWorksSection.astro
  git commit -m "refactor(theme): replace hardcoded hex with theme tokens in About/Services/HowItWorks"
  ```

- [ ] **Step 4: Repeat for `CaseStudies`, `Testimonials`, `ROI`**

  Same process. Commit as:
  ```bash
  git commit -m "refactor(theme): replace hardcoded hex with theme tokens in CaseStudies/Testimonials/ROI"
  ```

- [ ] **Step 5: Repeat for `FAQ`, `Contact`, `Footer`, `TrustedBy`**

  Commit as:
  ```bash
  git commit -m "refactor(theme): replace hardcoded hex with theme tokens in FAQ/Contact/Footer/TrustedBy"
  ```

- [ ] **Step 6: Repeat for React components**

  Files: `FAQAccordion.tsx`, `ChatWidget.tsx`, `StatCounter.tsx`, `ROICalculator.tsx`, `ContactForm.tsx`, `IndustryTabs.tsx`, `MobileMenu.tsx`, `Button.tsx`, `Badge.tsx`, `GlassCard.tsx`

  For React, inline styles using `var(--color-*)` or Tailwind utility classes both work. Prefer Tailwind utilities.

  Commit as:
  ```bash
  git commit -m "refactor(theme): replace hardcoded hex with theme tokens in React components"
  ```

---

### Task 6: Hero section — theme strategy (Option A path)

**Files:**
- Modify: `astro-site/src/components/astro/HeroSection.astro`
- Modify: `astro-site/src/components/react/MeshGradientHero.tsx`

This task assumes **Decision 1 = Option A** (Hero stays dark always, rendered as intentional dark band). If Option B is chosen, skip this task and execute Task 6b instead.

- [ ] **Step 1: Force dark theme inside hero section**

  Open `src/components/astro/HeroSection.astro`. Find the root `<section id="hero" ...>` element. Add `data-theme="dark"` as an attribute:

  ```astro
  <section id="hero" data-theme="dark" class="relative min-h-[92vh] flex items-center pt-20 pb-12 overflow-hidden">
  ```

  This scopes the dark theme to just the hero — every child uses dark-mode tokens, but the rest of the page continues to honor the root theme. CSS variable cascading handles this automatically since `[data-theme="dark"]` is a descendant selector.

- [ ] **Step 2: Wrap hero in a dark ambient layer**

  Inside the `<section>`, ensure the first child sets a dark background explicitly (not just inherited tokens). Add or confirm:

  ```astro
  <section id="hero" data-theme="dark" class="relative min-h-[92vh] flex items-center pt-20 pb-12 overflow-hidden bg-surface-primary">
  ```

  `bg-surface-primary` now resolves to `#0B0F1F` aurora navy because of the `data-theme="dark"` scope.

- [ ] **Step 3: Update hardcoded violet hex in SVG planet scene**

  The SVG planet scene has hardcoded violets like `#7c3aed`, `#a78bfa`, `#352d5e`. Update these to match Palette E's violet (`#7C5CFF`) and mint (`#6BFFCB`). Find each occurrence in the SVG and replace:

  | Old | New |
  |-----|-----|
  | `#7c3aed` | `#7C5CFF` |
  | `#a78bfa` | `#9B7EFF` |
  | `#c4b5fd` | `#B8A5FF` |
  | `#818cf8` | `#6BFFCB` (for contrast/highlights) |
  | `#3b82f6` | `#6BFFCB` |
  | `#231e3d` | `#131A35` |
  | `#352d5e` | `#1B2544` |
  | `#0f0e1a` | `#0B0F1F` |

  This keeps the animated planet/rocket but repaints it in Palette E colors.

- [ ] **Step 4: Update `MeshGradientHero.tsx`**

  Open the React mesh gradient component. Replace any hardcoded violet hex values with Palette E equivalents (same mapping as Step 3).

- [ ] **Step 5: Test hero in both themes**

  `npm run dev` → visit `http://localhost:4321`. Toggle theme.

  **Expected:**
  - Light mode: everything except hero is warm cream. Hero is a dark navy band at the top with violet glows.
  - Dark mode: everything is dark navy. Hero blends seamlessly.

  Both should look intentional.

- [ ] **Step 6: Commit**

  ```bash
  git add src/components/astro/HeroSection.astro \
          src/components/react/MeshGradientHero.tsx
  git commit -m "feat(theme): scope hero section to dark theme (Option A)"
  ```

---

### Task 6b: Light hero component (Option B path — SKIP if Option A)

**Only execute if Decision 1 = Option B.**

**Files:**
- Create: `astro-site/src/components/astro/HeroSectionLight.astro`
- Modify: `astro-site/src/pages/index.astro`

- [ ] **Step 1: Create `HeroSectionLight.astro`**

  Build an editorial warm hero variant: bold sienna headline, warm cream background, a static orchestration diagram in sienna on cream, no animation, no glass. Use the one-pager header visual from `resources/one-pager/ai-forte-one-pager-header-1.jpg` as visual reference.

  This is a significant component build (~60-90 min). Full implementation left for execution time — reference the editorial layouts in `resources/palette-samples/preview.html` column A for styling cues.

- [ ] **Step 2: Conditional render in `index.astro`**

  ```astro
  ---
  // At the top of frontmatter
  ---
  <BaseLayout>
    <Navbar />
    <main>
      <!-- Hero is rendered by JS based on data-theme; both are in DOM but one is display:none -->
      <div class="theme-hero-light">
        <HeroSectionLight />
      </div>
      <div class="theme-hero-dark">
        <HeroSection />
      </div>
      <!-- ... rest of main ... -->
    </main>
  </BaseLayout>
  ```

  Add CSS to `global.css`:
  ```css
  .theme-hero-light { display: block; }
  .theme-hero-dark  { display: none; }
  [data-theme="dark"] .theme-hero-light { display: none; }
  [data-theme="dark"] .theme-hero-dark  { display: block; }
  ```

- [ ] **Step 3: Commit**

  ```bash
  git add src/components/astro/HeroSectionLight.astro \
          src/pages/index.astro \
          src/styles/global.css
  git commit -m "feat(theme): add light hero variant (Option B)"
  ```

---

### Task 7: Full smoke test

**Files:** None — testing only

- [ ] **Step 1: Run dev server**

  ```bash
  cd astro-site && npm run dev
  ```

- [ ] **Step 2: Verify light mode**

  1. Clear `localStorage` in DevTools → reload
  2. If Decision 2 = 2a, set OS to light preference first
  3. Page should load in light mode with no FOUC (no flash of dark)
  4. Scroll through entire page — every section uses cream/espresso/sienna
  5. Hero section renders as a dark band at the top (Option A) or light editorial hero (Option B)
  6. Hover states, buttons, links all use sienna accent
  7. No contrast failures visible
  8. No hardcoded violet bleeding through anywhere except hero (Option A)

- [ ] **Step 3: Verify dark mode**

  1. Click theme toggle
  2. Entire page swaps to aurora navy
  3. Glass cards visibly have backdrop blur and inset highlights
  4. Violet/mint gradients appear
  5. Hero section looks unchanged from pre-plan state
  6. All text remains readable

- [ ] **Step 4: Verify persistence**

  1. Reload page in dark mode → stays dark
  2. Close browser tab → reopen → stays dark
  3. Clear localStorage → reload → reverts to Decision 2 default

- [ ] **Step 5: Verify reduced motion**

  1. In DevTools: Rendering tab → Emulate CSS media feature prefers-reduced-motion → reduce
  2. Click theme toggle → colors snap instantly (no 200ms transition)

- [ ] **Step 6: Run build**

  ```bash
  npm run build && npm run preview
  ```

  Expected: build succeeds, preview at `http://localhost:4321` shows both themes working identically to dev mode.

- [ ] **Step 7: Final commit**

  ```bash
  git commit --allow-empty -m "test(theme): dual-theme smoke test passed"
  ```

---

## Self-Review

### Spec coverage
- ✅ Light mode = Palette A → Task 2 (`:root` tokens)
- ✅ Dark mode = Palette E → Task 2 (`[data-theme="dark"]` tokens)
- ✅ Theme toggle → Task 4 Step 3
- ✅ Persistence → Task 4 Step 3 (localStorage)
- ✅ FOUC prevention → Task 4 Steps 1-2 (inline blocking script)
- ✅ All components theme-aware → Task 5
- ✅ Hero treatment → Task 6 (Option A) or 6b (Option B)
- ✅ Glass effects per theme → Task 2 Step 4
- ✅ Gradient backgrounds per theme → Task 2 Step 6
- ✅ Accessibility (reduced motion) → Task 2 Step 7, Task 7 Step 5

### Open decisions require resolution before execution
- **Decision 1** (Hero) blocks Task 6
- **Decision 2** (default theme) blocks Task 4 Step 1
- **Decision 3** (typography) blocks Task 3
- **Decision 4** (transition) blocks Task 2 Step 7

---

## Total time estimate

| Task | Estimate |
|------|----------|
| 1. Hex audit | 20 min |
| 2. Theme token system | 60 min |
| 3. Typography decision | 10 min (3a) / 20 min (3b/3c) |
| 4. Toggle + init script | 45 min |
| 5. Component sweep | 90 min |
| 6. Hero (Option A) | 30 min |
| 6b. Hero (Option B) — alternative | 90 min |
| 7. Smoke test | 20 min |
| **Total (Option A path)** | **~4.5 hrs** |
| **Total (Option B path)** | **~6 hrs** |

## Execution handoff

This plan is saved. It is **not ready to execute** until the four open decisions are resolved.

When ready to execute, two options:

1. **Subagent-Driven** — dispatch a fresh subagent per task, review between tasks
2. **Inline Execution** — execute all tasks in one session with checkpoints

Note: `astro-site/` is a separate git repository — all commits land there, not in the parent project repo.
