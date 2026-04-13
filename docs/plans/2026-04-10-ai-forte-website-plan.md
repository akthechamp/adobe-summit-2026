# AI Forte Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development or superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Transform the existing `astro-site/` into a Summit-ready AI Forte marketing site that doubles as a credibility anchor for Adobe Summit 2026 conversations. Ship a live URL before April 17 that you can point to during every pitch.

**Architecture:** The site already exists as an Astro 5 + React 19 + Tailwind 4 + Framer Motion + GSAP project with a complete home page (Hero, TrustedBy, About, Services, HowItWorks, CaseStudies, Testimonials, ROI, FAQ, Contact, Footer). Work is **content + positioning + deploy** — not a rebuild.

**Current State (audit):**
- ✅ Full single-page site with 11 sections, animated hero, GSAP timelines
- ✅ Services, case studies, FAQ, testimonials all in typed data files (`src/data/*.ts`)
- ✅ Dependencies modern and clean (no cleanup needed)
- ⚠️ Positioning is generic "marketing automation agency" — NO Adobe ecosystem mentions
- ⚠️ Case studies are fictional (GrowthLoop, RelayHealth, CloseWise) — need re-labeling or replacement
- ⚠️ Hero copy "Your marketing on autopilot" — not AI Forte-unique
- ⚠️ Single page only — no `/services`, `/about`, `/adobe-summit` landing page
- ⚠️ Not deployed

**Tech Stack:** Astro 5.17, React 19, Tailwind 4, Framer Motion 12, GSAP 3, TypeScript

---

## Scope Decision

This is NOT a rebuild. You have ~15 hours of total site work across 7 days. Scope is:
1. **Reposition content** (services, hero, about) for Adobe ecosystem + AI orchestration
2. **Add a `/adobe-summit` landing page** that lives as a dedicated Summit touchpoint
3. **Replace/relabel fictional case studies** with honest "illustrative" framing or real agency projects
4. **Add trust signals** — Adobe certifications (after Summit), tech stack logos, Adobe partner badges
5. **Deploy to Vercel/Netlify** with a real domain
6. **Generate hero imagery** via Gemini 3 prompts already in the Summit plan

**Out of scope:** Blog, CMS, backend forms (use a static form service), multi-language, SEO deep-dive, analytics beyond GA4 basic.

---

## File Structure (Files to Touch)

### New files to create:
- `src/pages/adobe-summit.astro` — dedicated Summit landing page
- `src/components/astro/SummitBanner.astro` — top-of-site "Meet us at Adobe Summit" banner
- `src/components/astro/AdobeEcosystemSection.astro` — Adobe products/capabilities grid
- `src/data/adobe-capabilities.ts` — typed data for Adobe ecosystem services
- `public/og-image.png` — social share image (Gemini 3 generated)
- `public/ai-forte-logo.svg` — generated logo
- `public/favicon.svg` — favicon from logo
- `vercel.json` OR `netlify.toml` — deployment config

### Files to modify:
- `src/pages/index.astro` — add SummitBanner, AdobeEcosystemSection
- `src/data/services.ts` — rewrite all 6 services for Adobe + agent orchestration
- `src/data/case-studies.ts` — relabel as "Illustrative Scenarios" or replace with real work
- `src/data/faq.ts` — add Adobe-specific FAQs (update unseen, will read during execution)
- `src/data/testimonials.ts` — honest curation (remove if fake, keep if real)
- `src/components/astro/HeroSection.astro` — rewrite headline, subhead, stats
- `src/components/astro/AboutSection.astro` — add AI Forte founder story + Adobe credibility
- `src/components/astro/TrustedBy.astro` — Adobe tech stack logos
- `src/components/astro/Footer.astro` — add Summit 2026 link, contact, Adobe disclaimers
- `src/components/astro/Navbar.astro` — add "Adobe Summit 2026" nav link
- `src/layouts/BaseLayout.astro` — update meta tags, OG image, title template

---

## Task 1: Content Repositioning — Services Data (30 min)

**Goal:** Rewrite `src/data/services.ts` to speak fluently about Adobe + agent orchestration.

**File:** `src/data/services.ts` (modify)

- [ ] **Step 1: Open the file and review current structure**

  Current services (generic): Marketing Automation, AI Agents, CRM Intelligence, Operations AI, Analytics, Integration Platform. Interface has `id`, `title`, `description`, `icon`, `features[]`, `category`.

- [ ] **Step 2: Replace with Adobe-aligned services**

  Replace the entire `services` array with:

  ```typescript
  export const services: Service[] = [
    {
      id: 'agent-orchestration',
      title: 'AI Agent Orchestration',
      description: 'We design and ship coordinated multi-agent systems on Adobe Agent Orchestrator and custom stacks. Not one-off chatbots — production agent ecosystems that drive measurable ROI.',
      icon: 'Network',
      features: ['Multi-Agent System Design', 'Adobe Agent Orchestrator', 'Agent Governance & Guardrails', 'Human-in-the-Loop Workflows'],
      category: 'agents',
    },
    {
      id: 'adobe-commerce',
      title: 'Adobe Commerce Development',
      description: 'Enterprise storefronts on Adobe Commerce (Magento). Migrations, B2B commerce, custom modules, and Edge Delivery Services for storefront performance that scores 100 on Lighthouse.',
      icon: 'ShoppingBag',
      features: ['Commerce Cloud Service Migration', 'B2B Commerce (quotes, company accounts)', 'Edge Delivery Services', 'Custom Extensions & Integrations'],
      category: 'commerce',
    },
    {
      id: 'marketo-automation',
      title: 'Marketo Engage & Marketing Automation',
      description: 'Marketo implementation, optimization, and HubSpot↔Marketo migrations. We bridge enterprise Marketo with the Adobe ecosystem — Journey Optimizer, Real-Time CDP, and Sales Qualifier agents.',
      icon: 'Megaphone',
      features: ['Marketo Implementation', 'HubSpot ↔ Marketo Migration', 'Journey Optimizer B2B', 'Lead Scoring & Revenue Cycle Modeler'],
      category: 'marketing',
    },
    {
      id: 'aem-experiences',
      title: 'Adobe Experience Manager (AEM)',
      description: 'AEM Sites, Edge Delivery Services, and headless content architectures. Our frontend team ships AEM-powered experiences with React, Next.js, and standard HTML/CSS/JS.',
      icon: 'Layout',
      features: ['AEM Sites Development', 'Edge Delivery Services', 'Headless AEM + React/Next.js', 'Content Fragment Models'],
      category: 'content',
    },
    {
      id: 'crm-intelligence',
      title: 'CRM Intelligence & Integration',
      description: 'Connect Marketo, Salesforce, HubSpot, and Adobe Real-Time CDP with custom pipelines. Add predictive scoring, next-best-action, and unified customer profiles on top.',
      icon: 'Users',
      features: ['Real-Time CDP Integration', 'Salesforce / HubSpot Sync', 'Predictive Lead Scoring', 'Unified Customer Profiles'],
      category: 'crm',
    },
    {
      id: 'custom-development',
      title: 'Custom Web & Mobile Development',
      description: '20-person team shipping React, Next.js, and mobile apps. We handle the stuff Adobe products can\'t — custom portals, proprietary workflows, and full-stack product builds.',
      icon: 'Code',
      features: ['React / Next.js Applications', 'Mobile Apps (iOS / Android / PWA)', 'API & Backend Development', 'DevOps & Deployment'],
      category: 'development',
    },
  ];
  ```

  Also update the `category` union type to: `'agents' | 'commerce' | 'marketing' | 'content' | 'crm' | 'development'`

- [ ] **Step 3: Verify icons exist in lucide-react**

  Check: Network, ShoppingBag, Megaphone, Layout, Users, Code. All are valid lucide-react icons.

- [ ] **Step 4: Check consumers don't break**

  Search for uses of old service IDs or categories in components. Likely only `ServicesSection.astro` and `IndustryTabs.tsx` reference them. Update category filters if any.

- [ ] **Step 5: Visual check**

  Run `npm run dev`, load the home page, verify ServicesSection renders 6 new services. Check mobile + desktop.

- [ ] **Step 6: Commit**

  ```bash
  git add src/data/services.ts
  git commit -m "content: reposition services for Adobe ecosystem + agent orchestration"
  ```

---

## Task 2: Hero Rewrite (25 min)

**Goal:** Replace generic "marketing on autopilot" with AI Forte's sharp positioning.

**File:** `src/components/astro/HeroSection.astro` (modify)

- [ ] **Step 1: Rewrite hero badge, headline, subheadline, CTAs, stats**

  Find the content block (lines ~13-55) and replace with:

  ```astro
  <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-medium bg-brand-50 text-brand-400 border border-brand-200/30 mb-5">
    <span class="w-1.5 h-1.5 rounded-full bg-accent-500 animate-pulse"></span>
    Meet us at Adobe Summit 2026 • April 19-22 • Vegas
  </span>

  <h1 class="text-4xl sm:text-5xl lg:text-[3.25rem] font-bold text-text-heading leading-[1.08] tracking-tight mb-5">
    AI agents,
    <span class="gradient-text">orchestrated</span>.
    Built on Adobe.
  </h1>

  <p class="text-base text-text-muted leading-relaxed mb-7 max-w-md">
    We design and ship multi-agent systems on Adobe Experience Cloud. Commerce, Marketo, AEM, Journey Optimizer — coordinated by agents that actually drive business outcomes.
  </p>

  <div class="flex flex-wrap gap-3 mb-8">
    <a href="/adobe-summit" class="inline-flex items-center gap-2 px-6 py-3 rounded-xl text-sm font-medium bg-brand-600 text-white hover:bg-brand-500 shadow-lg shadow-brand-600/30 hover:shadow-brand-500/40 transition-all">
      Meet us at Summit
      <svg width="14" height="14" viewBox="0 0 16 16" fill="none"><path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
    </a>
    <a href="#services" class="inline-flex items-center gap-2 px-6 py-3 rounded-xl text-sm font-medium glass text-brand-400 hover:text-brand-300 transition-all">
      See What We Do
    </a>
  </div>

  <!-- Stats row -->
  <div class="flex gap-6">
    <div>
      <div class="text-2xl font-bold text-text-heading">20+</div>
      <p class="text-xs text-text-muted mt-0.5">Devs & Designers</p>
    </div>
    <div class="w-px bg-border-default"></div>
    <div>
      <div class="text-2xl font-bold text-text-heading">6</div>
      <p class="text-xs text-text-muted mt-0.5">Adobe Products</p>
    </div>
    <div class="w-px bg-border-default"></div>
    <div>
      <div class="text-2xl font-bold text-text-heading">Since 2016</div>
      <p class="text-xs text-text-muted mt-0.5">Magento / Adobe Commerce</p>
    </div>
  </div>
  ```

  (Replace "Since 2016" with your actual agency start date. Same for `20+` if team size is different.)

- [ ] **Step 2: Visual check + commit**

  ```bash
  git add src/components/astro/HeroSection.astro
  git commit -m "content: rewrite hero for AI Forte + Adobe positioning"
  ```

---

## Task 3: Case Studies — Honest Relabeling (20 min)

**Goal:** The current case studies (GrowthLoop, RelayHealth, CloseWise) are fabricated. Using fake client names at Summit is a huge risk — Adobe attendees will Google and blow your cover.

**Decision:** Relabel as "Illustrative Scenarios" OR replace with real sanitized agency work.

**File:** `src/data/case-studies.ts` (modify)

- [ ] **Step 1: Pick your approach**

  **Option A (Recommended if you have real Magento/CRM work):** Replace with 2-3 real projects, anonymized as "Mid-Market Home Goods Retailer" style. Keep real metrics.

  **Option B (If no time for real work):** Relabel all three as "Illustrative Scenarios" with a clear disclaimer. Honest and usable.

- [ ] **Step 2 (Option B path): Update interface and content**

  Add a new field to the interface:
  ```typescript
  export interface CaseStudy {
    id: string;
    client: string;
    industry: string;
    title: string;
    summary: string;
    metrics: { value: string; label: string }[];
    tags: string[];
    imagePrompt: string;
    type: 'real' | 'illustrative'; // NEW
  }
  ```

  For each of the 3 existing entries, set `type: 'illustrative'` and change the client names to generic placeholders:
  - `GrowthLoop` → `Mid-Market DTC Retailer`
  - `RelayHealth` → `B2B Healthcare SaaS`
  - `CloseWise` → `Enterprise B2B SaaS`

- [ ] **Step 3: Update CaseStudiesSection.astro**

  Add a section label above the grid: "Illustrative Scenarios — How we approach Adobe + agent orchestration engagements. Contact us for real client references."

- [ ] **Step 4 (Option A path): Replace with real work**

  Write 2-3 real case studies from your agency's portfolio. Anonymize clients if required by NDA. Keep real metrics. Same interface, `type: 'real'`.

- [ ] **Step 5: Commit**

  ```bash
  git add src/data/case-studies.ts src/components/astro/CaseStudiesSection.astro
  git commit -m "content: honest case study labeling (illustrative vs real)"
  ```

---

## Task 4: Adobe Ecosystem Section (45 min)

**Goal:** Add a new visual section showing exactly which Adobe products AI Forte works with. This is the section Summit attendees will screenshot.

**Files:**
- Create: `src/data/adobe-capabilities.ts`
- Create: `src/components/astro/AdobeEcosystemSection.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Create data file**

  `src/data/adobe-capabilities.ts`:
  ```typescript
  export interface AdobeCapability {
    id: string;
    product: string;
    role: string;
    capability: string;
    icon: string;
  }

  export const adobeCapabilities: AdobeCapability[] = [
    {
      id: 'commerce',
      product: 'Adobe Commerce',
      role: 'Storefront + B2B',
      capability: 'Storefront development, B2B commerce, migrations, Edge Delivery Services, agentic shopping experiences',
      icon: 'ShoppingCart',
    },
    {
      id: 'marketo',
      product: 'Marketo Engage',
      role: 'Marketing Automation',
      capability: 'Implementation, optimization, HubSpot ↔ Marketo migration, lead scoring, engagement programs',
      icon: 'Zap',
    },
    {
      id: 'aem',
      product: 'AEM Sites + Assets',
      role: 'Content & Experience',
      capability: 'Sites development, Edge Delivery Services, headless AEM, DAM workflows, Content AI',
      icon: 'Layout',
    },
    {
      id: 'ajo',
      product: 'Journey Optimizer',
      role: 'Cross-Channel Orchestration',
      capability: 'Journey design, B2B Edition, cross-channel campaigns, AJO agents',
      icon: 'GitBranch',
    },
    {
      id: 'rtcdp',
      product: 'Real-Time CDP',
      role: 'Customer Data',
      capability: 'Unified profiles, segment activation, data integration, privacy governance',
      icon: 'Database',
    },
    {
      id: 'orchestrator',
      product: 'Agent Orchestrator',
      role: 'AI Agent Platform',
      capability: 'Multi-agent orchestration, Brand Concierge, AI Assistant integration, custom agent development',
      icon: 'Network',
    },
  ];
  ```

- [ ] **Step 2: Create the section component**

  `src/components/astro/AdobeEcosystemSection.astro`:
  ```astro
  ---
  import { adobeCapabilities } from '../../data/adobe-capabilities';
  ---

  <section id="adobe-ecosystem" class="py-20 bg-surface-secondary">
    <div class="max-w-7xl mx-auto px-6">
      <div class="text-center max-w-2xl mx-auto mb-14">
        <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-medium bg-brand-50 text-brand-400 border border-brand-200/30 mb-4">
          Adobe Experience Cloud
        </span>
        <h2 class="text-3xl sm:text-4xl font-bold text-text-heading mb-4 tracking-tight">
          Six Adobe products. One orchestrated stack.
        </h2>
        <p class="text-base text-text-muted">
          We build across the Adobe ecosystem — from Commerce storefronts to Marketo campaigns to Agent Orchestrator multi-agent systems. Deep platform expertise, not product-of-the-week consulting.
        </p>
      </div>

      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-5">
        {adobeCapabilities.map((cap) => (
          <div class="glass rounded-2xl p-6 hover:shadow-glass-violet transition-all">
            <div class="flex items-center gap-3 mb-3">
              <div class="w-10 h-10 rounded-xl bg-brand-50 flex items-center justify-center">
                <span class="text-brand-400 text-lg">●</span>
              </div>
              <div>
                <h3 class="text-base font-semibold text-text-heading leading-tight">{cap.product}</h3>
                <p class="text-xs text-text-light">{cap.role}</p>
              </div>
            </div>
            <p class="text-sm text-text-muted leading-relaxed">{cap.capability}</p>
          </div>
        ))}
      </div>
    </div>
  </section>
  ```

- [ ] **Step 3: Import and mount in `src/pages/index.astro`**

  Add import line and mount after ServicesSection:
  ```astro
  import AdobeEcosystemSection from '../components/astro/AdobeEcosystemSection.astro';
  ```
  ```astro
  <ServicesSection />
  <AdobeEcosystemSection />
  <HowItWorksSection />
  ```

- [ ] **Step 4: Visual check + commit**

  ```bash
  git add src/data/adobe-capabilities.ts src/components/astro/AdobeEcosystemSection.astro src/pages/index.astro
  git commit -m "feat: add Adobe Experience Cloud capabilities section"
  ```

---

## Task 5: Summit Landing Page (60 min)

**Goal:** A dedicated `/adobe-summit` page you can link to from LinkedIn, business cards, and email signatures. Single-purpose CTA: book a meeting at Summit.

**Files:**
- Create: `src/pages/adobe-summit.astro`

- [ ] **Step 1: Create the page**

  `src/pages/adobe-summit.astro`:
  ```astro
  ---
  import BaseLayout from '../layouts/BaseLayout.astro';
  import Navbar from '../components/astro/Navbar.astro';
  import Footer from '../components/astro/Footer.astro';
  ---

  <BaseLayout title="Meet AI Forte at Adobe Summit 2026 — April 19-22, Las Vegas">
    <Navbar />
    <main>
      <!-- Hero -->
      <section class="relative min-h-[80vh] flex items-center pt-24 pb-16 overflow-hidden bg-gradient-to-b from-surface-primary to-surface-secondary">
        <div class="max-w-5xl mx-auto px-6 text-center">
          <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-medium bg-accent-500/10 text-accent-500 border border-accent-500/20 mb-6">
            <span class="w-1.5 h-1.5 rounded-full bg-accent-500 animate-pulse"></span>
            April 19-22, 2026 • The Venetian, Las Vegas
          </span>

          <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold text-text-heading leading-[1.08] tracking-tight mb-6">
            Let's talk <span class="gradient-text">agent orchestration</span><br/>at Adobe Summit.
          </h1>

          <p class="text-lg text-text-muted leading-relaxed mb-10 max-w-2xl mx-auto">
            AI Forte is at Summit 2026. If you're working on AI agents, Commerce, Marketo, or Experience Manager — let's grab 20 minutes. No deck, just a real conversation about where you're stuck.
          </p>

          <div class="flex flex-wrap gap-4 justify-center mb-12">
            <a href="YOUR_CALENDLY_URL" target="_blank" class="inline-flex items-center gap-2 px-8 py-4 rounded-xl text-base font-medium bg-brand-600 text-white hover:bg-brand-500 shadow-lg shadow-brand-600/30 transition-all">
              Book a 20-min Meeting
              <svg width="16" height="16" viewBox="0 0 16 16" fill="none"><path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
            </a>
            <a href="#what-well-discuss" class="inline-flex items-center gap-2 px-8 py-4 rounded-xl text-base font-medium glass text-brand-400 hover:text-brand-300 transition-all">
              What We'll Discuss
            </a>
          </div>
        </div>
      </section>

      <!-- What We'll Discuss -->
      <section id="what-well-discuss" class="py-20 bg-surface-primary">
        <div class="max-w-5xl mx-auto px-6">
          <h2 class="text-3xl sm:text-4xl font-bold text-text-heading mb-12 text-center tracking-tight">Good conversations for us</h2>
          <div class="grid md:grid-cols-2 gap-6">
            <div class="glass rounded-2xl p-6">
              <h3 class="text-lg font-semibold text-text-heading mb-2">You're building AI agents</h3>
              <p class="text-sm text-text-muted">You've piloted a chatbot or a content generator. Now you need orchestration — agents that coordinate across Commerce, Marketo, and AEM. We've done this.</p>
            </div>
            <div class="glass rounded-2xl p-6">
              <h3 class="text-lg font-semibold text-text-heading mb-2">You're migrating Magento / Commerce</h3>
              <p class="text-sm text-text-muted">Moving to Adobe Commerce as a Cloud Service? We've been building on Magento since before the Adobe acquisition.</p>
            </div>
            <div class="glass rounded-2xl p-6">
              <h3 class="text-lg font-semibold text-text-heading mb-2">You're evaluating HubSpot → Marketo</h3>
              <p class="text-sm text-text-muted">We know both sides. We've done migrations and we can tell you honestly when Marketo is the right call and when it isn't.</p>
            </div>
            <div class="glass rounded-2xl p-6">
              <h3 class="text-lg font-semibold text-text-heading mb-2">You need a technical partner</h3>
              <p class="text-sm text-text-muted">20-person build team. We ship code, not slide decks. Frontend, backend, mobile, integrations.</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Schedule snippet -->
      <section class="py-20 bg-surface-secondary">
        <div class="max-w-3xl mx-auto px-6 text-center">
          <h2 class="text-2xl sm:text-3xl font-bold text-text-heading mb-4 tracking-tight">Where we'll be</h2>
          <p class="text-base text-text-muted mb-8">Sessions we're attending — feel free to catch us before or after</p>
          <div class="glass rounded-2xl p-6 text-left space-y-3 text-sm">
            <div class="flex justify-between py-2 border-b border-border-default">
              <span class="text-text-heading font-medium">Mon Apr 20 • Welcome Reception</span>
              <span class="text-text-muted">6:00-7:30 PM</span>
            </div>
            <div class="flex justify-between py-2 border-b border-border-default">
              <span class="text-text-heading font-medium">Tue Apr 21 • Marketo Roadmap [S202]</span>
              <span class="text-text-muted">11:30 AM</span>
            </div>
            <div class="flex justify-between py-2 border-b border-border-default">
              <span class="text-text-heading font-medium">Tue Apr 21 • Commerce Roadmap [S301]</span>
              <span class="text-text-muted">1:30 PM</span>
            </div>
            <div class="flex justify-between py-2 border-b border-border-default">
              <span class="text-text-heading font-medium">Tue Apr 21 • Summit Bash</span>
              <span class="text-text-muted">7:30-11:00 PM</span>
            </div>
            <div class="flex justify-between py-2">
              <span class="text-text-heading font-medium">Wed Apr 22 • Agent Orchestrator Lab [L815]</span>
              <span class="text-text-muted">1:00 PM</span>
            </div>
          </div>
          <div class="mt-10">
            <a href="YOUR_CALENDLY_URL" target="_blank" class="inline-flex items-center gap-2 px-8 py-4 rounded-xl text-base font-medium bg-brand-600 text-white hover:bg-brand-500 shadow-lg shadow-brand-600/30 transition-all">
              Book a meeting at Summit
            </a>
          </div>
        </div>
      </section>
    </main>
    <Footer />
  </BaseLayout>
  ```

- [ ] **Step 2: Replace `YOUR_CALENDLY_URL` with real link**

  Create Calendly if you don't have one, paste URL in both places.

- [ ] **Step 3: Visual check**

  Navigate to `http://localhost:4321/adobe-summit`, verify layout, mobile responsive.

- [ ] **Step 4: Commit**

  ```bash
  git add src/pages/adobe-summit.astro
  git commit -m "feat: add dedicated Adobe Summit 2026 landing page"
  ```

---

## Task 6: Summit Banner & Navbar Update (20 min)

**Goal:** Site-wide banner announcing Summit presence + nav link.

**Files:**
- Create: `src/components/astro/SummitBanner.astro`
- Modify: `src/components/astro/Navbar.astro`
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Create banner component**

  `src/components/astro/SummitBanner.astro`:
  ```astro
  ---
  ---
  <div class="relative bg-brand-600 text-white text-center py-2.5 px-4 text-xs sm:text-sm z-50">
    <span class="inline-flex items-center gap-2 flex-wrap justify-center">
      <span class="w-1.5 h-1.5 rounded-full bg-accent-400 animate-pulse"></span>
      <strong>We're at Adobe Summit 2026</strong>
      <span class="hidden sm:inline">April 19-22 • Las Vegas</span>
      <a href="/adobe-summit" class="underline underline-offset-2 hover:text-accent-300 font-medium ml-1">Book a meeting →</a>
    </span>
  </div>
  ```

- [ ] **Step 2: Mount banner at top of all pages**

  In `src/layouts/BaseLayout.astro`, import and render above `<slot />`:
  ```astro
  import SummitBanner from '../components/astro/SummitBanner.astro';
  ```
  ```astro
  <body>
    <SummitBanner />
    <slot />
  </body>
  ```

- [ ] **Step 3: Add nav link**

  In `src/components/astro/Navbar.astro`, add a link to `/adobe-summit` in the nav items list.

- [ ] **Step 4: Commit**

  ```bash
  git add src/components/astro/SummitBanner.astro src/components/astro/Navbar.astro src/layouts/BaseLayout.astro
  git commit -m "feat: add site-wide Summit banner and nav link"
  ```

---

## Task 7: Logo, Favicon, OG Image (30 min)

**Goal:** Brand assets generated via Gemini 3.

- [ ] **Step 1: Generate logo using Gemini 3**

  Use Prompt #1 from `docs/plans/2026-04-10-revised-summit-preparation.md` Gemini section. Generate 4 variations, pick the best.

  Save as `public/ai-forte-logo.svg` (if SVG output) or `public/ai-forte-logo.png`.

- [ ] **Step 2: Generate favicon**

  Use Prompt #2 (icon-only mark). Save as `public/favicon.svg` and also generate a 512x512 PNG as fallback.

- [ ] **Step 3: Generate OG image**

  Use a variant of Prompt #3 (LinkedIn banner) at 1200x630 px for Open Graph. Save as `public/og-image.png`.

- [ ] **Step 4: Update BaseLayout.astro meta tags**

  ```html
  <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
  <meta property="og:image" content="/og-image.png" />
  <meta property="og:title" content="AI Forte — AI Agent Orchestration on Adobe Experience Cloud" />
  <meta property="og:description" content="We design and ship multi-agent systems on Adobe. Commerce, Marketo, AEM, Journey Optimizer — orchestrated for business outcomes." />
  <meta name="twitter:card" content="summary_large_image" />
  ```

- [ ] **Step 5: Update logo in Navbar and Footer**

  Reference `/ai-forte-logo.svg` instead of placeholder text.

- [ ] **Step 6: Commit**

  ```bash
  git add public/ src/layouts/BaseLayout.astro src/components/astro/Navbar.astro src/components/astro/Footer.astro
  git commit -m "feat: add AI Forte brand assets (logo, favicon, OG image)"
  ```

---

## Task 8: TrustedBy / Tech Stack Section (20 min)

**Goal:** Replace generic "trusted by" logos with Adobe ecosystem tech stack.

**File:** `src/components/astro/TrustedBy.astro` (modify)

- [ ] **Step 1: Repurpose the section**

  Rewrite as "Built on technologies we're certified in" or "Our stack" showing:
  - Adobe Commerce
  - Adobe Marketo Engage
  - Adobe Experience Manager
  - Adobe Journey Optimizer
  - HubSpot
  - Salesforce
  - React / Next.js
  - Shopify

  Use simple wordmarks or SVG logos. No fake client logos — use TECH stack logos, which is honest and still builds trust.

- [ ] **Step 2: Commit**

  ```bash
  git add src/components/astro/TrustedBy.astro
  git commit -m "content: replace trusted-by with honest tech stack"
  ```

---

## Task 9: Remove / Fix Fake Testimonials (15 min)

**File:** `src/data/testimonials.ts` (modify)

- [ ] **Step 1: Audit current testimonials**

  Read the file. If testimonials are fabricated (likely, given the fake case studies), either:
  - Delete the section from the homepage, OR
  - Replace with real testimonials from real past clients (even if just 1-2)

  **Honest empty is better than fake full.** Summit buyers WILL Google your testimonials.

- [ ] **Step 2: If deleting: remove from index.astro**

  ```astro
  <!-- Remove this line: -->
  <TestimonialsSection />
  ```

- [ ] **Step 3: Commit**

---

## Task 10: Deploy (30 min)

**Goal:** Live URL you can link from LinkedIn, business cards, email signature.

- [ ] **Step 1: Pick a host**

  Vercel recommended (fastest for Astro, free tier, auto-deploys from Git, custom domain free).

- [ ] **Step 2: Push to GitHub**

  ```bash
  cd "/Users/ashishkumar/Projects/Ashish Kumar/Adobe Summit 2026/astro-site"
  gh repo create ai-forte-website --private --source=. --push
  ```

- [ ] **Step 3: Deploy to Vercel**

  - Go to [vercel.com/new](https://vercel.com/new)
  - Import the GitHub repo
  - Framework: Astro (auto-detected)
  - Click Deploy
  - Get `https://ai-forte-website.vercel.app` URL

- [ ] **Step 4: (Optional) Custom domain**

  If you own `aiforte.ai` / `aiforte.io` / `aiforte.com` or similar, point DNS to Vercel. Otherwise, ship with the vercel.app URL — totally fine for Summit.

- [ ] **Step 5: Smoke test**

  Visit production URL, verify:
  - Home page loads, animations work
  - `/adobe-summit` loads
  - Calendly link works
  - OG image shows in a LinkedIn post preview (use LinkedIn Post Inspector)
  - Mobile responsive

- [ ] **Step 6: Add URL everywhere**

  - LinkedIn profile (website field)
  - LinkedIn About CTA
  - Digital business card (Blinq/Popl)
  - One-pager PDF footer
  - Email signature
  - Gmail draft follow-up templates

---

## Task 11: Contact Form Wiring (30 min — OPTIONAL)

**Goal:** Make the contact form actually submit.

**File:** `src/components/react/ContactForm.tsx` (modify)

- [ ] **Step 1: Pick a form service**

  **Recommended: [Formspree](https://formspree.io/)** — free tier, no backend needed, email on submit. Takes 5 minutes.

  Alternative: Netlify Forms, Vercel's built-in, Basin, Web3Forms.

- [ ] **Step 2: Wire up submission**

  Point the form's `action` or `onSubmit` to the Formspree endpoint. Test a submission. Verify email arrives.

- [ ] **Step 3: Commit and redeploy**

  Vercel auto-deploys on push.

---

## Total Time Estimate

| Task | Time |
|------|------|
| 1. Services rewrite | 30 min |
| 2. Hero rewrite | 25 min |
| 3. Case studies relabel | 20 min |
| 4. Adobe Ecosystem section | 45 min |
| 5. Summit landing page | 60 min |
| 6. Summit banner + nav | 20 min |
| 7. Logo/favicon/OG | 30 min |
| 8. TrustedBy fix | 20 min |
| 9. Testimonials audit | 15 min |
| 10. Deploy | 30 min |
| 11. Contact form (optional) | 30 min |
| **TOTAL** | **~5.5 hours** |

Spread across Apr 11-16 as daily collateral work (see revised Summit plan).

---

## Daily Execution Mapping

| Day | Site Tasks |
|-----|-----------|
| **Apr 11 (Sat)** | Task 1 (Services rewrite) + Task 2 (Hero rewrite) — 55 min |
| **Apr 12 (Sun)** | Task 3 (Case studies) + Task 4 (Adobe Ecosystem section) — 65 min |
| **Apr 13 (Mon)** | Task 5 (Summit landing page) — 60 min |
| **Apr 14 (Tue)** | Task 6 (Banner + nav) + Task 8 (TrustedBy) + Task 9 (Testimonials) — 55 min |
| **Apr 15 (Wed)** | Task 7 (Logo/favicon/OG via Gemini 3) — 30 min |
| **Apr 16 (Thu)** | Task 10 (Deploy) + Task 11 (Contact form) + final polish — 60 min |
| **Apr 17 (Fri)** | Smoke test, share URL on LinkedIn, pack, depart |

---

## Self-Review Checklist

Before Task 10 (Deploy), verify:

- [ ] All "GrowthLoop / RelayHealth / CloseWise" strings removed or relabeled as illustrative
- [ ] No "lorem ipsum" or placeholder text anywhere
- [ ] Calendly URL filled in on both `/adobe-summit` buttons
- [ ] LinkedIn URL in footer is correct
- [ ] Mobile responsive on all pages (resize browser)
- [ ] All links work (no 404s)
- [ ] Meta description and OG image set in BaseLayout
- [ ] Favicon shows in browser tab
- [ ] Hero animations still work after content changes
