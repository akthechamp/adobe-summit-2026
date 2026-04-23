# AD0-E555 — Adobe Marketo Engage Professional — Attempt 1

**Result:** ❌ Not passed
**Score:** 31 / 55 (56.4%)
**Date:** April 20, 2026, 10:52 AM (Adobe Summit, Las Vegas)
**Duration:** 24 minutes, 42 seconds (~27 sec/question)
**Candidate:** Web Forte Technologies (Adobe ID: `05BB38D45768CBFB7F000101@AdobeID`)

---

## Score breakdown

| # | Section | Raw score | % | Questions wrong |
|---|---------|----------|----|----|
| 1 | Building and Managing Programs | 12 / 21 | 57% | 9 |
| 2 | Building Assets | 6 / 10 | 60% | 4 |
| 3 | Defining and Targeting Audiences | 10 / 17 | 59% | 7 |
| 4 | Analyzing and Building Reports | 3 / 7 | **43%** | 4 |
| — | **Total** | **31 / 55** | **56%** | 24 |

Passing threshold for Adobe Professional exams is typically 65–70% — gap of 5–8 correct answers.

## Analysis

**Gap was broad, not narrow.** Every section landed below pass threshold. No single topic area carried the failure; the entire exam surface needs more depth.

**Rushed pacing.** 27 seconds per question is fast for scenario-heavy Marketo items. A 60-minute+ pace (~65 sec/q) would allow reading carefully and catching the filter-vs-trigger / status-vs-success distinctions that Marketo loves to test.

**Weakest — Reports & Analytics (43%).** This is the smallest section but the lowest percentage. Revenue Cycle Modeler, attribution models, and Revenue Explorer are the likely culprits — they're genuinely different concepts from HubSpot's reporting.

**Highest absolute losses — Programs (9 wrong).** Largest section, so biggest improvement lever. Engagement Programs (streams, cadence, transitions) and program-token inheritance are the typical gotchas.

## Retake study plan (priority order)

### 1. Reports & Analytics — raise 43% → 80%+
- **Revenue Cycle Modeler (RCM):** model stages, success path vs detour, transition rules, how to visualize
- **Revenue Explorer:** when it's used vs Opportunity Analyzer, which report for which question
- **Email Performance Report** vs **Program Performance Report** — what each shows
- **Attribution models** — First-Touch vs Multi-Touch, how Marketo assigns
- **Engagement dashboards** — member counts, stream stats
- **Report subscriptions** — delivery cadence, recipients

### 2. Programs — raise 57% → 80%+
- **Engagement Programs:** Streams (how to design), Cadence (weekly / bi-weekly / monthly), transitions between streams, Exhausted vs Engaged, Pause/Resume
- **Program types:** Default vs Engagement vs Email, when to pick which
- **Program Status vs Success** — these are different things (status = where member is in flow, success = did conversion happen)
- **Tokens:** Program tokens, My Tokens, folder inheritance chain
- **Costs:** Period Cost, Program Cost, how they roll up
- **Channels & Tags** — how they drive reporting

### 3. Audiences — raise 59% → 80%+
- **Smart List filters vs triggers** — the single most-tested distinction
- **Nested smart lists** + **Data Value Changed** + **Activity filters**
- **Segments vs Segmentations** (not interchangeable terms)
- **Lead partitions + workspaces** — very different from HubSpot teams
- **Lead scoring:** Behavior Score + Demographic Score + combined

### 4. Assets — raise 60% → 80%+
- **Progressive profiling on forms** + form validation rules
- **Email tokens** (system, program, my tokens) + fallback values
- **Snippets** + dynamic content + segmentation-based variants
- **Landing page templates** + responsive behavior

## Concrete study resources

- Adobe Learning (free): <https://experienceleague.adobe.com/docs/marketo/using/home.html> — RCM and Engagement Program sections specifically
- Marketo Certified Expert exam prep materials (Engage tier)
- EDUSUM practice tests (was in Summit prep plan — do 2-3 full tests before retake)
- LinkedIn Learning or Udemy Marketo course — focus on labs, not lectures

## Retake timeline

- Retake policy: <https://certification.adobe.com/support/faq>
- Typical: 24hr wait after first attempt; detailed topic-level report in Adobe Cert Account within 72 hours
- Detailed report will name the specific topics missed — wait for it before diving deep, to focus study
- Plan: detailed report in by Apr 23 → study Apr 23–28 → retake ~Apr 29 (post-Summit, home)

## Context

- **First Adobe cert exam.** HubSpot certified previously, so some concepts transfer but Marketo's model is distinct.
- **Exam was taken at Summit** on Day 2. Environment was the conference cert booth — hurried context, probably contributed to the 24-minute pace.
- Adobe Commerce cert (AD0-E712) also planned — not yet attempted.

## Lessons for next attempt

1. **Slow down.** Use the full allocated time. Read each question twice. Many Marketo answers turn on a single word ("trigger" vs "filter", "success" vs "status").
2. **Practice in a sandbox.** Adobe offers developer instances. Build 3-4 Engagement Programs with streams + tokens + reports before retaking. Concepts stick only after clicking through them.
3. **Memorize the RCM lexicon.** Stage, transition, success path, detour — these words have exact meanings in Marketo that aren't obvious from English.
4. **Wait for the detailed report.** It names the topic areas of missed questions — cheaper to study targeted than to re-read everything.
