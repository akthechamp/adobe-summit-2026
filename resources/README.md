# Resources — AI Forte Brand Assets

All brand assets, collateral templates, and image generation prompts for AI Forte / Adobe Summit 2026.

## How to Use

**HTML assets** → open in browser → screenshot at the specified dimensions (or Cmd+P → Save as PDF for the one-pager). Each file has the target dimensions in its `<title>` tag and CSS comments.

**SVG assets** → use directly in the website, Canva, InDesign, or any design tool. They scale to any size.

**Gemini prompts** → copy from `prompts/gemini-3-all-prompts.md`, paste into Gemini 3 (Nano Banana Pro) for higher-fidelity raster versions.

## Asset Index

### Logo (`logo/`)
| File | Format | Usage |
|------|--------|-------|
| `ai-forte-logo.svg` | SVG | Website header, one-pager, email sig — dark text on light bg |
| `ai-forte-logo-white.svg` | SVG | Dark backgrounds (banners, cards, social) — white text |
| `ai-forte-icon.svg` | SVG | Favicon, app icon, profile picture, small accents |
| `logo-wordmark-option-a-nodes.svg` | SVG | Alt logo — triangular node network + wordmark |
| `logo-wordmark-option-b-monogram.svg` | SVG | Alt logo — monogram style + wordmark |
| `logo-wordmark-option-c-flow.svg` | SVG | Alt logo — flow/wave style + wordmark |
| `icon-option-a-nodes.svg` | SVG | Alt icon — triangular node network |
| `icon-option-b-monogram.svg` | SVG | Alt icon — monogram |
| `icon-option-c-flow.svg` | SVG | Alt icon — flow/wave |

### LinkedIn (`linkedin/`)
| File | Format | Dimensions | Usage |
|------|--------|-----------|-------|
| `banner.html` | HTML | 1584 x 396 | Open in browser, screenshot, upload to LinkedIn cover photo |
| `linkedin-banner-clean.png` | PNG | 1584 x 396 | Pre-rendered banner — clean version (no text overlay) |
| `linkedin-banner-with-text.png` | PNG | 1584 x 396 | Pre-rendered banner — with headline text |

### OG Image (`og/`)
| File | Format | Dimensions | Usage |
|------|--------|-----------|-------|
| `og-image.html` | HTML | 1200 x 630 | Screenshot → save as `og-image.png` → put in `astro-site/public/` |

### Social Media (`social/`)
| File | Format | Dimensions | Usage |
|------|--------|-----------|-------|
| `summit-announcement.html` | HTML | 1200 x 628 | LinkedIn/Twitter post announcing Summit attendance |
| `post-template.html` | HTML | 1080 x 1080 | Reusable template — edit the headline for each post |
| `social-post-template-clean.png` | PNG | 1080 x 1080 | Pre-rendered social template — background only |
| `social-post-template-with-text.png` | PNG | 1080 x 1080 | Pre-rendered social template — with sample text |

### Business Card (`business-card/`)
| File | Format | Dimensions | Usage |
|------|--------|-----------|-------|
| `digital-card-cover.html` | HTML | 1080 x 1920 | Screenshot → upload to Blinq/Popl as cover image |
| `business-card-clean.png` | PNG | 1080 x 1920 | Pre-rendered card — clean version |
| `business-card-with-text.png` | PNG | 1080 x 1920 | Pre-rendered card — with contact details |

### One-Pager (`one-pager/`)
| File | Format | Usage |
|------|--------|-------|
| `ai-forte-one-pager.html` | HTML (A4) | Open in browser → Cmd+P → Save as PDF → share at Summit |
| `one-pager-header-clean.png` | PNG | Pre-rendered header banner — background only |
| `one-pager-header-with-text.png` | PNG | Pre-rendered header banner — with title text |

### Headshot (`headshot/`)
| File | Format | Usage |
|------|--------|-------|
| `README.md` | Guide | Gemini 3 prompt for professional background replacement of `ashish-pic.jpg` |

### Prompts (`prompts/`)
| File | Format | Usage |
|------|--------|-------|
| `gemini-3-all-prompts.md` | Markdown | All 8 Gemini 3 prompts consolidated — copy-paste ready |

## Brand System

| Element | Value |
|---------|-------|
| **Primary** | Deep Midnight Navy `#0A1628` |
| **Accent 1** | Electric Indigo `#5B5BFF` |
| **Accent 2** | Vibrant Coral `#FF5B5B` |
| **Text (light bg)** | `#0A1628` |
| **Text (dark bg)** | `#FFFFFF` / `rgba(255,255,255,0.55)` |
| **Font** | Inter (700/800 for headlines, 400/500 for body) |
| **Motif** | Interconnected orchestration nodes — network pattern |
| **Archetypes** | Stripe, Linear, Vercel, Palantir |

## Quick Screenshot Guide

For HTML → PNG conversion at exact dimensions:

**Option A — Browser DevTools:**
1. Open the HTML file in Chrome
2. Cmd+Opt+I → toggle device toolbar (Cmd+Shift+M)
3. Set custom dimensions to match the file (e.g., 1584x396 for banner)
4. Right-click → "Capture screenshot" or Cmd+Shift+P → "Capture full size screenshot"

**Option B — CLI (requires Puppeteer or Playwright):**
```bash
npx playwright screenshot banner.html banner.png --viewport-size=1584,396
```

**Option C — macOS Screenshot:**
1. Open HTML, zoom browser to 100%
2. Cmd+Shift+4 → drag to select the exact area
