# Resources — AI Forte Brand Assets

All final brand assets for AI Forte, generated with **Nano Banana Pro** (`google/gemini-3-pro-image-preview`) via OpenRouter, using the locked **Palette A (Warm Premium)** from [`brand-system.md`](./brand-system.md).

## Asset index

### Logo (`logo/`)
| File | Type | Use |
|------|------|-----|
| `ai-forte-logo.png` | Primary wordmark lockup (2K) | Website header, one-pager, email signature, press |
| `ai-forte-icon.png` | Icon only, 1:1 square (1K) | Favicon, profile pic, app icon, small accents |

### LinkedIn (`linkedin/`)
| File | Use |
|------|-----|
| `ai-forte-linkedin-banner.png` | LinkedIn profile cover banner (4:1 wide, 2K) |

### OG Image (`og/`)
| File | Use |
|------|-----|
| `ai-forte-og-image-1.jpg` | Primary Open Graph image (16:9) |
| `ai-forte-og-image-2.jpg` | Alternate Open Graph variation |

### Social Media (`social/`)
| File | Use |
|------|-----|
| `ai-forte-post-template-1.jpg` | Reusable square post background — add headline overlay in Canva/Figma |
| `ai-forte-post-template-2.jpg` | Alternate template variation |
| `ai-forte-summit-announcement-1.jpg` | "See you in Vegas" Summit announcement post (16:9) |
| `ai-forte-summit-announcement-2.jpg` | Alternate announcement variation |

### Business Card (`business-card/`)
| File | Use |
|------|-----|
| `ai-forte-business-card-1.jpg` | Digital business card cover (9:16 portrait, Blinq/Popl) — add contact overlay in app |
| `ai-forte-business-card-2.jpg` | Alternate card variation |

### One-Pager (`one-pager/`)
| File | Use |
|------|-----|
| `ai-forte-one-pager-header-1.jpg` | Wide hero banner for top of one-pager PDF (3:1, 2K) |
| `ai-forte-one-pager-header-2.jpg` | Alternate header variation |

### Headshot (`headshot/`)
| File | Use |
|------|-----|
| `ashish-headshot-warm.png` | Founder headshot with warm cream background (edited from `../../ashish-pic.JPG`, 4:5 portrait) |
| `README.md` | Original Gemini prompt reference (historical) |

### Brand System & Decision Trail
| File | Purpose |
|------|---------|
| `brand-system.md` | Locked brand spec — colors, typography, logo rules, component primitives, voice |
| `generation-plan.md` | All 9 prompts used for generation, organized by asset |
| `palette-samples/` | Historical research trail — decision record, 5-palette HTML preview, prompt candidates |

## Generation details

- **Model:** `google/gemini-3-pro-image-preview` (Nano Banana Pro)
- **Access:** OpenRouter API via skill `nano-banana-pro-openrouter`
- **Command:** `uv run ~/.claude/skills/nano-banana-pro-openrouter/scripts/generate_image.py --prompt ... --filename ... --resolution 1K|2K`
- **Date:** 2026-04-14
- **Palette:** A — Warm Premium (cream #F8F3EC, espresso #2C1810, sienna #C65D2E, taupe #8B7355, cream border #E8DDD0)

## Regenerating an asset

If any asset needs iteration, find its prompt in [`generation-plan.md`](./generation-plan.md), tweak the prompt, and rerun the same script command. Composition (aspect ratio) is described in the prompt text — Nano Banana Pro respects it reliably when specified clearly.

## What's NOT here

- **Real client case studies / testimonials** — still needed, not AI-generatable
- **Calendly link** — needs manual setup at calendly.com
- **Custom domain for astro-site** — needs purchase + DNS
- **Physical print finishing** — sent to print vendor with these assets as source
