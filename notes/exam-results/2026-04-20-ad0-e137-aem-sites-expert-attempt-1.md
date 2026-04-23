# AD0-E137 — Adobe Experience Manager Sites Developer **Expert** — Attempt 1

**Result:** ❌ Not passed
**Score:** 20 / 50 (40%)
**Date:** April 20, 2026, 11:23 AM (Adobe Summit, Las Vegas)
**Duration:** 21 minutes, 53 seconds (~26 sec/question)
**Tier:** **Expert** (not Professional — harder tier, typically requires 2+ years of hands-on AEM dev)
**Candidate:** Web Forte Technologies (Adobe ID: `05BB38D45768CBFB7F000101@AdobeID`)

---

## Score breakdown

| # | Section | Raw score | % | Questions wrong |
|---|---------|----------|----|----|
| 1 | Configurations | 8 / 12 | **67%** | 4 |
| 2 | AEM Development | 9 / 20 | 45% | 11 |
| 3 | Build and Deployment | 2 / 10 | 20% | 8 |
| 4 | Environment Maintenance | 1 / 8 | **13%** | 7 |
| — | **Total** | **20 / 50** | **40%** | 30 |

Passing threshold for Adobe **Expert** exams is typically 65–72% — this was a 25+ percentage-point gap.

## Analysis — honest read

**Expert tier vs background mismatch.** AD0-E137 is the **Expert** tier, which Adobe explicitly targets at candidates with 2+ years of hands-on AEM development experience (OSGi bundles, Sling models, HTL/Sightly, JCR, CRXDE, component authoring, Apache Sling/Felix internals). Coming from a frontend + HubSpot background without deep AEM time, the failure isn't a reflection of capability — it's an experience-gap exam that isn't realistic to pass on conceptual study alone.

**Timing: two exams back-to-back.** This was completed 31 minutes after the AD0-E555 Marketo result came in (10:52 AM → 11:23 AM). No break, no reset. Decision fatigue was stacked against this attempt from the start.

**26 sec/question — rushed, again.** Same pacing issue as the Marketo exam. Expert-tier questions are typically longer + more scenario-heavy than Professional questions, so the time pressure hit harder here.

**Section breakdown tells the story:**
- **Configurations (67%)** — conceptual OSGi / dispatcher / replication knowledge mostly landed. Study-based.
- **AEM Development (45%)** — the heart of the exam. Building components with dialogs, Sling Models, HTL templates, JCR queries, event listeners, workflows. Needs **hands-on** — you can't read your way through component authoring.
- **Build and Deployment (20%)** — Maven + filter.xml + package manager + CI/CD for AEM specifically. Very hands-on.
- **Environment Maintenance (13%)** — dispatcher troubleshooting, GC, performance tuning, logs analysis. Production-ops territory.

The bottom two sections (Build/Deploy + Env Maintenance = 18 questions) are almost entirely *in-the-trenches* AEM work. Impossible to fake.

## Recommendation: is AD0-E137 worth retaking?

**Probably not — consider a different AEM path:**

1. **Drop down a tier.** Adobe has a **Professional** tier for AEM Sites (not yet checked which code — around AD0-E126 or similar). Professional tier is more conceptual and fits someone doing dev-adjacent work. Expert tier is for full-stack AEM implementors.

2. **Business Practitioner tier exists too** (AD0-E117 range) — for authors, not developers. Depends on what cert value you need for Summit lead conversations.

3. **If you genuinely want Expert:** minimum 60–90 days of hands-on AEM Cloud Service work (Adobe provides free developer instances). Build 3-4 actual sites. Then retake.

4. **Opportunity cost right now:** You still have AD0-E712 (Adobe Commerce Professional) unattempted. Commerce is closer to your Magento/frontend background. Much higher pass probability than re-attempting AEM Expert.

## What this means for cert stack strategy

Your actual cert roadmap, refined:

| Cert | Tier | Your fit | Priority |
|---|---|---|---|
| AD0-E712 — **Adobe Commerce Professional** | Professional | High (Magento heritage) | **P1 — target next** |
| AD0-E555 — Adobe Marketo Engage Professional | Professional | Medium (post-HubSpot transfer) | P2 — retake after detailed report |
| AD0-E137 — AEM Sites Developer **Expert** | Expert | Low without hands-on | **Skip or defer 60-90 days** |
| AD0-E117 / E126 range — AEM **Professional** | Professional | TBD — check scope | P3 — alternative to Expert if AEM cred is needed |

## Retake logistics

- Same retake policy as Marketo: <https://certification.adobe.com/support/faq>
- Expert exams sometimes have stricter retake windows + cost implications (Professional voucher won't cover it)
- Detailed topic report within 72 hours (~Apr 23) — useful even if not retaking, shows exactly which AEM topics were weakest

## Lessons carried forward

1. **Don't stack exams back-to-back.** 30-minute gap is not enough. The second attempt inherits fatigue from the first.
2. **Match tier to experience.** Expert ≠ Professional. Read the Adobe role prerequisite carefully before booking an Expert exam.
3. **Pacing discipline.** Both exams today were done in under 30 minutes of ~60 available. Slowing down costs nothing; rushing costs 15-20 percentage points.
4. **Free vouchers are tempting but not free if you fail an exam you can't retake cheaply.** Adobe Summit vouchers typically cover one exam per attendee — using it on a tier mismatch wasted the voucher.
