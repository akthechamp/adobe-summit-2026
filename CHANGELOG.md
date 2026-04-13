# Changelog

All notable milestones and decisions for the Adobe Summit 2026 / AI Forte project.

---

## [2026-04-13] — Git Init + Project Management Setup

### Added
- Initialized git repository for the project management / docs layer
- `BOARD.md` — kanban board for tracking all workstreams
- `CHANGELOG.md` — this file
- `.gitignore` — excludes `astro-site/` (separate repo), OS files, IDE files

### Changed
- `README.md` — rewritten as proper project README with status table, quick start, structure, and plans reference

### Architecture Decision
- **Two-repo setup:** This repo covers planning, docs, learning resources, session data, notes, and project management. The `astro-site/` directory is a separate git repository for the AI Forte website (Astro 5 + React 19 + Tailwind 4). They live in the same parent directory but are tracked independently.

---

## [2026-04-10] — Revised Plan v2 + AI Forte Website Plan

### Added
- `docs/plans/2026-04-10-revised-summit-preparation.md` — compressed 7-day sprint plan replacing the original 11-day plan
- `docs/plans/2026-04-10-ai-forte-website-plan.md` — 11-task website implementation plan for repositioning the existing astro-site
- NotebookLM integration — 3 notebooks (Commerce, Marketo, AI Agents) with Audio Overview strategy
- 10 curated TED Talks / sales talks with direct URLs
- 8 Gemini 3 (Nano Banana Pro) image generation prompts for brand assets
- Daily Collateral Ship Tracker — parallel learning + shipping structure
- Flight Content Pack — hour-by-hour plan for offline learning during travel

### Changed
- Daily structure changed from sequential (learn → then collateral) to **parallel** (learn + ship every day)
- Certification exam details corrected: AD0-E712 is 50 questions/100 min/60% pass; AD0-E555 is 55 questions/110 min/65% pass

### Decisions
- **AI Forte positioning adopted** — agency repositioned as "AI Orchestrator Agency" for Summit
- AI Forte aligns directly with Adobe Summit 2026's dominant "agentic AI" theme
- Existing agency capabilities (Commerce, Marketo, AEM, frontend, CRM) become the execution layer under the AI Forte brand
- Session priority shifted to agent-heavy sessions (L815, L816, L817, L335, L821)

---

## [2026-04-10] — Curated Learning Resources

### Added
- `docs/curated-learning-resources.md` — replaced vague "search YouTube" suggestions with specific named resources
  - 4 Udemy courses for Commerce (1 free, 3 paid)
  - 6 Udemy courses for Marketo (2 free, 4 paid)
  - 4 Udemy courses for AEM
  - 8 Adobe official free training resources
  - 9 YouTube channels (Max Pronko, Mark Shust, Automation Geeks, Joe Reitz, AEM Geeks, etc.)
  - EDUSUM practice questions for both certification exams
  - HubSpot ↔ Marketo migration guides

---

## [2026-04-07] — Resource Curation Overhaul

### Changed
- Main plan updated to reference curated resources document instead of inline vague links
- All "Search YouTube for X" replaced with specific channel names and URLs
- Certification exam sections updated with accurate pass scores and section weights

---

## [2026-04-06] — Project Inception

### Added
- `docs/plans/2026-04-06-adobe-summit-preparation.md` — original 11-day preparation plan (now superseded)
- `sessions-parsed.md` — 325 Summit sessions parsed from `adobe-sessions.html`, organized by product area
- `summit-exams.png` — screenshot of certification exams available at Summit
- `README.md` — initial project profile and goals

### Context
- First-time Adobe Summit attendee
- Agency with ~20 developers + designers
- Strong HubSpot + Magento background, new to broader Adobe ecosystem
- Goal: generate leads and customers at Summit
- Full conference pass, departing evening April 17
- No existing Adobe ecosystem network
