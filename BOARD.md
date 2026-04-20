# Project Board

> Kanban-style project board for Adobe Summit 2026 / AI Forte preparation.
> Move items between columns by cutting/pasting. Update status emoji as you go.
>
> **Columns:** Backlog → In Progress → Done
> **Labels:** `[LEARN]` `[SITE]` `[BRAND]` `[CERT]` `[NETWORK]` `[OPS]`

---

## Backlog

**Reordered Apr 17** — top 12 are departure-blockers in execution order. See [Reality Check in the revised plan](docs/plans/2026-04-10-revised-summit-preparation.md#current-state--reality-check-apr-17).

### P0 — Ship today before departure (in order)
- [ ] `[SITE]` **DEPLOY** astro-site to Vercel — whatever state, ship it *(30–45 min)*
- [ ] `[CERT]` Book both exam slots at Summit (AD0-E712 + AD0-E555) — target Wed Apr 22 *(15 min)*
- [ ] `[NETWORK]` Book priority labs — L817, L815, L335, L816, L821, L223, L320, L321 *(20 min)*
- [ ] `[BRAND]` LinkedIn overhaul — banner upload, headline, About, skills, Featured, QR *(45 min)*
- [ ] `[BRAND]` Digital business card setup (Blinq free) with live site URL + Calendly *(20 min)*
- [ ] `[OPS]` Calendly setup — "AI Forte — 20-min Summit Follow-up" *(15 min)*
- [ ] `[BRAND]` One-pager PDF — Canva using `resources/one-pager/ai-forte-one-pager-header-1.jpg` + AI Forte structure from plan Task 16A Step 2 *(45 min)*
- [ ] `[OPS]` NotebookLM — Commerce + Marketo notebooks, Audio Overviews, **download MP3 to phone** *(40 min)*
- [ ] `[OPS]` Lead capture Google Sheet *(15 min)*
- [ ] `[OPS]` Follow-up email templates — 3 drafts in Gmail *(30 min)*
- [ ] `[NETWORK]` Pre-Summit LinkedIn post with live site URL *(15 min)*
- [ ] `[OPS]` **Flight content pack** — Udemy offline, TED playlist, cert prep PDFs, NotebookLM audio, AI Forte cheat sheet — **before leaving home wifi** *(30–45 min)*
- [ ] `[OPS]` Final pitch practice — 10-sec / 30-sec / problem-solver, out loud 3× each *(15 min)*
- [ ] `[OPS]` Physical pack — laptop, charger, battery, shoes, layers, notepad *(15 min)*

### P1 — Drop if time-crunched
- [ ] `[OPS]` NotebookLM third notebook (AI Agents) *(10 min)*
- [ ] `[SITE]` Contact form wiring (Formspree) *(30 min)*
- [ ] `[SITE]` Scroll-narrative Phase B (Ch 3–6) — `docs/plans/2026-04-17-scroll-narrative-transformation.md` *(multi-hour)*
- [ ] `[NETWORK]` Join Adobe Summit community forum *(10 min)*
- [ ] `[LEARN]` AI Forte cheat sheet — `notes/ai-forte-cheat-sheet.md` *(30 min)*

### Flight / Vegas (defer to travel time)
- [ ] `[LEARN]` TED Talks — 10 sales + persuasion talks *(2.5 hrs on flight)*
- [ ] `[CERT]` Commerce cert practice — EDUSUM + Udemy *(flight)*
- [ ] `[CERT]` Marketo cert practice — EDUSUM + Udemy *(flight)*
- [ ] `[LEARN]` AEM Basics (Bortnikov) — 1.5× speed *(flight)*

---

## In Progress

Items currently being worked on.

*(move items here as you start them)*

---

## Done

Completed items. Add date when moved here.

- [x] `[OPS]` Project inception + first plan (Apr 6)
- [x] `[OPS]` Session parsing — 325 sessions organized (Apr 6)
- [x] `[OPS]` Curated learning resources document (Apr 7)
- [x] `[OPS]` Revised plan v2 — AI Forte pivot, NotebookLM, daily collateral (Apr 10)
- [x] `[SITE]` Website plan created — superseded in practice by scroll-narrative + cleanup-SEO plans (Apr 10)
- [x] `[OPS]` Git repo initialized + BOARD + CHANGELOG (Apr 13, `b68e112`)
- [x] `[LEARN]` Foundation (partial) — ecosystem overview started (Apr 6-9)
- [x] `[BRAND]` Palette A (Warm Premium) locked with decision record (Apr 14, `5ec0b1a`)
- [x] `[BRAND]` All 9 AI Forte brand assets generated via Nano Banana Pro in Palette A — logo, icon, LinkedIn banner, OG, social post, summit announcement, business card, one-pager header, headshot (Apr 14, `c1b3be3`)
- [x] `[SITE]` Website SEO/AEO audit + Terms/Privacy + canonical/OG/JSON-LD + llms.txt + UTM attribution (Apr 17, `2026-04-16-website-cleanup-seo.md`)
- [x] `[SITE]` Honest content pass — removed fake testimonials, unverified compliance claims, dead footer links (Apr 17)
- [x] `[SITE]` Scroll-narrative Phase A — Ch 1 Hook + Ch 2 Problem + chapter lib + reduced-motion (Apr 17)
- [x] `[SITE]` Dark mode dropped, dual-theme plan superseded (`f0699cd`)
- [x] `[LEARN]` AEM foundation (merged with broader research)
- [x] `[LEARN]` Commerce foundation (merged)
- [x] `[LEARN]` Marketo foundation (merged)

---

## Blocked

Items that can't proceed until a dependency is resolved.

*(nothing currently blocked)*

---

## Notes on Using This Board

### Daily Workflow
1. Open `BOARD.md` at the start of each day
2. Check the [revised plan](docs/plans/2026-04-10-revised-summit-preparation.md) for today's scheduled tasks
3. Move those items from **Backlog** → **In Progress**
4. Work through them
5. When done, move to **Done** with the date
6. Commit the board update: `git add BOARD.md && git commit -m "board: update progress"`

### How Items Map to Plans
Each `[SITE]` task references a numbered task in `docs/plans/2026-04-10-ai-forte-website-plan.md`.
Each `[LEARN]`, `[CERT]`, `[BRAND]`, `[NETWORK]`, `[OPS]` task references a step in `docs/plans/2026-04-10-revised-summit-preparation.md`.

### Labels
| Label | Meaning |
|-------|---------|
| `[LEARN]` | Adobe ecosystem learning (courses, videos, NotebookLM) |
| `[SITE]` | AI Forte website implementation |
| `[BRAND]` | Branding collateral (LinkedIn, logo, one-pager, digital card) |
| `[CERT]` | Certification exam prep |
| `[NETWORK]` | Networking strategy, session scheduling, community |
| `[OPS]` | Setup, tools, systems (NotebookLM, Calendly, lead sheet, packing) |

### Recommended Daily Mapping (Apr 13-17)

| Day | Pick from Backlog |
|-----|-------------------|
| **Apr 13** | `[LEARN]` AEM foundation + `[SITE]` Task 5 (Summit page) + `[OPS]` NotebookLM setup |
| **Apr 14** | `[CERT]` Both cert preps + `[SITE]` Tasks 6+8+9 |
| **Apr 15** | `[CERT]` Practice exams + `[BRAND]` Gemini 3 assets + `[BRAND]` LinkedIn overhaul + `[SITE]` Task 7 |
| **Apr 16** | `[SITE]` Task 10 (DEPLOY) + `[BRAND]` One-pager + `[OPS]` Lead sheet + Calendly + `[NETWORK]` Session schedule + LinkedIn post + `[LEARN]` TED Talks |
| **Apr 17** | `[OPS]` Flight pack download + pitch practice + pack + depart |
