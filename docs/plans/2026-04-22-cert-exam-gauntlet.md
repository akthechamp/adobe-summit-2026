# Apr 22 Cert Exam Gauntlet — Summit Day 4

**Goal:** Maximize cert pickups on the last day of Summit, taking advantage of free vouchers for Adobe Digital Experience certification exams.

**Context:** Day 4 of Summit. Day 1 (Apr 20) was 5 exams → 1 pass (AD0-E712 Commerce BP). Today (Apr 21) is rest + study. Tomorrow (Apr 22) is the last chance to capitalize on free Summit vouchers before leaving Las Vegas.

**Exams booked for tomorrow (in planned execution order):**

1. 🟥 **AD0-E555 Marketo Engage Professional** — *retake* (first attempt failed 56% on Apr 20)
2. 🟩 **Adobe Analytics Business Practitioner Professional** — fresh, high fit
3. 🟦 **AD0-E726 Adobe Commerce Front-end Developer Professional** — fresh, depends on Magento FE recency
4. 🟪 **AD0-E724 Adobe Commerce Developer Professional** — fresh, hardest fit

**Financial stakes:** $0 tomorrow (free Summit vouchers). Retake wait if failed: 15 calendar days per Adobe policy. Acceptable — any failed retake is pushed to ~May 7.

**Honest pass-probability estimate going in:**

| Exam | Est. pass % | Why |
|---|---|---|
| AD0-E555 Marketo retake | 55-65% | Known gaps + 6 hours focused study + slower pacing |
| Analytics BP | 60-70% | HubSpot reporting transfers cleanly; conceptual exam |
| AD0-E726 Commerce FE Dev | 35-45% | General frontend ≠ Magento 2 theming (Knockout/LESS/Layout XML) |
| AD0-E724 Commerce Dev | 25-35% | Requires recent Magento 2 PHP (di.xml, plugins, observers) |

**Expected haul:** 1-2 passes realistically. 3 would be excellent. 4 would be a statistical outlier worth celebrating.

---

## The Day in Detail

### Tonight (Apr 21 evening) — Marketo-focused study

~3.5 hours concentrated. See "Marketo Retake Study Plan" section below. **Nothing else** tonight — prep for other exams happens in the 10-15 min slots between exams tomorrow.

### Tomorrow morning pre-9 AM (Apr 22)

- **6:30-7:00 AM** — real breakfast. Protein + slow carbs. Not a pastry-and-espresso.
- **7:00-8:30 AM** — final Marketo review (flashcards sheet + RCM diagrams)
- **8:30-9:00 AM** — get to cert booth. Water, bathroom, deep breathing.

### Exam sequence (execution order + rationale)

| Slot | Exam | Why this order |
|---|---|---|
| **9:00 AM** | Marketo retake | Peak brain. This is the biggest investment; give it your sharpest state. |
| 10:00 AM | 60-min break | Walk, snack, hydrate. No phone scroll. |
| **11:00 AM** | Analytics BP | Still sharp. HubSpot background transfers. Quick exam — probably finish in 30 min. |
| 11:45 AM | 75-min lunch | Real food. Step outside if possible. |
| **1:00 PM** | AD0-E726 FE Dev | Afternoon slump starts, but frontend work is familiar territory. |
| 2:00 PM | 60-min break | Power nap if possible (even 15 min). Coffee. |
| **3:00 PM** | AD0-E724 Commerce Dev | Hardest. By now it's "house money" — prior 3 are banked. Go in loose. |

Total: ~6 hours of exams + ~3 hours of breaks = full day.

### Pacing rules (applies to ALL exams)

- **Target 60-65 seconds per question.** Last attempts averaged 25-30 sec → 15-20% points lost to rushing.
- **Two-pass strategy:** First pass answer only the confident ones (mark-and-return for the rest), second pass attack the hard ones.
- **Eliminate obvious wrongs first.** Most Adobe MCQs have 1 distractor that's clearly wrong.
- **If you're finishing in <40 min, you're rushing.** Slow down and re-read.

---

## Marketo Retake Study Plan (6 hours)

**Current score:** 31/55 (56%). **Target:** 38/55 (~70%). **Gap:** +7 correct answers.

**Section-level priority (from Apr 20 breakdown):**

| Section | Apr 20 | Target | Swing needed |
|---|---|---|---|
| Reports & Analytics | 3/7 (43%) | 5/7 | +2 |
| Programs & Managing | 12/21 (57%) | 15/21 | +3 |
| Audiences | 10/17 (59%) | 12/17 | +2 |
| Assets | 6/10 (60%) | 7/10 | +1 |

Total possible gain: +8 → 39/55 (71%) if executed.

### Tonight: 3.5 hours across 3 blocks

**Block 1 — Reports & Analytics (90 min, biggest leverage)**

Read on Adobe Experience League:
- [Revenue Cycle Modeler overview](https://experienceleague.adobe.com/docs/marketo/using/product-docs/demand-generation/revenue-cycle-modeler/understanding-revenue-cycle-modeler/overview-of-revenue-cycle-modeler.html)
- [Revenue Explorer](https://experienceleague.adobe.com/docs/marketo/using/product-docs/reporting/revenue-explorer/understanding-revenue-explorer/overview-of-revenue-explorer.html)

Memorize these distinctions:
- **RCM stages** (Early / Mid / Late / Hand-Raisers) vs **program success** (generic)
- **Model stages** include detour paths and back-flow — members can regress
- **Revenue Explorer** = pre-built reports, ad-hoc via Analyzers
- **Opportunity Analyzer** vs **Program Analyzer** vs **Company Web Activity** — know what each does
- **First-Touch** (FT = lead source) vs **Multi-Touch** attribution (MT = programs touching)
- **Email Performance Report** (aggregate) vs **Email Link Performance Report** (click-level) vs **Program Performance Report** (membership + success)

YouTube: search **"Etumos Revenue Cycle Model"** — ~15-min explainer. Also try "Perkuto Marketo RCM".

**Block 2 — Engagement Programs deep dive (60 min)**

[Engagement Programs docs](https://experienceleague.adobe.com/docs/marketo/using/product-docs/demand-generation/engagement-programs/understanding-engagement-programs/understanding-engagement-programs.html)

Memorize:
- **Streams** = ordered content queues within an Engagement Program
- **Cadence** = every 1, 2, or 4 weeks (only these options)
- **Pause** (keeps member) vs **Exhausted** (out of content) vs **Engaged** (completed all streams)
- **Transitioning streams** = rules that move members between streams based on behavior
- Emails sent in stream order → exhausted → transition or stay exhausted
- **Cast frequency** is set at program level, not stream level

**Block 3 — Flashcards / distinctions memorization (30 min)**

The "which word is correct?" distinctions tested repeatedly:
- **Filter** (static, past behavior) vs **Trigger** (starts flow on event)
- **Smart List** (dynamic, re-queries) vs **Static List** (snapshot)
- **Program Status** (state in flow: "Invited", "Registered") vs **Program Success** (conversion, binary)
- **Segments** (partition you define) vs **Segmentations** (parent container of segments)
- **My Token** (inherits from folder/program) vs **Program Token** (inherits into program)
- **Lead Partition** (data-level separation, permission-gated) vs **Workspace** (admin-level grouping of assets)

Write on a sheet. Re-read before bed + again at 7 AM.

### Tomorrow 7:00-8:30 AM (90 min)

**Block 4 — Audiences: Smart Lists (60 min)**

[Smart Lists docs](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists/understanding-smart-lists/understanding-smart-list-filters.html)

Filter categories:
- **Demographic** (lead attributes: Country = "US")
- **Company** (company attributes)
- **Behavior** (Opened Email, Clicked Link, Filled Out Form, Visited Web Page)
- **Activity Log** (data value change events)
- **Smart Campaign** (was in campaign)
- **Scoring** (Behavior Score > X)

Trigger categories: same names but **start a flow** when event occurs. Key rule: **Triggers start flows; filters narrow audiences.** A smart campaign needs at least one trigger OR schedule — filters alone never start anything.

**Block 5 — Assets: Tokens + Progressive Profiling (30 min)**

- **System tokens:** automatic, e.g. `{{lead.First Name}}`, `{{company.Name}}`
- **My Tokens:** custom variables at folder/program/workspace; inherit downward
- **Token precedence:** closest token wins (program overrides folder)
- **Progressive profiling:** form shows only missing fields, priority fields asked first, max N per visit (configurable)
- **Email snippets:** reusable content blocks; update once, reflect everywhere

### 8:30-9:00 AM — Final review

Re-read flashcard sheet one more time. No new material.

---

## Analytics Business Practitioner Pre-Exam Quick Review (15 min over lunch, pre-11 AM)

Skim [Adobe Analytics overview](https://experienceleague.adobe.com/docs/analytics/landing/home.html).

Key concepts to memorize quickly:
- **Dimensions** (the "what" — pages, products, campaigns) vs **Metrics** (the "how much" — visits, revenue, bounces)
- **Workspace** vs **Reports & Analytics** (legacy)
- **Segments** — in-panel filter; applies to all components in panel
- **Calculated Metrics** — formulas combining existing metrics (e.g., `Revenue / Orders = AOV`)
- **Attribution IQ** — first-touch, last-touch, linear, U-shaped, participation, custom
- **Virtual Report Suites** — segmented views of a parent suite; don't duplicate data
- **Flow visualization** — shows next/previous page paths
- **Fallout reports** — funnel drop-off analysis

Your HubSpot reporting background covers 70%+ of this conceptually. You'll recognize patterns. Don't over-study; trust the transfer.

---

## Commerce Front-end Developer (E726) Pre-Exam Review (10-15 min over lunch break)

Focus on Magento 2 specifics that DIFFER from general frontend:

- **Theme hierarchy:** parent theme → child theme → override. Common parents: `Magento/luma`, `Magento/blank`.
- **Layout XML:** `default.xml`, `catalog_product_view.xml` (page-type handles). Key elements: `<referenceBlock>`, `<referenceContainer>`, `<move>`, `<remove>`.
- **Templates:** `.phtml` files in `view/frontend/templates/`. Access `$block` for data.
- **LESS:** Magento uses LESS (not Sass). Compiled via `bin/magento setup:static-content:deploy`.
- **RequireJS config:** `view/frontend/requirejs-config.js` — define paths + shims + mixins.
- **Knockout:** Magento uses KO for checkout + mini-cart. `data-bind` attributes, `uiComponent` pattern.
- **UI Components (JS):** `*.js` + `*.html` (template) + `*.xml` (layout) + `*.phtml` (server bootstrap).
- **Page Builder content types:** custom types via `view/adminhtml/pagebuilder/content_type/` + frontend renderer.

If any of those terms feel unfamiliar → likely a fail. If they ring bells → decent shot.

---

## Commerce Developer (E724) Pre-Exam Review (10-15 min, post-Analytics break)

Backend Magento 2 specifics:

- **Module structure:** `app/code/Vendor/Module/` with `etc/module.xml`, `registration.php`, `composer.json`.
- **Dependency Injection:** `etc/di.xml` — `preference` (override class), `plugin` (extend method: before/after/around), `type` / `arguments`.
- **Plugins vs Preferences:** plugins extend (multiple allowed); preferences replace (one winner). Prefer plugins.
- **Observers:** `etc/events.xml` → `Observer\Name.php implements ObserverInterface`. Sync, one-direction.
- **UI Components (admin grids):** `view/adminhtml/ui_component/*.xml` + listing data provider + collection.
- **GraphQL:** `etc/schema.graphqls` + resolver classes. Know the `@doc`, `@resolver` directives.
- **REST API:** `etc/webapi.xml` + service contract interface + implementation.
- **Indexers:** `etc/indexer.xml` + action class. Know: Update on Save vs Update on Schedule.
- **Cron:** `etc/crontab.xml` + job class.
- **Areas:** frontend, adminhtml, crontab, webapi_rest, webapi_soap — configs split per area.

This exam likely fails unless you've written Magento 2 modules in the last 12 months. Go in with realistic expectations — use as practice reconnaissance for a later retake.

---

## Post-Exam Protocol (per exam)

- Screenshot the result page → save to `Adobe Summit 2026/notes/exam-results/`
- Don't dwell on failures — each failure has a 15-day retake wait regardless of how bad the score
- **Passes:** LinkedIn post within 30 min (Summit visibility window is narrow)

## End of day wrap

- Tally results: X passes, Y fails
- Update `notes/exam-results/` with all 4 result files
- Update `CHANGELOG.md` with Summit final cert tally
- Decide if any of the fails are worth retaking from home (15 days later = ~May 7)

---

## Lessons carried from Apr 20

1. **60-sec pacing per question**, not 25. Slow down.
2. **Eat a real breakfast.** Rushing on empty stomach cost points.
3. **Between-exam breaks must be 60+ min.** 30-min gaps break focus.
4. **Commerce Business Practitioner passed.** Prove the Professional tier + adjacent-background combo works.
5. **Expert tier = skip.** Today's exams are all Professional — don't accidentally book an Expert one.
