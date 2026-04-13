# Project Board

> Kanban-style project board for Adobe Summit 2026 / AI Forte preparation.
> Move items between columns by cutting/pasting. Update status emoji as you go.
>
> **Columns:** Backlog → In Progress → Done
> **Labels:** `[LEARN]` `[SITE]` `[BRAND]` `[CERT]` `[NETWORK]` `[OPS]`

---

## Backlog

Items ready to be picked up. Ordered by priority (top = highest).

- [ ] `[SITE]` Task 1: Rewrite services data for Adobe ecosystem — `src/data/services.ts` *(30 min)*
- [ ] `[SITE]` Task 2: Rewrite hero section — `HeroSection.astro` *(25 min)*
- [ ] `[SITE]` Task 3: Case studies — honest relabeling *(20 min)*
- [ ] `[SITE]` Task 4: Adobe Ecosystem section — new component + data *(45 min)*
- [ ] `[SITE]` Task 5: `/adobe-summit` landing page *(60 min)*
- [ ] `[SITE]` Task 6: Summit banner + navbar link *(20 min)*
- [ ] `[SITE]` Task 8: TrustedBy → tech stack logos *(20 min)*
- [ ] `[SITE]` Task 9: Testimonials audit *(15 min)*
- [ ] `[BRAND]` Task 7: Generate logo, favicon, OG image via Gemini 3 *(30 min)*
- [ ] `[SITE]` Task 10: Deploy to Vercel *(30 min)*
- [ ] `[SITE]` Task 11: Wire contact form (Formspree) *(30 min — optional)*
- [ ] `[BRAND]` LinkedIn overhaul — banner, headline, About, skills, Featured, QR code *(90 min)*
- [ ] `[BRAND]` One-pager PDF — design + export *(45 min)*
- [ ] `[BRAND]` Digital business card setup (Blinq/Popl) *(15 min)*
- [ ] `[LEARN]` Commerce foundation — Udemy + Adobe tutorials + NotebookLM *(90 min)*
- [ ] `[LEARN]` Marketo foundation — Udemy + Adobe + HubSpot↔Marketo mapping *(90 min)*
- [ ] `[LEARN]` AEM foundation — Udemy/CloudFoundation + Edge Delivery *(90 min)*
- [ ] `[LEARN]` AI Agent Orchestration — Deloitte, Kanerika, Adobe agent landscape *(60 min)*
- [ ] `[LEARN]` AI Forte cheat sheet — write `notes/ai-forte-cheat-sheet.md` *(30 min)*
- [ ] `[CERT]` Commerce cert prep — prep guide + EDUSUM practice test *(90 min)*
- [ ] `[CERT]` Marketo cert prep — prep guide + EDUSUM practice test *(90 min)*
- [ ] `[CERT]` Book both exam slots at Summit *(15 min)*
- [ ] `[OPS]` NotebookLM setup — 3 notebooks + populate sources + generate Audio Overviews *(20 min)*
- [ ] `[OPS]` Calendly setup — "AI Forte 20-min Summit Follow-up" *(15 min)*
- [ ] `[OPS]` Lead capture Google Sheet setup *(15 min)*
- [ ] `[OPS]` Follow-up email templates — 3 drafts saved in Gmail *(30 min)*
- [ ] `[NETWORK]` Session schedule — register for priority labs and sessions *(45 min)*
- [ ] `[NETWORK]` Pre-Summit LinkedIn post with site URL *(15 min)*
- [ ] `[NETWORK]` Join Adobe Summit community forum *(10 min)*
- [ ] `[LEARN]` TED Talks — watch/listen 10 sales + persuasion talks *(2.5 hrs — can split)*
- [ ] `[OPS]` Flight content pack — download all content to phone before wifi cutoff *(30 min)*
- [ ] `[OPS]` Physical pack checklist — laptop, charger, battery, shoes *(15 min)*
- [ ] `[OPS]` Final pitch practice — 3 versions out loud *(15 min)*

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
- [x] `[SITE]` Website plan created — 11 tasks mapped to daily schedule (Apr 10)
- [x] `[OPS]` Git repo initialized + BOARD + CHANGELOG (Apr 13)
- [x] `[LEARN]` Foundation (partial) — ecosystem overview started (Apr 6-9)

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
