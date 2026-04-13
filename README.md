# Adobe Summit 2026 — AI Forte

> Preparation hub for Adobe Summit 2026 (April 19-22, Las Vegas). Learning, certifications, collateral, website, networking — everything needed to launch **AI Forte** as an AI Orchestrator Agency at Adobe's flagship event.

## Status

| Area | Status | Notes |
|------|--------|-------|
| **Active Plan** | `docs/plans/2026-04-10-revised-summit-preparation.md` | 7-day sprint + flight content |
| **Website** | `astro-site/` — in progress | Astro 5 + React 19 + Tailwind 4 |
| **Website Plan** | `docs/plans/2026-04-10-ai-forte-website-plan.md` | 11 tasks, ~5.5 hrs |
| **Certifications** | Studying | AD0-E712 (Commerce) + AD0-E555 (Marketo) |
| **LinkedIn** | Pending overhaul | Templates ready in plan |
| **Collateral** | Daily shipping | Logo, banner, one-pager, digital card |
| **Event** | April 19-22 | The Venetian, Las Vegas |

---

## Quick Start

```bash
# This repo: project management, plans, docs, learning resources
git log --oneline -5              # see recent progress
cat BOARD.md                       # see kanban board

# AI Forte website (SEPARATE REPO in sibling directory)
cd astro-site && npm install && npm run dev
# Opens at http://localhost:4321
```

**Follow the plan:** Open `docs/plans/2026-04-10-revised-summit-preparation.md` and work through today's tasks. Each day has a Learning block + Collateral Ship block + NotebookLM parallel block.

**Track progress:** See `BOARD.md` for the kanban board and `CHANGELOG.md` for full history.

## Repository Architecture

**Two separate repos** — they share a parent directory but are tracked independently.

| Repo | Purpose | Path |
|------|---------|------|
| **adobe-summit-2026** (this repo) | Project management, plans, docs, learning resources, session data, notes | `.` |
| **ai-forte-website** (separate repo) | AI Forte marketing site (Astro 5 + React 19 + Tailwind 4) | `astro-site/` |

The `.gitignore` in this repo excludes `astro-site/` entirely. Commits to the website are tracked in the astro-site repo. This repo tracks plans, board state, learning progress, and project decisions.

---

## What Is AI Forte

**AI Forte = an AI Orchestrator Agency.** We design and ship coordinated multi-agent systems on Adobe Experience Cloud — Commerce, Marketo, AEM, Journey Optimizer, Agent Orchestrator. 20-person build team (developers + designers). Based on a decade of Magento, HubSpot, and frontend development experience.

**Summit 2026 alignment:** Adobe's dominant theme this year is agentic AI. Every keynote and track is about Agent Orchestrator, Brand Concierge, Agentic Web. AI Forte positions directly into this narrative.

---

## Profile

**Ashish Kumar** — Founder & CEO
- 20-person agency (developers + designers)
- Core: Frontend, Ecommerce (Shopify, Adobe Commerce/Magento), Marketing Automation (HubSpot, Marketo), CRM, Web & Mobile
- Adobe: Commerce (prior Magento), Marketo (learning via HubSpot crossover), AEM (new), Creative Cloud
- Target clients: SMBs & mid-market

---

## Objectives

| # | Objective | Target |
|---|-----------|--------|
| 1 | Pass Adobe Commerce cert (AD0-E712) | Free at Summit |
| 2 | Pass Adobe Marketo cert (AD0-E555) | Free at Summit |
| 3 | Collect qualified contacts | 20+ |
| 4 | Identify hot leads | 5+ |
| 5 | Find referral partners | 3+ |
| 6 | Ship AI Forte website live | Before Apr 17 |
| 7 | LinkedIn profile overhauled | Before Apr 17 |
| 8 | One-pager PDF ready | Before Apr 17 |
| 9 | Post-Summit follow-ups sent | Within 48 hrs |

---

## Project Structure

```
.                                       # ── This repo: adobe-summit-2026 ──
├── README.md                           # Project overview (this file)
├── CHANGELOG.md                        # Full project history
├── BOARD.md                            # Kanban board — project management
├── .gitignore                          # Excludes astro-site/ (separate repo)
│
├── docs/
│   ├── curated-learning-resources.md   # All courses, videos, links (named, with URLs)
│   └── plans/
│       ├── 2026-04-06-adobe-summit-preparation.md   # v1 — original plan (archived)
│       ├── 2026-04-10-revised-summit-preparation.md # v2 — ACTIVE: 7-day sprint
│       └── 2026-04-10-ai-forte-website-plan.md      # Website impl plan (11 tasks)
│
├── notes/                              # Personal study notes
├── sessions-parsed.md                  # 325 Summit sessions parsed
├── adobe-sessions.html                 # Raw session HTML source (3.4MB)
├── summit-exams.png                    # Certification exams screenshot
└── linkedin-profile.png                # Current LinkedIn profile snapshot

astro-site/                             # ── Separate repo: ai-forte-website ──
├── src/                                # (has its own .git, tracked independently)
│   ├── pages/                          # index.astro, adobe-summit.astro
│   ├── components/{astro,react,ui}/    # All UI components
│   ├── data/                           # Typed data (services, cases, FAQ, etc.)
│   ├── layouts/                        # BaseLayout.astro
│   └── lib/                            # GSAP init, animations
├── public/                             # Logo, favicon, OG image
└── package.json                        # Astro 5, React 19, Tailwind 4, GSAP
```

---

## Plans Reference

| Plan | Purpose | Status |
|------|---------|--------|
| [Revised Summit Prep (v2)](docs/plans/2026-04-10-revised-summit-preparation.md) | Master plan: daily schedule, AI Forte positioning, NotebookLM, cert prep, TED Talks, Gemini 3 prompts, session strategy, networking, lead capture | **ACTIVE** |
| [AI Forte Website Plan](docs/plans/2026-04-10-ai-forte-website-plan.md) | 11-task website implementation: services rewrite, hero, Summit landing page, Adobe section, deploy | **ACTIVE** |
| [Curated Learning Resources](docs/curated-learning-resources.md) | All Udemy courses, Adobe free training, YouTube channels, practice exams — specific names + URLs | Reference |
| [Original Summit Prep (v1)](docs/plans/2026-04-06-adobe-summit-preparation.md) | First plan created Apr 6, 11-day timeline — superseded by v2 | Archived |

---

## Event Details

| Detail | Info |
|--------|------|
| Event | Adobe Summit 2026 — The Digital Experience Conference |
| Dates | April 19-22, 2026 (Sun preconference → Wed) |
| Venue | The Venetian Convention and Expo Center, Las Vegas |
| Pass | Full Conference Pass |
| Departure | Evening of April 17 |
| Sessions | 325 total — parsed in `sessions-parsed.md` |
| Certifications | 9 available — targeting Commerce (AD0-E712) + Marketo (AD0-E555) |
