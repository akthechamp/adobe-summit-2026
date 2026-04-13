# AI Forte Logo Revisit — Icon Redesign Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use `svg-logo-designer` skill to generate the actual SVG variations during execution. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the current AI Forte orchestration icon with a more crafted, distinctive mark grounded in the brand name's actual symbolic territory (music dynamics, strength, expertise) — not a generic AI network diagram.

**Approach:** Explore the name's latent meaning first, generate 5 concept directions as SVGs using the installed `svg-logo-designer` skill, review side-by-side, pick one, then produce full lockup variations.

**Skill dependency:** `svg-logo-designer` (installed at `~/.claude/skills/svg-logo-designer/`) — will be available in the next Claude Code session. Use it during Phase 2 concept generation.

**Status:** Plan only — execution deferred until user is ready.

---

## Context: Why the current icon fails

The current mark in `resources/logo/ai-forte-logo.png` and `ai-forte-icon.png` shows a central espresso circle surrounded by four sienna satellite nodes connected by hairline curves — a literal "orchestration network."

Problems:

1. **Too literal.** Every AI agent startup in 2026 uses network node iconography. It's the visual cliché of the category. A Forbes search for "AI agent startup logo" returns the same 4-node network fifty times.

2. **Doesn't feel crafted.** It reads as "AI-generated" because it was — procedurally described ("one central node + satellites + hairlines") rather than deliberately composed. Real brand marks have asymmetric intention, negative space play, letterform craft. This has none.

3. **Ignores the name.** "Forte" is one of the most evocative words in branding — **musical forte dynamic marking (loud/strong)**, **French word for strong/fortress**, and the English idiom "one's forte" meaning area of expertise/strength. We gave all of that up for "network nodes" because we only thought about the "AI" half.

4. **Not distinctive at small sizes.** At 16px (favicon size), the 4 satellite nodes merge with the central node and become a brown blob. A great logo has a recognizable silhouette at thumbnail size.

5. **Gender-neutral, fine — but personality-neutral, not fine.** The current mark has no attitude. It could be a molecule, a wifi diagram, a social network, a CPU, an atom. That's the opposite of a memorable brand.

### Evidence

Compare against brands that got this right:
- **Stripe** — crafted "S" with clever gradient hand, infinitely scalable
- **Linear** — abstract geometric mark with custom angles, doesn't look like anything but Linear
- **Anthropic** — a single shape with asymmetric weight, architectural
- **Notion** — letterform "N" that's also a stack of pages, obvious in hindsight
- **Raycast** — gradient ray burst, bold stance
- **Framer** — simple "F" with a unique twist, works at any size

None of them are network diagrams. None look generic. All of them "mean something" when you see them and think about the brand name.

---

## Phase 1: Brand name exploration (no files)

Before any pixels get drawn, we explore the symbolic territory the name "AI Forte" actually offers. This phase produces a written concept brief — not an image.

### Task 1: Write the brand concept brief

**Files:**
- Create: `resources/logo/concept-brief.md`

- [ ] **Step 1: Document the three meanings of "Forte"**

  Create `resources/logo/concept-brief.md` with:

  ```markdown
  # AI Forte — Brand Concept Brief

  ## The name unlocks three symbolic territories

  ### 1. Musical — "Forte" as dynamic marking
  In music notation, *forte* (f) means "loud / strong." It's written as a stylized
  italic lowercase **f** — one of the most recognizable symbols in Western notation.
  Its sibling dynamics form a family: piano (p), mezzo-forte (mf), fortissimo (ff).
  A crescendo mark (<) builds INTO forte. An AI Forte logo rooted here could use:
  - The italic f glyph itself (too obvious on its own, but powerful as a hidden form)
  - A crescendo wedge suggesting growth, amplification, building volume
  - Dynamic marking notation style: italic + weighted + gestural
  - Conductor's baton as a verb of orchestration (connects to the positioning)

  ### 2. Architectural — "Fort/Forte" as strength and structure
  French *fort* means "strong." A *forte* (obsolete military term) is a fortress,
  a stronghold, the strongest line of defense. Symbolically:
  - Pillar, column, bracket — bearing weight
  - Bastion walls, crenellations (more historical than modern)
  - Weight distribution, foundation, base
  - Monumental typography (Trajan Column)

  ### 3. Idiomatic — "Someone's forte" as mastery / expertise
  English usage: "agent orchestration is their forte." Signals:
  - Craftsmanship, deliberate skill
  - A specific area someone dominates
  - Quiet confidence, "we know this cold"
  - Not "we do everything" — specifically "we do THIS"

  ## What should the mark mean?

  AI Forte = "AI is our forte." The agency has AI agent orchestration as its
  specific craft strength. The mark should communicate **mastery + strength +
  dynamic expression** — not "network of nodes."

  ## Brand personality anchors

  - **Confident, not loud.** The name is already forte — the mark should be a
    whisper, not a shout. Subtle can be stronger than literal.
  - **Crafted, not generated.** Asymmetric, intentional, has a single "hero move."
  - **Musical over technical.** Lean into the dynamic marking heritage. Tech
    brands using technical icons are a dime a dozen. A tech brand using musical
    typography would stand apart.
  - **Warm.** The locked palette is warm premium. The mark should feel hand-drawn
    or letterpress, not digital or geometric.

  ## What to avoid

  - Network diagrams (the current mistake)
  - Brain iconography (lowest common denominator of AI branding)
  - Spark/lightning bolts (startup cliché)
  - Generic "A" or "F" letterforms with no twist
  - 3D / glow / gradients (conflicts with Palette A flat aesthetic)
  - Anything that looks like a wifi signal, atom, or molecule
  ```

- [ ] **Step 2: Commit the brief**

  ```bash
  cd "/Users/ashishkumar/Projects/Ashish Kumar/Adobe Summit 2026"
  git add resources/logo/concept-brief.md
  git commit -m "docs(logo): add brand concept brief for icon revisit"
  ```

---

## Phase 2: Generate 5 concept directions

Use the `svg-logo-designer` skill (installed at `~/.claude/skills/svg-logo-designer/`) to produce 5 distinct SVG concept directions. Each direction has:
- A primary SVG icon (square, 64×64 viewBox)
- A horizontal wordmark lockup SVG (for comparison)
- A 2-sentence rationale

### Task 2: Invoke svg-logo-designer for concept generation

**Files:**
- Create: `resources/logo/concepts/01-musical-f/icon.svg`
- Create: `resources/logo/concepts/01-musical-f/lockup.svg`
- Create: `resources/logo/concepts/02-crescendo/icon.svg`
- Create: `resources/logo/concepts/02-crescendo/lockup.svg`
- Create: `resources/logo/concepts/03-pillar/icon.svg`
- Create: `resources/logo/concepts/03-pillar/lockup.svg`
- Create: `resources/logo/concepts/04-monogram-af/icon.svg`
- Create: `resources/logo/concepts/04-monogram-af/lockup.svg`
- Create: `resources/logo/concepts/05-conductor-arc/icon.svg`
- Create: `resources/logo/concepts/05-conductor-arc/lockup.svg`

- [ ] **Step 1: Create the concepts directory structure**

  ```bash
  cd "/Users/ashishkumar/Projects/Ashish Kumar/Adobe Summit 2026"
  mkdir -p resources/logo/concepts/01-musical-f \
           resources/logo/concepts/02-crescendo \
           resources/logo/concepts/03-pillar \
           resources/logo/concepts/04-monogram-af \
           resources/logo/concepts/05-conductor-arc
  ```

- [ ] **Step 2: Invoke svg-logo-designer with Concept 1 — Musical F**

  Use the `Skill` tool:
  ```
  Skill: svg-logo-designer
  Args: (paste the full brief below)
  ```

  Brief to provide:

  ```
  Create an SVG logo for "AI Forte," an AI agent orchestration agency.

  CONCEPT: "Musical F" — the mark is a stylized italic lowercase letterform "f"
  that functions as both the musical forte dynamic marking AND as the second half
  of the brand name. Treatment: bold italic serif-lite letterform, asymmetric
  weight distribution (heavier bottom stem, lighter top crossbar), with a subtle
  diagonal emphasis that suggests forward motion or crescendo.

  TYPE: Combination mark (icon + wordmark). The icon is the stylized f. The
  wordmark reads "AI Forte" in a bold condensed sans-serif.

  STYLE: Minimalist, crafted, editorial. Reference: Aesop brand identity,
  Kinfolk magazine mastheads, Wallpaper magazine brand marks. Not tech-startup
  style — closer to a design-led consultancy.

  COLORS (from Palette A — Warm Premium, locked):
  - Background: warm cream #F8F3EC
  - Foreground / "Forte" text: deep espresso #2C1810
  - Accent / "AI" text + icon: burnt sienna #C65D2E
  - Muted: warm taupe #8B7355

  CONSTRAINTS:
  - Flat color only. NO gradients, NO glow, NO 3D, NO shadows.
  - The f letterform should be recognizable at 16px (favicon size).
  - Must work as an icon-only square mark AND as a horizontal lockup.
  - Hand-drawn or letterpress feel over geometric precision.
  - Avoid: network diagrams, sparks, brain imagery, technical iconography.

  DELIVERABLES:
  - icon.svg: 64×64 viewBox, centered, icon only
  - lockup.svg: 400×80 viewBox, horizontal icon + wordmark lockup
  - Both files should be clean, optimized SVG without unnecessary attributes.

  Save to:
  - resources/logo/concepts/01-musical-f/icon.svg
  - resources/logo/concepts/01-musical-f/lockup.svg
  ```

- [ ] **Step 3: Invoke svg-logo-designer with Concept 2 — Crescendo**

  ```
  Skill: svg-logo-designer
  ```

  Brief:

  ```
  Create an SVG logo for "AI Forte," an AI agent orchestration agency.

  CONCEPT: "Crescendo" — the mark is the musical crescendo symbol (<), a wedge
  opening rightward, suggesting growth, amplification, building toward forte.
  The wedge is drawn with calligraphic variable stroke weight (thicker at the
  open end, tapered at the point) for a confident, hand-drawn quality. Negative
  space inside the wedge forms a subtle secondary shape — possibly an "f" or an
  arrow. Positioned so it reads as "building toward strength."

  TYPE: Combination mark. Icon = crescendo wedge. Wordmark = "AI Forte".

  STYLE: Minimalist, editorial, confident gesture. Reference: musical notation
  manuscripts, calligraphic brand marks, architectural bracket forms.

  COLORS: (Palette A — same as Concept 1)
  - Background: #F8F3EC warm cream
  - Foreground: #2C1810 deep espresso
  - Accent (the crescendo wedge + "AI" text): #C65D2E burnt sienna
  - Muted: #8B7355 warm taupe

  CONSTRAINTS:
  - Flat color, no gradients, no effects.
  - The crescendo wedge should be recognizable at 16px — sharp silhouette.
  - Asymmetric weight distribution gives the mark personality.
  - Must work icon-only AND as horizontal lockup.

  DELIVERABLES:
  - icon.svg: 64×64 viewBox
  - lockup.svg: 400×80 viewBox horizontal lockup

  Save to:
  - resources/logo/concepts/02-crescendo/icon.svg
  - resources/logo/concepts/02-crescendo/lockup.svg
  ```

- [ ] **Step 4: Invoke svg-logo-designer with Concept 3 — Pillar**

  ```
  Skill: svg-logo-designer
  ```

  Brief:

  ```
  Create an SVG logo for "AI Forte," an AI agent orchestration agency.

  CONCEPT: "Pillar" — an abstract architectural bracket or column form. Two
  vertical elements of unequal height, connected by a subtle horizontal lintel
  at the top — evoking a stylized gate, a bracket, or a Doric column capital.
  Represents "strength, foundation, forte = fortress." The form is confident,
  bearing weight, with intentional asymmetry (one column taller/bolder).

  TYPE: Combination mark. Icon = abstract pillar/bracket. Wordmark = "AI Forte".

  STYLE: Architectural, minimalist, monumental. Reference: Trajan column
  inscriptions, Brutalist architecture brand marks, Swiss modernist logos
  (Saul Bass era), Japanese kamon family crests.

  COLORS: (Palette A)
  - Background: #F8F3EC warm cream
  - Foreground: #2C1810 deep espresso
  - Accent: #C65D2E burnt sienna (one column or the lintel)
  - Muted: #8B7355 warm taupe

  CONSTRAINTS:
  - Flat color, geometric precision.
  - Silhouette must be instantly recognizable as "bracket / pillar / gate" —
    not a T, not an H, something distinctive.
  - Asymmetric — NOT perfectly symmetrical (that would read as generic H or П).
  - Work at 16px with clear silhouette.

  DELIVERABLES:
  - icon.svg: 64×64 viewBox
  - lockup.svg: 400×80 viewBox horizontal lockup

  Save to:
  - resources/logo/concepts/03-pillar/icon.svg
  - resources/logo/concepts/03-pillar/lockup.svg
  ```

- [ ] **Step 5: Invoke svg-logo-designer with Concept 4 — Monogram AF**

  ```
  Skill: svg-logo-designer
  ```

  Brief:

  ```
  Create an SVG logo for "AI Forte," an AI agent orchestration agency.

  CONCEPT: "Monogram AF" — a custom ligature that fuses "A" and "F" into a
  single letterform. The crossbar of the A extends to become the top horizontal
  of the F. The vertical stem of the F doubles as one leg of the A. Negative
  space between letters is intentional and balanced. Treatment: geometric
  sans-serif, bold weight, slightly condensed, hand-tuned proportions.

  TYPE: Lettermark / monogram. The monogram IS the icon. A horizontal lockup
  pairs the monogram with the full "AI Forte" wordmark.

  STYLE: Custom letterform craft, editorial. Reference: HBO lettermark,
  Chanel CC monogram, Volkswagen VW, Louis Vuitton LV — letterform fusion
  done with care. Confident, timeless, typographic craft.

  COLORS: (Palette A)
  - Background: #F8F3EC warm cream
  - Foreground: #2C1810 deep espresso
  - Accent: #C65D2E burnt sienna (used for the "A" part of the fusion)
  - Muted: #8B7355 warm taupe

  CONSTRAINTS:
  - Flat color, bold geometric weight.
  - Must be a genuine fusion — not just A next to F. Shared strokes.
  - Works at 16px (favicon) and 400px (website header).
  - Color split can emphasize the fusion (A in sienna, F in espresso where they overlap gets sienna).

  DELIVERABLES:
  - icon.svg: 64×64 viewBox
  - lockup.svg: 400×80 viewBox (monogram left, wordmark "AI Forte" right)

  Save to:
  - resources/logo/concepts/04-monogram-af/icon.svg
  - resources/logo/concepts/04-monogram-af/lockup.svg
  ```

- [ ] **Step 6: Invoke svg-logo-designer with Concept 5 — Conductor Arc**

  ```
  Skill: svg-logo-designer
  ```

  Brief:

  ```
  Create an SVG logo for "AI Forte," an AI agent orchestration agency.

  CONCEPT: "Conductor Arc" — a single, confident curved stroke representing a
  conductor's baton gesture. The stroke has variable weight (thin-to-thick-to-thin)
  like a calligraphic brushstroke, curving in a J or fermata shape. Connects
  conceptually to "orchestration" (conductor = orchestrator) while avoiding the
  network-diagram cliché. Reads as gesture, motion, direction, deliberate movement.

  TYPE: Abstract mark. A single brushstroke-like form. Wordmark pairs beside.

  STYLE: Gestural, hand-drawn, Zen brushstroke quality. Reference: Muji brand
  mark simplicity, Japanese enso circle, Nike swoosh (for gestural confidence),
  calligraphic flourishes. Feels "drawn once, never redrawn."

  COLORS: (Palette A)
  - Background: #F8F3EC warm cream
  - Stroke: #C65D2E burnt sienna (full gesture is sienna)
  - Wordmark: "AI" in sienna, "Forte" in #2C1810 espresso
  - Muted: #8B7355 warm taupe

  CONSTRAINTS:
  - Single stroke or compound curve — NOT multiple separate shapes.
  - Variable stroke weight is essential (otherwise it looks generic).
  - Must work at 16px — the silhouette should be clearly "a gesture."
  - No geometric precision — this is the hand-drawn concept.

  DELIVERABLES:
  - icon.svg: 64×64 viewBox
  - lockup.svg: 400×80 viewBox horizontal lockup

  Save to:
  - resources/logo/concepts/05-conductor-arc/icon.svg
  - resources/logo/concepts/05-conductor-arc/lockup.svg
  ```

- [ ] **Step 7: Commit all 5 concepts**

  ```bash
  git add resources/logo/concepts/
  git commit -m "feat(logo): generate 5 icon concept directions via svg-logo-designer"
  ```

---

## Phase 3: Side-by-side comparison preview

Build a single HTML page that renders all 5 concepts side-by-side at multiple sizes, so the user can review them in one place and pick a winner.

### Task 3: Build the concept comparison preview

**Files:**
- Create: `resources/logo/concepts/preview.html`

- [ ] **Step 1: Write the comparison HTML**

  Create `resources/logo/concepts/preview.html` with a 5-column grid. Each column shows:
  1. Concept name + rationale
  2. Icon at 96×96 (hero size)
  3. Icon at 48×48 (medium — business card size)
  4. Icon at 16×16 (favicon test)
  5. Horizontal lockup at full size
  6. Lockup on dark background (to test inversion — useful for the dark theme companion)

  Skeleton:

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  <meta charset="UTF-8">
  <title>AI Forte — Logo Concepts</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Inter', sans-serif;
      background: #EDEEF1;
      padding: 40px 24px;
    }
    h1 { font-size: 28px; font-weight: 800; margin-bottom: 8px; color: #1A1D24; }
    .page-sub { font-size: 14px; color: #6B6F78; margin-bottom: 32px; max-width: 600px; }
    .grid {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 20px;
      max-width: 2100px;
    }
    @media (max-width: 1800px) { .grid { grid-template-columns: repeat(3, 1fr); } }
    @media (max-width: 1100px) { .grid { grid-template-columns: repeat(2, 1fr); } }
    @media (max-width: 700px) { .grid { grid-template-columns: 1fr; } }
    .concept {
      background: #fff;
      border-radius: 16px;
      padding: 24px;
      box-shadow: 0 4px 24px rgba(0,0,0,0.06);
    }
    .concept h2 { font-size: 14px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; color: #1A1D24; margin-bottom: 4px; }
    .concept .code { font-size: 11px; color: #999; font-family: monospace; margin-bottom: 12px; }
    .concept p { font-size: 12px; color: #555; line-height: 1.5; margin-bottom: 20px; }
    .sizes { display: flex; align-items: center; gap: 24px; background: #F8F3EC; padding: 20px; border-radius: 10px; margin-bottom: 14px; }
    .sizes img, .sizes object { display: block; }
    .size-96 { width: 96px; height: 96px; }
    .size-48 { width: 48px; height: 48px; }
    .size-16 { width: 16px; height: 16px; }
    .size-label { font-size: 9px; color: #8B7355; text-transform: uppercase; margin-top: 4px; text-align: center; }
    .lockup-box {
      background: #F8F3EC;
      padding: 16px 20px;
      border-radius: 8px;
      margin-bottom: 8px;
    }
    .lockup-box object { width: 100%; max-height: 60px; }
    .lockup-box.dark { background: #0B0F1F; }
  </style>
  </head>
  <body>

  <h1>AI Forte — Logo Concept Comparison</h1>
  <p class="page-sub">Five concept directions rooted in the brand name's symbolic territory — music, strength, expertise. Pick the one that feels right, or tell Claude which two to merge.</p>

  <div class="grid">

    <div class="concept">
      <h2>Musical F</h2>
      <div class="code">01-musical-f</div>
      <p>Stylized italic lowercase <em>f</em> that functions as both the musical forte dynamic marking and the second half of the brand name. Asymmetric weight, gestural serif.</p>
      <div class="sizes">
        <div><object data="01-musical-f/icon.svg" class="size-96"></object><div class="size-label">96</div></div>
        <div><object data="01-musical-f/icon.svg" class="size-48"></object><div class="size-label">48</div></div>
        <div><object data="01-musical-f/icon.svg" class="size-16"></object><div class="size-label">16</div></div>
      </div>
      <div class="lockup-box"><object data="01-musical-f/lockup.svg"></object></div>
      <div class="lockup-box dark"><object data="01-musical-f/lockup.svg"></object></div>
    </div>

    <div class="concept">
      <h2>Crescendo</h2>
      <div class="code">02-crescendo</div>
      <p>Musical crescendo wedge (<) with calligraphic variable stroke weight. Suggests growth, amplification, building toward strength. Confident single-gesture mark.</p>
      <div class="sizes">
        <div><object data="02-crescendo/icon.svg" class="size-96"></object><div class="size-label">96</div></div>
        <div><object data="02-crescendo/icon.svg" class="size-48"></object><div class="size-label">48</div></div>
        <div><object data="02-crescendo/icon.svg" class="size-16"></object><div class="size-label">16</div></div>
      </div>
      <div class="lockup-box"><object data="02-crescendo/lockup.svg"></object></div>
      <div class="lockup-box dark"><object data="02-crescendo/lockup.svg"></object></div>
    </div>

    <div class="concept">
      <h2>Pillar</h2>
      <div class="code">03-pillar</div>
      <p>Abstract architectural bracket — two vertical columns of unequal height joined by a lintel. Represents strength, foundation, fortress. Monumental geometry.</p>
      <div class="sizes">
        <div><object data="03-pillar/icon.svg" class="size-96"></object><div class="size-label">96</div></div>
        <div><object data="03-pillar/icon.svg" class="size-48"></object><div class="size-label">48</div></div>
        <div><object data="03-pillar/icon.svg" class="size-16"></object><div class="size-label">16</div></div>
      </div>
      <div class="lockup-box"><object data="03-pillar/lockup.svg"></object></div>
      <div class="lockup-box dark"><object data="03-pillar/lockup.svg"></object></div>
    </div>

    <div class="concept">
      <h2>Monogram AF</h2>
      <div class="code">04-monogram-af</div>
      <p>Custom ligature fusing A and F into a single letterform with shared strokes. Typographic craft, HBO-meets-Aesop discipline.</p>
      <div class="sizes">
        <div><object data="04-monogram-af/icon.svg" class="size-96"></object><div class="size-label">96</div></div>
        <div><object data="04-monogram-af/icon.svg" class="size-48"></object><div class="size-label">48</div></div>
        <div><object data="04-monogram-af/icon.svg" class="size-16"></object><div class="size-label">16</div></div>
      </div>
      <div class="lockup-box"><object data="04-monogram-af/lockup.svg"></object></div>
      <div class="lockup-box dark"><object data="04-monogram-af/lockup.svg"></object></div>
    </div>

    <div class="concept">
      <h2>Conductor Arc</h2>
      <div class="code">05-conductor-arc</div>
      <p>Single confident brushstroke suggesting a conductor's baton gesture. Variable stroke weight, Zen calligraphy quality. Orchestration without literalism.</p>
      <div class="sizes">
        <div><object data="05-conductor-arc/icon.svg" class="size-96"></object><div class="size-label">96</div></div>
        <div><object data="05-conductor-arc/icon.svg" class="size-48"></object><div class="size-label">48</div></div>
        <div><object data="05-conductor-arc/icon.svg" class="size-16"></object><div class="size-label">16</div></div>
      </div>
      <div class="lockup-box"><object data="05-conductor-arc/lockup.svg"></object></div>
      <div class="lockup-box dark"><object data="05-conductor-arc/lockup.svg"></object></div>
    </div>

  </div>

  </body>
  </html>
  ```

- [ ] **Step 2: Open in browser and inspect all 5 concepts**

  ```bash
  open resources/logo/concepts/preview.html
  ```

  Expected: a 5-column grid (or fewer on smaller screens) showing each concept at 96px, 48px, 16px sizes, plus horizontal lockups on both cream and dark backgrounds.

- [ ] **Step 3: Commit**

  ```bash
  git add resources/logo/concepts/preview.html
  git commit -m "feat(logo): add side-by-side concept comparison preview"
  ```

---

## Phase 4: Pick winner + iterate

**This phase requires user decision.** Execution pauses here until the user names a winner.

### Task 4: User picks winning concept

- [ ] **Step 1: User reviews `preview.html` and decides**

  Possible outcomes:
  - **"Concept N wins, ship it as-is"** → skip to Task 5
  - **"Concept N wins, but change X"** → Task 4a below
  - **"I like parts of N and M, merge them"** → Task 4b below
  - **"None of them work, try again with new directions"** → loop back to Phase 1 with user feedback

- [ ] **Step 2 (Task 4a — refine a single concept)**

  Re-invoke `svg-logo-designer` with the winning concept's brief PLUS the specific tweak the user requested. Save the refined version to `resources/logo/concepts/{N}-*/icon-v2.svg` and `lockup-v2.svg`. Update `preview.html` to include the v2 versions. User re-reviews.

- [ ] **Step 3 (Task 4b — merge two concepts)**

  Re-invoke `svg-logo-designer` with a new concept brief that combines elements from both winners. Save as `resources/logo/concepts/06-hybrid/icon.svg` + `lockup.svg`. User reviews the hybrid.

---

## Phase 5: Produce full lockup system for the winner

Once a winner is locked, generate the complete logo system in 5 layout variations.

### Task 5: Generate winner's full logo system

**Files (winner denoted as `{W}`):**
- Create: `resources/logo/ai-forte-logo-horizontal.svg`
- Create: `resources/logo/ai-forte-logo-vertical.svg`
- Create: `resources/logo/ai-forte-logo-icon.svg`
- Create: `resources/logo/ai-forte-logo-wordmark.svg`
- Create: `resources/logo/ai-forte-logo-reversed.svg` (for dark backgrounds)

- [ ] **Step 1: Remove the old AI-generated logo files**

  ```bash
  cd "/Users/ashishkumar/Projects/Ashish Kumar/Adobe Summit 2026"
  rm resources/logo/ai-forte-logo.png resources/logo/ai-forte-icon.png
  ```

- [ ] **Step 2: Invoke svg-logo-designer for the full layout system**

  ```
  Skill: svg-logo-designer
  ```

  Brief:

  ```
  We've picked Concept {W} from resources/logo/concepts/{W}-*/ as the final AI Forte mark.

  Read these source files:
  - resources/logo/concepts/{W}-*/icon.svg
  - resources/logo/concepts/{W}-*/lockup.svg

  Produce 5 production-ready variations of this mark:

  1. HORIZONTAL LOCKUP (primary)
     - Icon left, wordmark "AI Forte" right
     - Use: website header, one-pager header, email signature
     - Dimensions: 400×80 viewBox

  2. VERTICAL LOCKUP
     - Icon top, wordmark below, centered
     - Use: social media profiles, mobile app splash, square placements
     - Dimensions: 200×240 viewBox

  3. ICON ONLY
     - Icon alone, square
     - Use: favicon, app icon, profile picture, small-space accent
     - Dimensions: 64×64 viewBox

  4. WORDMARK ONLY
     - Text only, no icon
     - Use: minimal applications, email body, inline text
     - Dimensions: 300×60 viewBox

  5. REVERSED (for dark backgrounds)
     - Primary horizontal lockup but with cream (#F8F3EC) replacing the
       espresso (#2C1810) as the foreground color, for use on dark theme surfaces
       (the astro-site dark mode hero, dark business cards, etc.)
     - Dimensions: 400×80 viewBox

  COLORS (Palette A — locked brand system):
  - Primary background: #F8F3EC cream (except reversed, which is transparent)
  - Primary foreground: #2C1810 espresso (cream in reversed)
  - Accent: #C65D2E burnt sienna (same in both primary and reversed)

  CONSTRAINTS:
  - Flat color only, no gradients, no effects.
  - All 5 files must feel like the same mark — same proportions, same spirit,
    no accidental redesigns.
  - Each file must be clean optimized SVG.
  - Include accessibility: <title> and <desc> elements in each SVG.

  Save to:
  - resources/logo/ai-forte-logo-horizontal.svg
  - resources/logo/ai-forte-logo-vertical.svg
  - resources/logo/ai-forte-logo-icon.svg
  - resources/logo/ai-forte-logo-wordmark.svg
  - resources/logo/ai-forte-logo-reversed.svg
  ```

- [ ] **Step 3: Verify each file renders correctly**

  Open each file in the browser:
  ```bash
  open resources/logo/ai-forte-logo-horizontal.svg
  open resources/logo/ai-forte-logo-vertical.svg
  open resources/logo/ai-forte-logo-icon.svg
  open resources/logo/ai-forte-logo-wordmark.svg
  ```

  For the reversed variant, open a dark test HTML:
  ```html
  <!-- Save as /tmp/reversed-test.html -->
  <!DOCTYPE html><html><body style="background:#0B0F1F;padding:60px;">
  <object data="file:///Users/ashishkumar/Projects/Ashish%20Kumar/Adobe%20Summit%202026/resources/logo/ai-forte-logo-reversed.svg"></object>
  </body></html>
  ```

- [ ] **Step 4: Commit**

  ```bash
  git add resources/logo/
  git rm --cached resources/logo/ai-forte-logo.png 2>/dev/null || true
  git rm --cached resources/logo/ai-forte-icon.png 2>/dev/null || true
  git commit -m "feat(logo): lock concept {W}, produce full 5-layout SVG system"
  ```

---

## Phase 6: Update all downstream assets

The old icon appears in 9 places across `resources/`. Each one needs to be regenerated with the new mark. Some are easy (SVG swap), some require re-generating raster images.

### Task 6: Update collateral assets

- [ ] **Step 1: Update the primary logo PNG via nano-banana-pro-openrouter**

  The existing `resources/logo/ai-forte-logo.png` (raster) was generated via Nano Banana Pro. We now have a cleaner SVG source, so the raster can be produced by either:

  (a) Converting SVG directly to PNG via ImageMagick:
  ```bash
  cd "/Users/ashishkumar/Projects/Ashish Kumar/Adobe Summit 2026"
  magick -background "#F8F3EC" -density 400 \
    resources/logo/ai-forte-logo-horizontal.svg \
    resources/logo/ai-forte-logo.png
  magick -background "#F8F3EC" -density 400 \
    resources/logo/ai-forte-logo-icon.svg \
    resources/logo/ai-forte-icon.png
  ```

  (b) Or re-generating with Nano Banana Pro using the updated concept as visual reference (via `--input-image`).

  Option (a) is faster and produces a pixel-perfect raster from the SVG. Use (a).

- [ ] **Step 2: Regenerate LinkedIn banner with new icon**

  The LinkedIn banner at `resources/linkedin/ai-forte-linkedin-banner.png` embeds the old icon. Re-generate via nano-banana-pro-openrouter, passing the new primary logo as an `--input-image` reference so the model reuses the updated mark:

  ```bash
  cd "/Users/ashishkumar/Projects/Ashish Kumar/Adobe Summit 2026"
  uv run /Users/ashishkumar/.claude/skills/nano-banana-pro-openrouter/scripts/generate_image.py \
    --resolution 2K \
    --input-image resources/logo/ai-forte-logo-horizontal.svg \
    --filename resources/linkedin/ai-forte-linkedin-banner.png \
    --prompt "$(cat resources/generation-plan.md | sed -n '/### 3\. LinkedIn/,/### 4\./p')"
  ```

  Note: SVG input may or may not be supported by the model. If it fails, convert SVG to PNG first (Step 1 method), then pass the PNG.

- [ ] **Step 3: Regenerate OG image**

  Same pattern as Step 2 but for `resources/og/ai-forte-og-image.png` with the OG prompt from `generation-plan.md`.

- [ ] **Step 4: Regenerate social post template**

  Same pattern, `resources/social/ai-forte-post-template.png`.

- [ ] **Step 5: Regenerate Summit announcement**

  Same pattern, `resources/social/ai-forte-summit-announcement.png`.

- [ ] **Step 6: Regenerate business card cover**

  Same pattern, `resources/business-card/ai-forte-business-card.png`.

- [ ] **Step 7: Regenerate one-pager header**

  Same pattern, `resources/one-pager/ai-forte-one-pager-header.png`.

- [ ] **Step 8: Update astro-site logo references**

  In `astro-site/public/`, add the new SVG logo files:
  ```bash
  cp resources/logo/ai-forte-logo-horizontal.svg astro-site/public/logo.svg
  cp resources/logo/ai-forte-logo-icon.svg astro-site/public/favicon.svg
  cp resources/logo/ai-forte-logo-reversed.svg astro-site/public/logo-dark.svg
  ```

  Then update `astro-site/src/components/astro/Navbar.astro` and `Footer.astro` to reference the SVG (inline or via `<img>`). This is a separate commit in the astro-site repo.

- [ ] **Step 9: Commit the parent repo updates**

  ```bash
  cd "/Users/ashishkumar/Projects/Ashish Kumar/Adobe Summit 2026"
  git add resources/
  git commit -m "feat(logo): regenerate all downstream assets with new icon"
  ```

- [ ] **Step 10: Commit the astro-site repo updates**

  ```bash
  cd astro-site
  git add public/logo.svg public/favicon.svg public/logo-dark.svg \
          src/components/astro/Navbar.astro \
          src/components/astro/Footer.astro
  git commit -m "feat(logo): update to new AI Forte mark"
  ```

---

## Phase 7: Update brand system documentation

### Task 7: Update brand-system.md with new icon rules

**Files:**
- Modify: `resources/brand-system.md`

- [ ] **Step 1: Replace the "Logo System" section**

  Open `resources/brand-system.md`. Find the `## Logo System` section. Replace the "Icon construction rules" subsection with rules specific to the chosen concept:

  For example, if Concept 1 (Musical F) wins:
  ```markdown
  ### Icon construction rules — Musical F
  - Italic lowercase letterform "f" as the primary mark
  - Bold weight (~800), asymmetric stroke: heavier bottom stem, lighter top crossbar
  - Foreground color: burnt sienna #C65D2E on cream background
  - Letterform stands alone as the icon (no surrounding shape, no container)
  - Minimum size: 16px (below this, letterform loses legibility)
  - Clear space: minimum 0.5× letterform height on all sides
  - Never: distort, rotate, add effects, recolor outside brand system, pair with non-brand typography
  ```

- [ ] **Step 2: Update the "Implementation Status" table**

  Mark the logo files as ✅ Locked and update paths:
  ```markdown
  | Asset | Status |
  |-------|--------|
  | `resources/logo/ai-forte-logo-horizontal.svg` | ✅ Locked |
  | `resources/logo/ai-forte-logo-vertical.svg` | ✅ Locked |
  | `resources/logo/ai-forte-logo-icon.svg` | ✅ Locked |
  | `resources/logo/ai-forte-logo-wordmark.svg` | ✅ Locked |
  | `resources/logo/ai-forte-logo-reversed.svg` | ✅ Locked |
  ```

- [ ] **Step 3: Commit**

  ```bash
  git add resources/brand-system.md
  git commit -m "docs(brand): lock new logo system in brand-system.md"
  ```

---

## Phase 8: Update CHANGELOG

### Task 8: Update project changelog

**Files:**
- Modify: `CHANGELOG.md`

- [ ] **Step 1: Add entry**

  At the top of `CHANGELOG.md`, add:

  ```markdown
  ## [DATE] — Logo Redesign (Icon Revisit)

  ### Decision
  - Rejected the previous orchestration-network icon as generic AI slop
  - Explored five concept directions grounded in the brand name "Forte":
    Musical F, Crescendo, Pillar, Monogram AF, Conductor Arc
  - **Locked Concept {W}** after side-by-side review

  ### Added
  - `resources/logo/concept-brief.md` — brand name symbolic exploration
  - `resources/logo/concepts/` — all 5 explored directions with preview.html
  - `resources/logo/ai-forte-logo-{horizontal,vertical,icon,wordmark,reversed}.svg`
    — final 5-layout system

  ### Removed
  - `resources/logo/ai-forte-logo.png` (old AI-generated network icon)
  - `resources/logo/ai-forte-icon.png` (old AI-generated network icon)

  ### Regenerated (using new mark)
  - LinkedIn banner
  - OG image
  - Social post template
  - Summit announcement
  - Digital business card cover
  - One-pager header

  ### Process
  - Used the `svg-logo-designer` skill from `rknall/claude-skills` for SVG generation
  - Side-by-side preview HTML let comparison happen at real sizes (96/48/16px)
    and on both cream and dark backgrounds
  - Brand system documentation updated in `brand-system.md`
  ```

- [ ] **Step 2: Commit and push**

  ```bash
  git add CHANGELOG.md
  git commit -m "docs: log logo redesign in CHANGELOG"
  git push origin main
  ```

---

## Self-Review

### Spec coverage
- ✅ "Come up with something better" → Phase 1 (concept brief) + Phase 2 (5 directions)
- ✅ "Use skill finder to get the right skill" → svg-logo-designer installed, invoked in Phase 2 + 5
- ✅ "Only create a plan" → no execution steps run, plan saved

### Decisions required before execution
- **User decision** at end of Phase 3: pick winning concept (or request new directions)
- **Optional user decision** in Phase 4: refinements or merges

### Known gotchas
- SVG logo designer skill may produce multiple "concept" outputs per invocation — may need to pick the best variation per concept direction
- Concept 5 (Conductor Arc) may render poorly at 16px since gestural brushstrokes don't always hold up at favicon size — be prepared to drop it or regenerate
- `svg-logo-designer` skill activates on next Claude Code session (skills load at startup); until then, executing Phase 2 requires a fresh session

---

## Total time estimate

| Phase | Work | Estimate |
|------|------|----------|
| 1. Concept brief | Write brand name exploration | 20 min |
| 2. Generate 5 concepts | 5× svg-logo-designer invocations | 40 min (8 min each) |
| 3. Comparison preview | HTML + open in browser | 15 min |
| 4. User picks winner | (user time, not Claude time) | — |
| 5. Full lockup system | 1× svg-logo-designer invocation (5 files) | 15 min |
| 6. Regenerate downstream | 6× image generation via OpenRouter | 40 min |
| 7. Brand system docs | Update brand-system.md | 10 min |
| 8. CHANGELOG | Add entry, commit, push | 5 min |
| **Total** | | **~2.5 hours** |

---

## Execution handoff

Plan saved to `docs/plans/2026-04-14-logo-revisit.md`. Not ready to execute until user confirms. When ready:

1. **Start fresh Claude Code session** so the newly-installed `svg-logo-designer` skill is registered
2. Execute Phases 1-3 (concept brief + 5 directions + preview) in one session — no decisions needed, ~75 min
3. Pause at Phase 4 for user to pick a winner
4. Execute Phases 5-8 after winner chosen — ~70 min

Note: all file operations in this plan land in the parent repo (`github.com/akthechamp/adobe-summit-2026`) except the final step of Phase 6 which touches the separate `astro-site/` repo.
