# Changelog

All notable milestones and decisions for the Adobe Summit 2026 / AI Forte project.
Each entry includes the git commit hash where applicable.

---

## [2026-04-22] — Adobe Summit Day 3 — Two Certifications Earned

### Certifications passed at Summit 🎉

- **AD0-E712 Adobe Commerce Business Practitioner Professional** (Apr 20, 31/50 = 62%) — first cert
- **AD0-E555 Adobe Marketo Engage Professional** (Apr 22, 43/55 = 78%) — passed on 4th attempt after iterative study-guide refinement

### Exam attempt summary across 3 days (10 total attempts)

| Date | Exam | Score | Result |
|---|---|---|---|
| Apr 20 | AD0-E555 Marketo Pro (A1) | 31/55 (56%) | ❌ |
| Apr 20 | AD0-E137 AEM Developer **Expert** | 20/50 (40%) | ❌ (tier mismatch) |
| Apr 20 | **AD0-E712 Commerce BP** | 31/50 (62%) | ✅ |
| Apr 20 | AD0-E605 RTCDP Developer **Expert** | 22/68 (32%) | ❌ (tier mismatch) |
| Apr 20 | AD0-E911 Workfront PM Pro | 20/50 (40%) | ❌ |
| Apr 21 | AD0-E555 Marketo Pro (A2) | 33/55 (60%) | ❌ |
| Apr 21 | AD0-E559 Marketo BP **Expert** | 22/50 (44%) | ❌ (tier mismatch) |
| Apr 22 | AD0-E555 Marketo Pro (A3) | 35/55 (64%) | ❌ (1 short) |
| Apr 22 | **AD0-E555 Marketo Pro (A4)** | **43/55 (78%)** | **✅** |
| Apr 22 | AD0-E138 AEM Business Practitioner | 28/50 (56%) | ❌ (5 short) |

### Added

- `notes/exam-results/` — 10 detailed exam result writeups with section-level breakdowns, analysis, and retake guidance
- `notes/exam-flashcards/` — comprehensive study guides for Marketo, Analytics BP, Commerce FE Dev, Commerce Dev
  - `marketo.md` — iterative study guide that converted to pass (~800 lines)
    - Part 1: Triggers & Filters deep dive
    - Part 2: Program Cloning
    - Part 3: Period Costs & Budgets
    - Part 4: Engagement Programs (streams, transitions, exhausted)
    - Part 5: Channels & Progression Statuses
    - Part 6: Tokens (inheritance edge cases)
    - Part 7: Assets (Operational vs Regular emails)
    - Part 8: Reports
    - Part 9: Restrictions & "Cannot Do" Rules (segmentation, tokens, cloning, workspace)
    - Part 10: Known Exam Question Patterns (verbatim Q&A)
- `docs/plans/2026-04-22-cert-exam-gauntlet.md` — Day 3 exam scheduling + prep plan

### Lessons learned (confirmed patterns)

- **Professional / Business Practitioner tier** matches the user's background; **Expert / Developer** tier requires 1-2+ years hands-on in the specific product
- **Pacing discipline:** 35-45 minutes on a 100-110 min exam is the sweet spot. Under 25 min = rushed, losing easy points. Over 50 min = second-guessing.
- **Iterative study-guide iteration between retakes** delivered the Marketo pass. Each failed attempt informed the next study iteration.
- **Same-day retakes allowed with Summit vouchers** (regular Adobe policy is 15 days after second failure; Summit exception applied)
- **Decision fatigue is real** — 5 exams in 80 minutes caused pacing regression on exam #5 (AEM BP)

---

## [2026-04-20] — Project Reorganization: Brand Assets & Website Moved to `../AI Forte/` `4053885`

### Changed

- Moved `astro-site/` (its own git repo) → `../AI Forte/astro-site/`
- Moved `resources/` → `../AI Forte/assets/`
- Moved 6 brand/website plans → `../AI Forte/docs/plans/`
  - 2026-04-10-ai-forte-website-plan.md
  - 2026-04-14-astro-palette-a-migration.md
  - 2026-04-14-astro-dual-theme.md
  - 2026-04-14-logo-revisit.md
  - 2026-04-16-website-cleanup-seo.md
  - 2026-04-17-scroll-narrative-transformation.md

### Added

- `../AI Forte/CLAUDE.md` — brand-level context for future Claude Code sessions rooted in AI Forte directory
- `../AI Forte/README.md` — brand overview

### Rationale

Summit folder now focused on event prep only (CHANGELOG, BOARD, notes, session data, personal prep images). Brand + product work lives in its own directory at the sibling level. Astro site retains its own git history intact.

---

## [2026-04-17] — BOARD cleanup + Summit prep reality-check `deddfad`

Pre-departure trim of BOARD.md backlog (completed items removed) and updated `docs/plans/2026-04-10-revised-summit-preparation.md` with a "Current State — Reality Check (Apr 17)" section summarizing what had shipped before leaving for Vegas.

---

## [2026-04-13] — Git Init + Project Management Setup `b68e112`

### Added
- Initialized git repository for the project management / docs layer
- `BOARD.md` — kanban board for tracking all workstreams (30+ items across 6 labels)
- `CHANGELOG.md` — this file
- `.gitignore` — excludes `astro-site/` (separate repo), OS files, IDE files
- Pushed to origin: `github.com/akthechamp/adobe-summit-2026`

### Changed

### Architecture Decision
- **Two-repo setup:** This repo (`adobe-summit-2026`) covers planning, docs, learning resources, session data, notes, and project management. The `astro-site/` directory is a separate git repository for the AI Forte website (Astro 5 + React 19 + Tailwind 4). They live in the same parent directory but are tracked independently.

---

## [2026-04-10] — Revised Plan v2 + AI Forte Website Plan *(pre-git — included in `b68e112`)*

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

## [2026-04-10] — Curated Learning Resources *(pre-git — included in `b68e112`)*

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

## [2026-04-07] — Resource Curation Overhaul *(pre-git — included in `b68e112`)*

### Changed
- Main plan updated to reference curated resources document instead of inline vague links
- All "Search YouTube for X" replaced with specific channel names and URLs
- Certification exam sections updated with accurate pass scores and section weights

---

## [2026-04-06] — Project Inception *(pre-git — included in `b68e112`)*

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
