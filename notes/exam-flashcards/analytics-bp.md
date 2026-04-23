# Adobe Analytics Business Practitioner Professional — Study Guide + Flashcards

## Exam facts

| Attribute | Value | Confidence |
|---|---|---|
| Exam code | **AD0-E212** | ✅ Confirmed (EDUSUM + Adobe cert catalog) |
| Full title | Adobe Certified Professional — Adobe Analytics Business Practitioner | ✅ |
| Questions | ~50 (typical for Adobe Professional tier) | ⚠️ Not publicly published; verify at check-in |
| Duration | ~100 min | ⚠️ Not publicly published |
| Passing score | ~65-70% | ⚠️ Not publicly published |
| Retake wait (1st fail) | 24 hours | ✅ |
| Cost | ~$125 USD (free Summit voucher) | ✅ |
| Prerequisites | Business Practitioner = operational user; ~6-12 months Analytics use recommended | ✅ |

**Research limitation:** Adobe's detailed exam guide for AD0-E212 is behind login at [certification.adobe.com/courses/173](https://certification.adobe.com/courses/173). Domain weights are not public. Topics below are reconstructed from: the related Analytics Expert (AD0-E208) domain structure, Quizlet flashcard sets, EDUSUM sample questions, and standard Adobe Analytics Business Practitioner curriculum.

### Most likely domain structure (reconstructed)

Based on AD0-E208 Expert structure and Adobe's BP vs Expert tier patterns, AD0-E212 likely covers:

| Domain | Est. weight | Description |
|---|---|---|
| Reporting & Analysis | ~30-35% | Workspace projects, visualizations, components, freeform tables |
| Segmentation & Calculated Metrics | ~20-25% | Segment containers, calc metric formulas, sharing |
| Data Concepts | ~20% | Dimensions, metrics, eVars, props, events |
| Administration & Tools | ~15-20% | Report suites, VRS, admin console, Launch/Tags basics |
| Integrations & Ecosystem | ~10-15% | Customer Journey Analytics, Target, AEP, mobile SDK |

Treat this as a **guide, not gospel**. On exam day, watch the mix of questions to gauge actual weighting live.

---

# PART 1 — Full topic coverage

## Domain 1 — Reporting & Analysis (~30%)

### Adobe Analytics Workspace (the main UI)

- **Project** = a Workspace file (like a dashboard)
- **Panel** = section within a project (freeform, attribution, experimentation types exist)
- **Visualization** = chart or table (freeform table, line, bar, fallout, flow, cohort, venn, etc.)
- **Component** = draggable piece (dimension, metric, segment, date range)
- **Right-click → Breakdown** = add second dimension to existing row

### Key visualization types (know their purpose)

| Visualization | When to use |
|---|---|
| Freeform table | Default tabular analysis |
| Line | Trend over time |
| Bar / Horizontal Bar | Category comparison |
| Fallout | Ordered-step funnel with drop-off % |
| Flow | Next/previous page flow (unordered) |
| Cohort | Retention of groups over time |
| Venn | Overlap between 2-3 segments |
| Histogram | Distribution of metric |
| Summary Number / Change | KPI boxes |
| Scatter plot | Two-metric correlation |

### Panels — know the 3 types

- **Blank Panel** — build your own
- **Freeform Panel** — most common default
- **Attribution Panel** — compare attribution models side-by-side
- **Quick Insights Panel** — guided analysis
- **Media Concurrent Viewers** — streaming analytics

### Components — how to think about them

Components are the atomic drag-drop pieces:
- Dimensions (blue) = the WHAT
- Metrics (green) = the HOW MUCH
- Segments (yellow/blue) = filters
- Date Ranges (purple) = time frames

### Reporting approach: building a project

1. Pick date range
2. Drag dimension into table
3. Drag metric(s)
4. Add segments as filter
5. Breakdown for second dimension
6. Visualize → choose chart type

### Sharing

- **Share project** with users (view / edit / curate)
- **Scheduled projects** — email PDF or CSV on cadence
- **Download PDF / CSV** — one-off export

---

## Domain 2 — Segmentation & Calculated Metrics (~22%)

### Segment scopes (memorize — most-tested concept)

Hierarchy: **Visitor > Visit > Hit**

| Scope | What it captures |
|---|---|
| **Hit** (Page View) | Single interaction — narrowest |
| **Visit** (Session) | Group of hits, 30-min inactivity = new visit |
| **Visitor** | Individual (cookie) — widest |

**Rule:** Outer container can be broader than inner; inner can't be broader. ("Visit where visitor did X" is OK; "Visitor where hit X" means include the whole visitor if any hit qualifies.)

### Segment builder

- **Include / Exclude** logic
- **AND / OR** operators
- **Then** = sequential (X happened, THEN Y happened)
- **Within N visits / days / hits** — time/sequence constraint
- **Nested containers** — visitor > visit > hit logic
- **Segment stack** = combining multiple segments in a panel

### Segment approval

- Public segments visible to all
- Private segments visible only to creator
- Share → "Shared with me" for recipients
- Approve segments for enterprise use (limit sprawl)

### Calculated Metrics

- Formulas built from existing metrics + segments + date functions
- **Types:**
  - Ratio / Percent (`Orders / Visits * 100`)
  - Count (simple sum)
  - Segmented metric (`Revenue FROM segment X`)
- **Functions available:** IF/THEN, greater-than, boolean, math operators
- **Shared** via component library
- **Calc metric containers:** similar to segment containers, scoped Hit/Visit/Visitor

### Alerts

- Threshold-triggered notifications
- Metric exceeds X OR % change > Y
- Delivered via email / mobile push
- Scoped to report or standalone

---

## Domain 3 — Data Concepts (~20%)

### Dimensions vs Metrics (the foundational distinction)

| Dimension | Metric |
|---|---|
| The WHAT (page, product, campaign) | The HOW MUCH (visits, revenue, bounces) |
| Values are strings | Values are numbers |
| Rows in a freeform table | Columns in a freeform table |

### eVars vs Props (the most-tested tech distinction)

| eVar (Conversion Variable) | Prop (Traffic Variable) |
|---|---|
| **Persists** beyond current hit | **Hit-scope only** — dies after current hit |
| Used in **conversion reports** | Used in **traffic reports** (legacy heavy) |
| Allocation configurable (most recent / original / linear) | No allocation settings |
| Expiration configurable (visit / visitor / custom / conversion) | No persistence |
| Supports pathing via segments | Native pathing reports |
| Up to 250+ per report suite | Up to 75 per report suite |

### Events / Success Events

- Configurable metrics (orders, revenue, leads generated, custom events)
- **Numeric**, **Counter**, **Currency**
- **Serialized** events — dedupe by unique ID (prevents counting same order twice)

### Solution Variables

- **Products variable** — tracks e-commerce products list
- **Marketing Channels** — processing rules that categorize traffic source
- **List Props / List eVars** — track multiple values in single variable (categories, tags)

### Pathing Reports (flow, fallout, next/prev)

- Pathing enabled on specific dimensions
- Pages are the most common pathed dimension
- **Next Page Flow** shows what users went to next
- **Previous Page Flow** shows where they came from
- **Full Paths** = complete visit sequences

### Attribution IQ — know all 10 models

| Model | Definition |
|---|---|
| **Last-touch** | 100% credit to last touchpoint (default) |
| **First-touch** | 100% to first touchpoint |
| **Linear** | Equal credit across all touchpoints |
| **Participation** | 100% to EVERY touchpoint (sum > 100%) |
| **Same-touch** | Credit only on touchpoint that IS the conversion hit |
| **U-shaped / Position** | 40% first, 40% last, 20% middle |
| **J-shaped** | Weighted toward last |
| **Inverse J** | Weighted toward first |
| **Time decay** | Recent > older |
| **Custom** | User-defined weights per position |

**Rule:** Attribution model is **set on the metric** (or calculated metric) — you can show multiple models side-by-side in an Attribution Panel.

### eVar persistence (know the defaults)

- **Visit** (default) — expires at session end
- **Visitor** — until overwritten or manual expire
- **Custom** (N days, weeks, months)
- **Conversion / Purchase** — expires after success event
- **On Page View** — expires after next hit

### eVar allocation

- **Most Recent** (default) — last value wins
- **Original** — first value wins
- **Linear** — spread across all values in window

---

## Domain 4 — Administration & Tools (~15%)

### Report Suites

- **Report Suite** = data collection bucket where data lands
- **Global Report Suite** (GRS) — aggregate of multiple suites
- **Roll-Up Suite** — aggregated reporting without drill-down
- **Multi-Suite Tagging** = sending same hit to multiple suites
- Each suite has its own variable configuration

### Virtual Report Suites (VRS)

- **Segmented view of a parent suite** — no duplicated data storage
- Inherit parent's variable configuration (mostly)
- Use for: team-specific views, property-level reporting within global tracking
- Components can be scoped to VRS

### Admin Console (top-level)

- Report suite settings (conversion variables, events, traffic variables)
- Metrics / components
- User management + groups / permissions
- Data Warehouse configuration
- Classifications

### Classifications

- Map raw variable values to friendly labels
- Example: tracking code `nl_apr26` → classified as `Email / Spring 2026 Newsletter`
- Upload via CSV
- Multiple levels (hierarchy)

### Data Sources

- **Data Feeds** — raw hit-level export (FTP/S3, tab-separated files)
- **Data Warehouse** — exhaustive custom report export (slower, comprehensive)
- **Report Builder** — Excel add-in for pulling A4 data into Excel
- **Reporting API** — programmatic access (v2.0)

### Launch (Tags) / Adobe Experience Platform Tags

- Deploys JS libraries that call Analytics (replaces DTM)
- **Environments:** Development / Staging / Production
- **Extensions** — plugins for Analytics, Target, Audience Manager, etc.
- **Rules** — Event → Condition → Action

### Tracking Implementation

- **AppMeasurement.js** (legacy but still common) — JS library
- **Adobe Experience Platform Web SDK** (newer) — unified SDK for AEP + Analytics + Target
- **Mobile SDK / ACP SDK** — native iOS/Android
- **Server-side forwarding** — from Analytics to Target/AAM

### Processing Rules vs VISTA Rules

- **Processing Rules** — admin UI, modify hits before processing (self-serve)
- **VISTA Rules** — server-side, require Adobe Consulting (deeper transformations)

---

## Domain 5 — Integrations & Ecosystem (~10-15%)

### Adobe Experience Cloud Integrations

- **Adobe Target** — experimentation / personalization; share audiences
- **Adobe Audience Manager (AAM)** — segments synced bidirectionally
- **Customer Journey Analytics (CJA)** — cross-channel analysis on AEP
- **Adobe Experience Platform (AEP)** — unified profile
- **Customer Attributes** — import attributes (via FTP) to enrich visitors

### Activation downstream

- Segments can be exported to Target (A4T)
- Audiences flow to Ad platforms via AAM integrations
- Data flows to AEP for Real-Time CDP profiles

### Customer Journey Analytics (CJA) vs Adobe Analytics (AA)

| Analytics (traditional) | CJA |
|---|---|
| Web + mobile hits | Any dataset on AEP |
| Schema-rigid variables | Flexible schema |
| Last ~27 months data | Unlimited via AEP |
| Visitor ID model | Cross-device via Stitching |

### Real-Time Reports

- Live report (1-min lag)
- Limited metrics (page views, revenue, etc.)
- Not for deep analysis; monitoring only

---

# PART 2 — Rapid-Scan Flashcards

## ⚡ Top 12 most-tested distinctions

| A | B | Discriminator |
|---|---|---|
| **Dimension** | **Metric** | Dimension = string (WHAT); Metric = number (HOW MUCH) |
| **eVar** | **Prop** | eVar persists (visit/visitor/custom); Prop is hit-scope only |
| **Visitor** | **Visit** | Visitor = person (cookie); Visit = session (30-min inactivity = new) |
| **Segment** | **Calculated Metric** | Segment filters data (WHO); CalcMetric = formula on metrics (math) |
| **Virtual Report Suite** | **Report Suite** | VRS = segmented view, no duplicated data; RS = actual data bucket |
| **Roll-Up Suite** | **VRS** | Roll-Up = aggregated, no drill; VRS = drill available |
| **Fallout** | **Flow** | Fallout = ordered steps (funnel); Flow = next/prev paths (unordered) |
| **Processing Rules** | **VISTA Rules** | Processing = self-serve admin UI; VISTA = server-side, Adobe consulting |
| **Data Warehouse** | **Data Feeds** | Warehouse = custom report export; Feeds = raw hit-level firehose |
| **First-touch** | **Last-touch** | FT = first program credit; LT = last program credit (default) |
| **Linear** | **Participation** | Linear = equal split sums to 100%; Participation = full credit each (sums > 100%) |
| **AppMeasurement** | **Web SDK** | AppMeasurement = legacy JS; Web SDK = modern AEP-unified |

## ⚡ Segment scopes cheat

`Hit < Visit < Visitor` (narrowest to widest)

Outer container can be **broader** than inner, never narrower.

- "Visitor where visit had X" ✅ (include whole visitor because one visit matched)
- "Hit where visit had X" — invalid; hit scope can't contain visit container

## ⚡ All 10 attribution models (memorize)

Last-touch · First-touch · Linear · Participation · Same-touch · U-shaped · J-shaped · Inverse J · Time decay · Custom

## ⚡ eVar expiration options

Visit (default) · Visitor · Custom (N days/weeks/months) · Conversion/Purchase · On next hit · Never

## ⚡ Visualization → purpose map

- Freeform table = default
- Line = trend
- Fallout = ordered funnel
- Flow = paths
- Cohort = retention
- Venn = segment overlap
- Histogram = distribution
- Summary Number = KPI tile

## ⚡ Panel types

Blank · Freeform · Attribution · Quick Insights · Media Concurrent Viewers

## ⚡ Component colors in Workspace

- **Blue** = Dimension
- **Green** = Metric
- **Orange** = Calculated Metric
- **Purple** = Date Range
- **Yellow-ish** = Segment

## ⚡ eVar allocation (when multiple values in visit)

- **Most Recent** (default) = last value wins
- **Original** = first value wins
- **Linear** = spread credit across all values

## ⚡ Launch/Tags environments

Development → Staging → Production — each publishes its own library

## ⚡ Pathing

- Only on **pathing-enabled dimensions** (pages, custom paths)
- **Next Page Flow, Previous Page Flow, Full Paths** — free-form
- **Fallout Report** — ordered funnel with drop-off %

## ⚡ Key classifications concept

- Raw variable values → friendly names via lookup table
- Upload via CSV
- Hierarchical (multi-level)

## ⚡ Integrations you should recognize

Target (A4T) · Audience Manager · Customer Journey Analytics · AEP · Customer Attributes · Real-Time CDP · Launch (Tags) · Analysis Workspace · Report Builder

## ⚡ Exam strategy

- **HubSpot reporting background covers ~70%** of this — trust your intuition on segment + metric concepts
- **eVar vs prop** is the single most-tested technical concept — know it cold
- **Segment scope (Hit/Visit/Visitor)** appears in 3-5 questions typically — know the containment rule
- **Attribution model name recognition** matters — don't over-analyze, just match model to scenario
- When a question mentions specific **variable numbers** (eVar10, prop5), that's likely dev trivia — pick the answer that matches the BP mental model, not the dev detail

---

## Sources used

- [Adobe AD0-E212 Certification (official, login-gated)](https://certification.adobe.com/courses/173)
- [Adobe AD0-E208 Expert Analytics exam domains](https://www.edusum.com/adobe/adobe-analytics-business-practitioner-expert-exam-syllabus) (used as structural reference for BP tier)
- [Adobe Analytics Business Practitioner Professional Prep Guide](https://certification.adobe.com/courses/1195) (login-gated)
- [Adobe Experience League community AD0-E212 discussions](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics-questions/ad0-e212-adobe-analytics-business-practitioner-professional/td-p/735936)
- Standard Adobe Analytics Workspace documentation
