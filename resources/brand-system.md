# AI Forte Brand System — Locked Spec

**Palette:** Warm Premium (A) — locked 2026-04-14
**Decision record:** [`palette-samples/DECISION.md`](./palette-samples/DECISION.md)

This is the single source of truth for AI Forte brand colors, typography, and visual language. Use these values in every asset: website, logo, LinkedIn banner, one-pager, business card, social posts.

---

## Colors

### Core palette
```
Warm cream        #F8F3EC    rgb(248, 243, 236)   → backgrounds, canvas
Deep espresso     #2C1810    rgb(44, 24, 16)      → body text, wordmark
Burnt sienna      #C65D2E    rgb(198, 93, 46)     → primary accent, CTAs, "AI" in wordmark
Warm taupe        #8B7355    rgb(139, 115, 85)    → muted text, metadata
Cream border      #E8DDD0    rgb(232, 221, 208)   → borders, dividers, subtle surfaces
```

### Extended system (for components, states, data viz)
```
Soft sienna       #D97845    → hover state on sienna CTAs (10% lighter)
Deep sienna       #A84820    → pressed state, focus rings (10% darker)
Surface cream     #FEFCF8    → card backgrounds (1% lighter than core cream)
Warm shadow       rgba(44, 24, 16, 0.08)  → drop shadows, elevation
```

### Usage rules
- **Never** use sienna at <50% opacity on cream — it reads dirty. Use taupe instead.
- **Never** use pure white. Cream (`#F8F3EC`) is the lightest surface.
- **Never** use pure black. Espresso (`#2C1810`) is the darkest text.
- Body text must be espresso at full opacity for WCAG AA.
- CTA buttons: solid sienna bg + cream text. Outline CTAs: transparent bg + espresso border + espresso text.
- Headlines: espresso. Accent moments within headlines: sienna.

---

## Typography

- **Primary typeface:** Inter (Google Fonts, 100-900 weights)
- **Fallback:** `-apple-system, BlinkMacSystemFont, "SF Pro Display", "Helvetica Neue", sans-serif`
- **Hero headlines:** Inter 800 / 44-56px / -1px letter-spacing / 1.1 line-height
- **Section headings:** Inter 700 / 28-36px / -0.5px letter-spacing / 1.2 line-height
- **Body text:** Inter 400 / 15-17px / 0 letter-spacing / 1.6 line-height
- **Small / metadata:** Inter 500 / 11-13px / 0.2px letter-spacing / 1.4 line-height
- **Wordmark "AI Forte":** Inter 800 condensed feel, -0.8px letter-spacing

---

## Logo System

The AI Forte logo is a **wordmark + orchestration icon lockup**. Existing SVGs in `resources/logo/` use the old (navy/indigo) palette and need to be re-generated with palette A colors:

- [ ] `ai-forte-logo.svg` — primary wordmark (espresso + sienna accent) on cream
- [ ] `ai-forte-logo-white.svg` — N/A for palette A (no dark-background variant needed; if used on sienna, use all-cream)
- [ ] `ai-forte-icon.svg` — icon only (sienna nodes + espresso central) on cream

### Icon construction rules
- Central orchestrator node: solid sienna, 9px radius (at 64×64 base)
- Satellite nodes: 4 nodes at varying radii (4.5-6px), sienna with opacity variation (0.5-0.8)
- Connection lines: sienna, 1.8px stroke, opacity 0.3-0.4
- Inner central ring: espresso (4.5px) + sienna core (2.8px)

---

## Voice & Visual Language

- **Warm but confident** — not chilly tech, not fluffy design studio
- **Editorial, not corporate** — think Kinfolk magazine layouts, not pitch decks
- **Craft signals over technical signals** — show thoughtfulness, not just capability
- **No gradients, no glow, no 3D** — flat color, generous whitespace, strong type
- **Minimal decoration** — let the wordmark and the network motif do the work

### Visual moves to use
- Generous whitespace (never crowded)
- Tight headline tracking (negative letter-spacing)
- Serif-less but bold typography
- Single accent color (sienna) used sparingly
- Hairline borders in cream-border tone
- Subtle paper grain texture on backgrounds (optional, adds warmth)

### Visual moves to avoid
- Dark mode / dark backgrounds
- Neon, glow, or gradients
- Isometric 3D (unless hybrid flourish on astro-site hero — see DECISION.md)
- Multiple accent colors
- Stock photography of teams / handshakes / brains
- Glass morphism / backdrop blur

---

## Component Primitives

### Button — Primary (CTA)
```
background: #C65D2E
color: #F8F3EC
padding: 14px 24px
border-radius: 10px
font-weight: 600
font-size: 14px
hover: background #D97845
```

### Button — Secondary (outline)
```
background: transparent
color: #2C1810
border: 1px solid #2C1810
padding: 14px 24px
border-radius: 10px
font-weight: 600
font-size: 14px
hover: background rgba(44, 24, 16, 0.05)
```

### Badge / pill
```
background: rgba(198, 93, 46, 0.12)
color: #C65D2E
padding: 8px 16px
border-radius: 100px
font-weight: 600
font-size: 12px
```

### Card
```
background: #FEFCF8
border: 1px solid #E8DDD0
border-radius: 14px
padding: 24px
shadow: 0 2px 16px rgba(44, 24, 16, 0.06)
```

### Stat / metric display
```
value: Inter 800, 32-48px, color #C65D2E (sienna for emphasis)
label: Inter 500, 11-13px, color #8B7355 (taupe)
```

---

## Implementation Status

| Asset | Status |
|-------|--------|
| `brand-system.md` | ✅ Locked |
| `palette-samples/DECISION.md` | ✅ Documented |
| `resources/logo/ai-forte-logo.svg` | ⏳ Needs regeneration in palette A |
| `resources/logo/ai-forte-icon.svg` | ⏳ Needs regeneration in palette A |
| `resources/linkedin/banner.html` | ⏳ Needs palette A repaint |
| `resources/og/og-image.html` | ⏳ Needs palette A repaint |
| `resources/social/post-template.html` | ⏳ Needs palette A repaint |
| `resources/social/summit-announcement.html` | ⏳ Needs palette A repaint |
| `resources/business-card/digital-card-cover.html` | ⏳ Needs palette A repaint |
| `resources/one-pager/ai-forte-one-pager.html` | ⏳ Needs palette A repaint |
| `resources/headshot/` | ⏳ Needs bg replacement (palette A cream gradient) |
| `astro-site/` theme | ⏳ Needs palette A application |
