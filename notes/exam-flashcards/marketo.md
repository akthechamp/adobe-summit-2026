# Marketo Engage Business Practitioner Professional — Day 3 Focused Study (AD0-E555)

> **Attempt 3 focus.** Apr 20 → 56%, Apr 21 → 60%. Passing = 65.5% (36/55). Gap = 3 correct.
> **Apr 21 regression was in Programs (-2).** Deep-dive here on: **Triggers & Filters** (tested deeper than you'd expect), **Program Cloning** (what transfers vs doesn't), **Period Costs & Budgets**, Engagement Program transitions, Channel progression statuses.

## Exam facts

| Attribute | Value |
|---|---|
| Exam code | AD0-E555 |
| Questions | 55 |
| Duration | 110 minutes |
| Passing | 36/55 (65.5%) |
| Weights | Programs 39% (21q) · Audiences 33% (17q) · Assets 19% (10q) · Reports 9% (7q) |

---

# 🎯 PART 1 — Triggers & Filters (deep)

The exam probes much deeper than "filter = static, trigger = event." Memorize every rule in this section.

## The 4 hierarchical logic levels (Experience League's own framework)

1. **Smart List Filter Operator** — ALL / ANY / Advanced (between filters at the top level)
2. **Filter Type** — which specific filter you're using
3. **Filter Constraint Operator** — per-filter operators ("in past X days", "at least N times")
4. **Member of Smart List** — reference other smart lists for complex audiences

## Triggers vs Filters — the core rules (memorize every line)

| Aspect | Triggers | Filters |
|---|---|---|
| What they are | Live events that **start** a smart campaign flow | Criteria that **narrow** the audience |
| Logic | **Always OR** — can never be changed | ALL (AND) / ANY (OR) / Advanced |
| Number allowed | Multiple — ANY trigger firing qualifies lead | Multiple — combined via chosen logic |
| When evaluated | At the moment the event occurs (live) | Each time smart list runs |
| Can they coexist? | Yes — trigger starts flow, filters refine | Yes — but triggers eval first |

### Iron-clad rules (these ARE tested)

- **Trigger logic is ALWAYS OR.** You cannot change it. Advanced filter logic applies to FILTERS ONLY, not triggers.
- **A trigger must fire first, then filters evaluate.** Filters alone cannot start a smart campaign.
- **At least ONE trigger OR a schedule is required** for a smart campaign to ever run.
- **Complex "Trigger1 AND Filter1) OR (Trigger2 AND Filter2)" scenarios require SEPARATE smart campaigns.** One smart campaign can't apply AND between triggers.
- In trigger mode, smart campaign runs **one person at a time** (per event).
- In batch mode, smart campaign runs on all qualifying members at once.

## Filter operator modes in detail

### ALL (default AND)

All filters must be true. Use when every criterion matters.

### ANY (OR)

At least one filter must be true. Useful for alternate qualifying paths.

### Advanced logic (3+ filters required)

- Uses filter numbers (1, 2, 3...) and parentheses
- Example: `1 AND (2 OR 3)`
- Example: `(1 AND 2) OR (3 AND 4)`
- **Rule: "AND" must appear BEFORE "OR"** when entering rule logic — this prevents ambiguity
- Red underline on invalid syntax; hover to see error
- Replaces nested "Member of Smart List" chains = better performance

## Filter constraint operators — memorize (often tested in scenarios)

### Frequency constraints (for behavior filters)

- **at least N times** — member must have done the action ≥N times
- **at most N times** — action ≤N times
- **exactly N times** — action = N times
- **minimum** / **maximum** variants exist on some filters

### Date/time constraints

- **in past N days** / **in past N weeks** / **in past N months**
- **in future N days** (for date fields on leads)
- **before [date]**
- **after [date]**
- **between [date1] and [date2]**
- **on [exact date]**
- **in date range** (named ranges)
- **is empty** / **is not empty**

### String operators

- **is** / **is not**
- **contains** / **not contains**
- **starts with** / **starts not with**
- **ends with** / **ends not with**
- **in list** / **not in list**
- **any of** / **none of** (multi-select)

### ⚠️ Critical distinction (Experience League specifically calls out)

- **WAS** vs **WAS NOT** — these are OPPOSITES (not a typo, actual different filters)
- **XYZ** vs **NOT XYZ** — picking the wrong variant is a tested trap

## Common triggers + their constraints

| Trigger | Typical constraints |
|---|---|
| **Data Value Changes** | Attribute, New Value (optional), Previous Value (optional), Source (flow step / API / import / any) |
| **Person is Created** | Source (form / API / list import / etc.) |
| **Fills Out Form** | Form name, Web Page |
| **Opens Email** | Email name, Min Times |
| **Clicks Link in Email** | Email, Link, Min Times |
| **Visits Web Page** | Web Page, Min Number of Times |
| **Added to List** | List (specific), Source |
| **Member of Smart Campaign** | Campaign Name, Source |
| **Has Interesting Moment** | Type, Description, Min Times |
| **Score Changes** | Score field, change amount |

**Implicit relationships (tested):**
- **Clicks Link in Email** implies **Opens Email** — using both filters is redundant
- **Attended** for webinar implies **Registered** — chain progression
- **Visits Web Page** doesn't imply form submission

## Combining filters with triggers — worked examples

### Example 1 (standard)

**Goal:** Anyone who fills out Demo Request form OR Contact Us form, AND is in the US AND in Energy industry.

Setup:
- Trigger: Fills Out Form = Demo Request Form
- Trigger: Fills Out Form = Contact Us Form *(OR with first trigger automatically)*
- Filter: Country = US
- Filter: Industry = Energy

Logic: (Trigger1 OR Trigger2) AND Filter1 AND Filter2

### Example 2 (complex — needs separate campaigns)

**Goal:** (Fills Out Form AND US) OR (Visits Pricing Page AND UK)

**You cannot do this in one smart campaign** because triggers can't AND with filters in that configuration. You need:
- Campaign A: Trigger = Fills Out Form, Filter = Country is US
- Campaign B: Trigger = Visits Pricing Page, Filter = Country is UK

### Example 3 (advanced filter logic)

**Goal:** (Email engaged OR scored highly) AND (Industry is target OR Company is Enterprise)

Setup with 4 filters:
1. Opened Email in past 30 days
2. Behavior Score > 50
3. Industry = Finance
4. Company Size > 1000

Advanced logic: `(1 OR 2) AND (3 OR 4)` — but remember rule: AND must come before OR at the top level, so write it as `(1 OR 2) AND (3 OR 4)` which is valid since the top-level operator is AND.

---

# 🧬 PART 2 — Program Cloning (what transfers, what breaks)

## What gets cloned (✅)

- All **local assets** (emails, forms, landing pages, snippets)
- All **smart campaigns** inside the program
- All **smart lists** inside the program
- **My Tokens** defined at the program level
- Program **structure** (folder hierarchy inside)
- **Program Type** (Default / Engagement / Email / Event)
- **Channel** assignment
- **Tags** on the program

## What does NOT get cloned (❌) — highly tested

- ❌ **Period Costs** — explicitly DO NOT transfer. Must re-add manually in the Setup tab of cloned program.
- ❌ **Program member success/status history** (members aren't cloned; activity history belongs to members)
- ❌ **Reports** (program reports don't clone via API; program analyzers don't either)
- ❌ **Push Notifications, In-App Messages, Social Assets** — these program types can't be cloned via API at all
- ❌ **In-App programs** can't be cloned via API

## The List-size rule (tricky — often tested)

When cloning a program containing a **Static List**:
- **<1,000 members:** members clone WITH the list (list retains members in clone)
- **≥1,000 members:** list clones EMPTY (members do NOT carry over)

### Why this matters

If you clone a nurture program template that references a seed list of 500 members, your clone has the same 500. But if you clone a production program with a 50,000-member suppression list, the clone has an EMPTY list — and your suppression fails until you re-populate.

## Cross-workspace cloning

- Must **share all dependent assets** (shared emails, snippets, LP templates, global smart lists) with the destination workspace BEFORE cloning
- If a dependency isn't shared, clone fails or produces broken references
- Workspace-to-workspace is a common source of "why is my cloned program broken?" questions

## Engagement Program cloning specifics

- **Streams** clone (structure + cadence settings)
- **Transition rules** clone
- **Members do NOT clone** (they belong to the original program)
- **Content assignments** within streams clone

## Event Program cloning specifics

- **Webinar integration settings** clone (Zoom / ON24 / WebEx connection)
- **The webinar itself** does not auto-create in the vendor system — you must still configure the session
- **Registrations/attendance** do not clone

## Clone-as-template pattern

Best practice: create a "Gold Master" template program with:
- Pre-built smart campaigns (registration, reminder, follow-up)
- Pre-built emails + landing pages
- Standard tokens
- Standard smart lists
- **NO period cost** (you'll set per-instance)

Then clone this for every new initiative.

---

# 💰 PART 3 — Period Costs, Program Costs & Budgets

## The two cost concepts

| Concept | Definition | Where set |
|---|---|---|
| **Period Cost** | Cost spent in a specific month of a program | Setup tab → Period Cost settings |
| **Program Cost** | Sum of all period costs for the program | Auto-calculated |

## Period Cost deep dive

- Set as **per-month** allocation: "April 2026: $5,000"
- Multiple months can have different costs
- **Month** = Marketo's business month (calendar)
- Drag "Period Cost" from the right panel to Setup tab → enter month + amount

### Why period cost matters (required for these metrics)

- **Cost Per New Name (CPNN)**
- **Cost Per Success**
- **Return on Investment (ROI)**
- **First-Touch / Multi-Touch revenue attribution**

### 🔴 Critical rule (almost certainly tested)

**By default, Revenue Cycle Analytics (RCA) only shows programs that have period costs entered.** Programs with NO period cost are INVISIBLE in RCA attribution reports.

**Workaround:** For programs with legitimately $0 cost (pure organic web forms, email programs with no media spend), enter **$0 or $1** to make them visible in RCA.

## What counts as "variable cost" to include

- Agency fees for the specific program
- Event sponsorship fees
- Pay-Per-Click / paid media spend
- Promotional merchandise
- Any incremental cost attributable to that program

## What is NOT period cost

- Salaries (fixed overhead, not attributable)
- Marketo license fee
- General operational overhead

## Period Cost + Cloning interaction

Remember from Part 2: **period costs DO NOT clone**. If you clone a webinar program with $10,000 in period costs for Q1, the clone comes in with $0. Common failure mode: cloned program runs, generates leads, shows 0 ROI because no cost entered.

## Channel-level cost behavior

Each program has ONE channel (set via Channel dropdown). Channels group programs for reporting but DON'T inherit costs from a channel — each program's period cost is its own.

---

# 🔄 PART 4 — Engagement Programs (transitions + exhausted)

## Content cadence rules

- **Cadence options:** 1 week · 2 weeks · 4 weeks (only these — no 3-week option!)
- Cadence is set at the **program level** (not stream level) via Setup tab
- **Person cadence** vs **Cast frequency:**
  - Person cadence = timing per individual lead (based on their enrollment date)
  - Cast frequency = the schedule Marketo evaluates the program

## Stream content delivery

- Emails in a stream are sent **in stream order** (not reshuffled per lead)
- Each cast: each member gets the next-in-order email in their current stream
- A lead who enters mid-stream starts at content #1 of that stream

## Member states — memorize each definition

| State | What it means |
|---|---|
| **Normal** | Active; will receive next email at next cast |
| **Paused** | Skipped at cast time but kept in program (manual or via flow step) |
| **Exhausted** | Has received every piece of content in their CURRENT stream; sits idle |
| **Engaged** | Has completed ALL streams (terminally finished, nothing left) |

### Exhausted is the tested concept

- Exhausted = NO more content left in their **current** stream
- Exhausted members will receive NEW content added to the stream after their enrollment
- To keep exhausted members engaged, either: (a) add new content to their stream, or (b) use a **transition rule** to move them to another stream
- Marketo flags Exhausted members so you can see who needs attention

## Transition Rules (stream-to-stream movement)

- **Fire when the email in the PRIOR stream delivers** (not when the next one should send)
- Defined per-stream in the Streams tab
- Conditions: smart-list-like filters (e.g. "Clicked link in any stream 1 email" → move to stream 2)
- Execution is asynchronous — not guaranteed instant

### Common exam trap

Transition fires based on the **prior stream's email delivery + behavior**, not on the next send trigger. If a lead doesn't meet any transition criteria when their prior stream email delivers, they stay put.

## Cadence change gotcha

If you change cadence on a live engagement program, existing members adopt the new cadence at their NEXT eligible cast (not retroactively).

---

# 🎨 PART 5 — Channels & Progression Statuses

## Channel basics

- **Channel** = the grouping attribute for a program (Email Blast, Nurture, Event, Webinar, Trade Show, Online Ad, etc.)
- Set when creating a program; drives the **progression statuses** available
- Configured in Admin → Tags → Program Channels
- Each program uses exactly ONE channel

## Progression Statuses per channel

Different channels have different sets of statuses:

### Event channel (examples)

- Invited · Registered · Waitlisted · Attended · No Show · Sent Invite · Responded

**🔴 Event channel rule (tested):** When using type "Event", the system-mapped statuses **Registered**, **Waitlisted**, and **Attended** **cannot be hidden**. You can rename, but structure is required.

### Email Blast channel (examples)

- Sent · Opened · Clicked · Unsubscribed · Bounced · Converted

### Nurture channel (examples)

- Member · Engaged · Converted · Exhausted

## The Success Status — the most-tested concept

- Each channel **must have one** (and only one) status designated as **Success**
- Success = the conversion goal (the "did they actually convert?" flag)
- Success is a **boolean** attached to the status (not a separate state)
- You pick which status = success when creating/editing the channel

### Status vs Success (memorize this distinction)

- **Status** = where the member IS currently in the flow (current step)
- **Success** = did they hit the goal? Attached to specific statuses (e.g. "Attended" for Event)
- A member can have Status = "Attended" AND Success = true simultaneously
- Moving a member FROM a success status to a non-success status UN-marks their success

### Progression rules

- Statuses have a step number (ordered progression)
- Default behavior: status only moves FORWARD (e.g. Invited → Registered → Attended)
- Moving backward requires explicit flow step with "Allow any change" setting
- Hidden statuses don't appear in dropdowns but still exist for historical data

---

# 🏷️ PART 6 — Tokens (inheritance edge cases)

## Token hierarchy (highest to lowest precedence)

1. **Email / Landing Page / Flow Step tokens** (inline, specific use)
2. **Program Token** (program-level My Token)
3. **Folder Token** (folder-level My Token)
4. **Workspace-level tokens** (rarely used)

**Rule: Closest wins.** Program-level `{{my.cost}}` overrides the same token defined at folder level.

## Token types (recognize in questions)

| Type | Use |
|---|---|
| Text | Strings |
| Number | Integer/decimal |
| Rich Text | HTML content |
| Date | Dates (supports arithmetic like `{{my.date,+7}}`) |
| Email Script | Velocity scripting for dynamic email content |
| SFDC Campaign | Linked to Salesforce campaign ID |
| Score | Lead scoring |

## Common gotchas

- Tokens inside a **Local Asset** (like an email in a program) inherit from that program's tokens
- Tokens inside a **Global Asset** (Design Studio email) can ONLY reference system tokens + default values
- Tokens defined INSIDE an Engagement Program's stream inherit from the stream → program chain
- Token value changes apply only to FUTURE sends; emails already sent keep their old values

---

# 📧 PART 7 — Assets quick-deep

## Operational vs Regular Email

| | Operational | Regular (Marketing) |
|---|---|---|
| Respects Unsubscribe? | ❌ No | ✅ Yes |
| Respects Communication Limits? | ❌ No | ✅ Yes |
| Respects Marketing Suspended? | ❌ No | ✅ Yes |
| Respects Blacklist? | ❌ No | ❌ No (nobody gets blacklisted emails) |
| Use cases | Password resets, receipts, legal notices | Campaigns, newsletters, nurture |

**Rule:** Operational email bypass ≠ blacklist bypass. Blacklisted leads NEVER get email regardless.

## Progressive Profiling

- Form shows only missing fields
- Fields asked in **priority order** (configurable)
- **Max fields per visit** = set per form
- Fields marked "Required" always show
- Hidden fields populate silently (e.g. from URL params)

## Form field order of operations

1. **Hidden fields** populate first (URL parameters, page-level setters)
2. **Pre-fill** populates from cookie (if lead identified)
3. **Progressive Profiling** displays remaining priority fields
4. Validation runs on submit

## Snippets

- Reusable HTML/text blocks — update once, propagate everywhere
- **Dynamic snippets** use segmentation to vary per segment
- Snippet changes apply to FUTURE email sends only

## Dynamic Content (in emails)

- Varies based on **Segmentation** (NOT smart list)
- Segmentation must be **approved** before use
- Each lead belongs to exactly ONE segment per segmentation
- Can't edit approved segmentation; must clone to modify

---

# 📊 PART 8 — Reports (smallest section, quick)

## Report → purpose map

| Report | Shows |
|---|---|
| Email Performance | Sends, opens, clicks, unsubs, bounces per email |
| Email Link Performance | Which links got clicks |
| Program Performance | Members by status + success count |
| Lead Performance | Leads acquired over time |
| Company Performance | Company-level engagement (ABM) |
| Landing Page Performance | LP views, conversions |
| People Performance | People created/modified in period |

## RCM + Revenue Explorer (high-level)

- **RCM:** graphical model of Lead → MQL → SAL → SQL → Opp → Customer
- Has Success Paths and Detour Paths (regression allowed)
- Must be **activated** to collect data; ONE active at a time
- **Revenue Explorer:** ad-hoc analysis tool; requires **RCA license**
- **Opportunity Analyzer** / **Program Analyzer** / **Revenue Stage Analysis** are the Analyzers

---

# 🚫 PART 9 — Restrictions & "Cannot Do" Rules (heavy exam traps)

These are the "you cannot directly do X" answers Adobe tests. Each is a real product limitation documented in Adobe Experience League or Marketing Nation. Memorize every line.

## Segmentation restrictions

| Rule | Detail |
|---|---|
| ❌ Cannot edit an APPROVED segmentation directly | Must **Create a Segmentation Draft** first, modify the draft, then re-approve |
| ❌ Cannot delete the **Default segment** | Every segmentation has one; it can't be deleted or renamed |
| ⚠️ Deleting a segmentation has **no undo** | Affects all Dynamic Content in emails, LPs, snippets that reference it |
| ✅ Before approval: can change segment names, order, rules, add/delete segments freely | Draft state is the only time you have full flexibility |
| ⚠️ Approved segmentation used in Dynamic Content | Content tied to segments that are later removed will silently break |

**Best practice:** always check the "Used By" tab on a segmentation before editing/deleting.

## Token restrictions

| Rule | Detail |
|---|---|
| ❌ Cannot delete a token that's **in use** in an email or landing page | Even removing from the asset doesn't always unlock — Marketo may still report it in use |
| ❌ Cannot delete an **overridden** token directly | Workaround: **rename the override token in the program** → inherited value returns → then delete child |
| ⚠️ Token values resolve at **send-time, not create-time** | Changing a token value doesn't retroactively update emails already sent |
| ⚠️ Token precedence: program > folder > workspace | Closest wins; changing inheritance can silently flip values |

## Program restrictions

| Rule | Detail |
|---|---|
| ❌ Cannot delete a program if it contains a **form** used in that same program | Remove the form from use first |
| ❌ Cannot delete a program if **2 smart campaigns reference each other** | Circular reference blocks deletion |
| ❌ Cannot **move programs with members** | Workaround: export members to CSV, remove, move, re-import |
| ❌ Cannot move **child assets out of a program** | Must clone the whole program instead |
| ❌ Cannot convert **program type** (Default → Engagement, etc.) | Must create new program of desired type |
| ❌ Cannot change **channel** on a program with historical member data easily | Can change but progression statuses may not map |

## Cross-workspace restrictions

| Rule | Detail |
|---|---|
| ❌ Cannot **move** assets or programs between workspaces | Must **clone** |
| ❌ Cannot clone cross-workspace without **sharing dependencies first** | Global emails, snippets, LP templates must be shared to destination workspace |
| ✅ Workaround for moving a program across workspaces | Put program in a folder, drag the folder to the other workspace |
| ⚠️ Period costs do NOT clone | Must re-enter in destination program |
| ⚠️ Lists ≥1,000 members clone EMPTY | Must re-populate |

## Trigger Smart Campaign restrictions

| Rule | Detail |
|---|---|
| ⏰ **Auto-deactivation** after 6 months of 0 qualifications | Marketo runs cleanup quarterly |
| 📩 1-week advance notification email | Shows every campaign Marketo plans to deactivate |
| ✅ Reset the clock | (a) Deactivate + reactivate, OR (b) have anyone qualify for the campaign |
| ❌ Cannot edit an active trigger campaign structurally | Must deactivate first, then edit, then re-activate |
| ❌ Deactivating a trigger campaign | Cancels any pending flow actions mid-execution |

## Asset deletion / in-use restrictions

| Asset | Deletion rule |
|---|---|
| **Form** | Cannot delete if used in a landing page or smart campaign |
| **Landing Page** | Cannot delete if in use by a smart campaign |
| **Email** | Cannot delete if in use (sends, smart campaigns, engagement programs) |
| **Smart List** | Cannot delete if referenced by another smart list or smart campaign |
| **Static List** | Cannot delete if used as suppression in a flow |
| **Smart Campaign** | Cannot delete while active — deactivate first |
| **Custom Field** | Admin-only; cannot delete if has data (must export first) |
| **Custom Object** | Cannot delete if has records |

## Approval requirements (all these REQUIRE approval to be usable)

- ✅ **Emails** — approve before use in smart campaigns
- ✅ **Landing Pages** — approve before going live
- ✅ **Forms** — approve before embedding
- ✅ **Email Templates** — approve before new emails can use
- ✅ **Landing Page Templates** — approve before new LPs can use
- ✅ **Segmentations** — approve before use in Dynamic Content
- ✅ **Snippets** — approve before use in emails/LPs
- ⚠️ **Approved with Draft** — approved version is LIVE; draft exists but not published

## Activation requirements

- ✅ **Trigger Smart Campaigns** — must be activated to run (inactive by default after save)
- ✅ **RCM Model** — must be activated to collect data (only ONE active model per instance)
- ✅ **Segmentations** — must be approved to use in Dynamic Content (not "activated" per se)

## Rename rules (what IS renameable vs what isn't)

| Object | Can rename? |
|---|---|
| Program | ✅ Yes (but URL auto-updates for landing pages) |
| Smart Campaign | ✅ Yes |
| Smart List / Static List | ✅ Yes |
| Email | ✅ Yes (but subject line is separate) |
| Landing Page | ✅ Yes (URL updates) |
| Form | ✅ Yes (but breaks embedded forms using URL-based references) |
| **Token** | ❌ Cannot rename — must create new, copy value, delete old |
| **Segmentation (approved)** | ❌ Cannot rename directly — create draft first |
| **Default segment** | ❌ Cannot rename, cannot delete |
| **Custom field** | ✅ Admin UI only; may break reports/smart lists referencing old name |
| **Custom object** | ⚠️ Limited; affects API integrations |

## Dynamic Content restrictions

| Rule | Detail |
|---|---|
| ❌ Cannot use a **Smart List** for Dynamic Content | Must use **Segmentation** |
| ❌ Each lead = exactly ONE segment per segmentation | Overlapping segments not allowed |
| ❌ Default segment always catches leads not matching others | Cannot be removed |

## Flow step restrictions

| Restriction | Detail |
|---|---|
| **Wait step** | Cannot wait beyond the smart campaign's activation window for trigger campaigns |
| **Change Program Status** | Cannot move member to status that doesn't exist in target program's channel |
| **Change Data Value** | Cannot change system-managed fields (e.g. ID, Created At, Updated At) |
| **Operational Email in flow** | Bypasses unsubscribe but STILL blocked by Blacklist and Email Invalid |
| **Add to Engagement Program** | Cannot add to inactive/paused program |

## Communication Limit exceptions

| Email Type | Respects Unsub? | Respects Comm Limit? | Respects Marketing Suspended? | Respects Blacklist? |
|---|---|---|---|---|
| **Regular (Marketing)** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| **Operational** | ❌ No | ❌ No | ❌ No | ✅ Yes (always) |

**Key rule:** No email type can bypass the Blacklist. Blacklist = absolute stop.

## Workspace + Partition hierarchy

| Rule | Detail |
|---|---|
| Each lead belongs to exactly ONE partition | Data-level separation |
| Multiple workspaces can share ONE partition | Workspace is asset-level, partition is lead-level |
| Cannot have a lead in 2 partitions | Move between partitions is a manual action |
| Workspace permissions control asset access | Partition permissions control lead access |

## Miscellaneous gotchas (often tested)

- **Boolean trigger fields** must be set to 'false' explicitly (not empty) for evaluation
- **Smart Campaign Qualification:** by default, lead qualifies ONCE per campaign — "Allow Requalification" toggles this
- **Cloning creates local assets** — original global references become local copies
- **Changing engagement program cadence** applies to future casts only, not retroactively
- **Changing token value** doesn't update already-sent emails
- **Removing a lead from a smart list** doesn't delete the lead — just removes list membership
- **Sync to SFDC flow step** requires the integration to be active; queued if offline
- **Emails require both HTML and Text versions** — Marketo auto-generates text if you don't provide
- **RCM active model: ONE at a time** — switching models resets stage data

---

# 🎯 PART 10 — Known Exam Question Patterns (from actual retake attempts)

These are phrasings confirmed from prior attempts. Each has the definitive answer.

## Q: Which status in an Engagement Program is considered Success? (multiple choice)

**Answer:** **Engaged** is the default Success status for the Engagement channel. Each channel can only have ONE status flagged as Success, but custom channels may add a second success-mapped status like "Converted".

**NOT success:**
- ❌ Member (just enrolled, haven't completed)
- ❌ Exhausted (ran out of content in CURRENT stream — hasn't completed all streams)
- ❌ Paused (member skipped, kept in program)
- ❌ Normal (active, receiving content)

**Success:**
- ✅ **Engaged** (completed ALL streams — default success mapping)
- ✅ Any custom status explicitly flagged as Success in the channel config

**Key distinction to catch in the question wording:**
- "Engaged" = member state AND a program status that is Success-flagged
- "Member state" (Normal/Paused/Exhausted/Engaged) describes engagement program mechanics
- "Program status" is the channel's progression step

## Q: How do you add or restrict people in workspaces?

**Answer:** People don't go into workspaces directly — they go into **Partitions**. Workspaces group **assets**, not people. Three separate concepts:

| Concept | Level | Controls |
|---|---|---|
| **Workspace** | Asset-level | Which assets (programs, templates, emails) a user can see |
| **Partition** | Lead-level | Which leads/people records are grouped together |
| **Role** | User-level | What actions a user can do within their workspaces |

**To add/restrict USERS in a workspace:**
- Admin → Users & Roles → assign role with workspace access permission
- A user can have access to multiple workspaces
- Role defines their action permissions in each workspace

**To assign PEOPLE to a partition:**
- Admin → Database Management → Partitions → Assignment Rules
- Or via flow step: **Change Partition**
- Leads are auto-partitioned by creation rules when added

**Rules that often trip people up:**
- Each lead = exactly ONE partition (can't be in two)
- Each workspace has ONE default partition (for new assets/leads created in it)
- But MULTIPLE workspaces can share the SAME partition
- Permissions cascade: Role → Workspace (asset access) → Partition (lead access)

## Q: Budget added in a prior month — in which month is the goal (success) attributed?

**Answer:** **The month the success event actually OCCURRED** — not the month the budget was entered.

Period Cost and Success are tracked separately by month:

| Item | Attribution |
|---|---|
| Period Cost | Month you ASSIGNED it to (retroactive if added late) |
| Success event | Month it happened (never retroactive) |
| Cost Per Success (CPS) | Calculated per month using that month's Period Cost and that month's Successes |

**Example scenarios:**

| Scenario | Cost month | Success month | CPS calc |
|---|---|---|---|
| Budget $1K set for March, entered in May; 10 successes in March | March | March | $1K / 10 = $100 CPS (March) |
| Budget $1K set for March, entered in May; 10 successes in April | March | April | March CPS = $1K / 0 (if no March successes); April CPS uses April's budget |
| Budget $1K set for March; 5 successes in March, 5 in April | March | Split: 5 Mar + 5 Apr | March CPS = $200; April CPS uses April's budget |

**Key rule:** Retroactive budget entry works — Marketo correctly re-attributes costs to the month you assigned them to. But successes never shift months.

**Common trap:** Don't confuse "month budget was entered" (the calendar day you typed it in) vs. "month the budget is FOR" (what you selected in the drop-down). Only the latter matters for attribution.

---

# ⚡ RAPID-SCAN FLASHCARDS

## Top 20 iron-clad rules

1. **Triggers ALWAYS OR. Never changeable.**
2. **Advanced filter logic needs 3+ filters. "AND before OR" in syntax.**
3. **Smart campaign needs 1+ trigger OR a schedule.**
4. **Clone does NOT transfer period costs.**
5. **Clone does NOT transfer list members for lists ≥1,000 people.**
6. **RCA shows only programs WITH period costs (default).**
7. **Engagement Program cadence: 1, 2, or 4 weeks only.**
8. **Exhausted = no content left in CURRENT stream (not engagement program-wide).**
9. **Transition fires when PRIOR stream email delivers + criteria match.**
10. **Event channel: Registered/Waitlisted/Attended system-mapped, can't hide.**
11. **One Success status per channel.**
12. **Clicks Link implies Opens Email — using both is redundant.**
13. **Approved segmentation cannot be edited — must create a DRAFT first.**
14. **Default segment cannot be deleted or renamed.**
15. **Tokens cannot be deleted while in use in emails/LPs. Cannot be renamed — delete + recreate.**
16. **Overridden tokens: rename the child override to restore inherited value, then delete.**
17. **Cannot MOVE programs between workspaces — must clone (folder-drag workaround).**
18. **Cannot move programs with members — export, remove, move, re-import.**
19. **Trigger SCs auto-deactivate after 6 months of 0 qualifications; quarterly cleanup.**
20. **No email type bypasses Blacklist. Operational bypasses unsub/CL/Marketing Suspended only.**
21. **Engagement Program Success = "Engaged" status only (default). Exhausted ≠ Success.**
22. **People go to Partitions (lead-level), not Workspaces (asset-level). Users go to Workspaces via Roles.**
23. **Period Cost attributes to the month ASSIGNED; Success attributes to the month it OCCURRED. CPS calc uses same-month.**

## 15 distinction table (most-tested)

| A | B | Key |
|---|---|---|
| Filter | Trigger | Filter = narrows audience; Trigger = starts flow |
| AND (ALL) | OR (ANY) | ALL = every filter true; ANY = at least one |
| Standard logic | Advanced logic | Advanced needs 3+ filters with parens |
| Smart Campaign | Engagement Program | SC = one-time/triggered; EP = ongoing w/ streams |
| Batch SC | Trigger SC | Batch = scheduled; Trigger = live event |
| Status | Success | Status = current step; Success = goal-hit boolean |
| Program Cost | Period Cost | Prog Cost = sum; Period = per-month |
| Operational | Regular Email | Oper = bypasses unsub + CL; Reg = respects both |
| Filter constraint | Filter type | Type = WHICH filter; constraint = HOW it evaluates |
| Segment | Segmentation | Segmentation = parent; Segment = child value |
| My Token | System Token | My = custom var; System = auto (`{{lead.X}}`) |
| Lead Partition | Workspace | Partition = lead-level separation; Workspace = asset grouping |
| Exhausted | Engaged | Exhausted = stream done; Engaged = ALL streams done |
| Dynamic Content | Snippet | DC = segmentation-based variants; Snippet = reusable block |
| Cloned (<1000) | Cloned (1000+) | <1000: members clone; ≥1000: list empty |

## Filter constraint operators (recognize)

`is` · `is not` · `contains` · `not contains` · `starts with` · `ends with` · `in list` · `not in list` · `at least N times` · `at most N times` · `exactly N times` · `in past N days` · `in future N days` · `before date` · `after date` · `between dates` · `is empty` · `is not empty` · `any of` · `none of`

## 4 Program Types

- **Default** — general-purpose, blank
- **Engagement** — nurture w/ streams + cadence (1/2/4 weeks)
- **Email** — one-time blast, built-in A/B
- **Event** — webinar/in-person, registration + attendance tracking

## 4 Member states (Engagement Program)

Normal · Paused · Exhausted · Engaged

## Smart Campaign Flow Steps (key ones)

Send Email · Change Data Value · Add to List · Remove from List · Change Program Status · Change Score · Wait · Send Alert · Interesting Moment · Sync to SFDC · Add to Engagement Program · Change Engagement Program Stream · Remove from Flow · Change Owner

## The 7 System Smart Lists

All People · Possible Duplicates · Marketing Suspended · Blacklist · Unsubscribed · Email Invalid · Normal Leads

## Critical edge cases (often tested traps)

- **WAS vs WAS NOT** are OPPOSITES — watch the wording
- **Clicks Link in Email** implies **Opens Email** (redundant together)
- **Attended** implies **Registered** (chain)
- **Triggers use OR among themselves, ALWAYS**
- **Period cost set per MONTH**, not as lifetime total
- **Cloning creates local assets; cross-workspace requires pre-sharing dependencies**
- **Boolean trigger fields** must be explicitly set to 'false' (not empty) for evaluation
- **Marketing Suspended** blocks marketing email but NOT operational email
- **Change Engagement Program Stream** is the flow step that moves a lead between streams
- **Revoke Lead Status** undoes the Program Status change

## Final exam-day protocol

1. **Read each question twice** before looking at options
2. **Identify keyword:** BEST / MOST / PRIMARY = pick closest right; ALWAYS / NEVER = usually wrong
3. **On trigger vs filter questions, first ask: is this live-event or static-criteria?**
4. **On program cloning questions, first ask: is this asset or member-level?**
5. **On period cost questions, default answer is "yes, required for reporting"**
6. **Two-pass:** confident first, mark-and-return later
7. **60-65 sec/question pacing** — use the full 110 minutes

---

## Sources (Adobe Experience League + Marketing Nation)

- [Understanding smart campaigns: Triggers and filters](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-28480)
- [Using Standard Smart List Rule Logic](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/using-smart-campaigns/using-standard-smart-list-rule-logic)
- [Using Advanced Smart List Rule Logic](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/using-smart-lists/using-advanced-smart-list-rule-logic)
- [Clone a Program](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/programs/working-with-programs/clone-a-program)
- [Edit a Segmentation](https://experienceleague.adobe.com/docs/marketo/using/product-docs/personalization/segmentation-and-snippets/segmentation/edit-a-segmentation.html)
- [Deactivate a Trigger Smart Campaign](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/using-smart-campaigns/deactivate-a-trigger-smart-campaign-schedule-tab)
- [Automatic Trigger Campaign Cleanup](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/using-smart-campaigns/automatic-trigger-campaign-cleanup)
- [Create a Program Channel](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/tags/create-a-program-channel)
- [Change Program Status](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/program-flow-actions/change-program-status)
- [Why You Need Period Costs for Reporting](https://nation.marketo.com/t5/marketo-whisperer-blogs/why-you-need-period-costs-for-reporting/bc-p/247309)
- [Cannot move assets into new workspace](https://experienceleaguecommunities.adobe.com/adobe-marketo-engage-27/cannot-move-assets-into-new-workspace-161931)
- [How to delete an Overridden token](https://nation.marketo.com/t5/product-discussions/how-to-delete-an-overridden-token/td-p/97876)
- [Conquering Smart List Logic](https://experienceleague.adobe.com/en/perspectives/conquering-smart-list-logic-to-reach-your-campaign-audience)
