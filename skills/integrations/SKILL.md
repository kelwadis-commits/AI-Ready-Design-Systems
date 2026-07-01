---
name: integrations
description: >
  This skill should be used when the user asks about connecting ARDS outputs to Lovable, Figma,
  Tokens Studio, Tailwind CSS, v0, Cursor, Storybook, Manus, Trickle, n8n, Ideogram, Canva, Tally, Stripe,
  or any builder tool; what format to export tokens in for a specific tool; how to hand off a
  design system to a builder tool; whether ARDS supports a specific integration; what integrations
  are planned vs available now; how to set up the Lovable workflow end-to-end; how to use Refero
  alongside the Figma MCP; or how to wire up the full business factory stack (design → assets → payments → launch).
---

# Integration Partners — AI-Ready Design Systems

## The Integration Philosophy

ARDS is the upstream intelligence layer. It generates structured artifacts — tokens, specs, copy, audit reports — that downstream tools consume. Every integration follows that pattern: **ARDS produces → the tool receives.**

A well-integrated ARDS session produces zero re-work. The output goes directly into the next tool without transformation.

---

---

## Business Factory Architecture

The thread insight that shapes this skill: instead of ARDS connecting to 20 tools separately, the recommended architecture is:

```
Claude + ARDS
      ↓
  n8n (MCP)          ← one integration, 1000+ app reach
      ↓
────────────────────────────
Lovable    → app / site build
Ideogram   → brand image generation
Canva      → marketing asset creation
Tally      → forms, waitlists, lead capture
Stripe     → products, subscriptions, payment links
Google Drive / Sheets / Airtable / Slack / Notion / ...
────────────────────────────
```

**ARDS is the brain. n8n is the hands.**

This architecture makes ARDS competitive with closed platforms like Vibiz — the difference being that ARDS + Claude + n8n is fully owned, customizable infrastructure rather than a locked SaaS. The full workflow:

```
User drops URL or idea
  → ARDS system-setup: extracts brand, generates token system + style guide
  → ARDS asset-generation: generates screen designs + component specs
  → ARDS copy-generation: generates UX + marketing copy
  → n8n triggers:
      Lovable:  builds the live product / landing page
      Ideogram: generates brand imagery + ad creatives
      Canva:    creates social posts + marketing materials
      Tally:    creates waitlist / lead capture form
      Stripe:   creates product + payment link
  → Business live
```

When a user asks to "go from idea to live", this is the architecture to invoke.

---

## Tier 1 — Core Integrations

### Figma ✦ Wired

**What it is:** The design tool where the visual system lives and where tokens become variables.

**What ARDS gives Figma:**
- A complete Figma variable spec (name, value, mode, scope, group) ready to paste or import
- Token diff: when a Figma file is connected via MCP, ARDS detects existing variables and flags conflicts before overwriting
- Audit results that reference specific Figma component names when a file is connected

**The handoff:**
```
ARDS system-setup → Figma variable spec → Import into Figma via Variables panel or Tokens Studio
```

**Setup:** Connect the Figma MCP with `FIGMA_API_TOKEN` in your environment. Provide a Figma file URL in any skill.

**Status:** Wired (Figma MCP in `.mcp.json`)

---

### Refero / styles.refero.design ✦ Figma Peer Integration

**What it is:** A dual-surface research tool — a Figma plugin for inserting real production screens as references, and a standalone MCP that gives AI agents access to 150,000+ real app screens, 6,000+ user flows, and 2,000+ DESIGN.md style profiles from the world's best-designed products.

**Why it belongs alongside the Figma MCP:**
Refero operates as a peer to the Figma MCP, not downstream of it. The Figma MCP reads *your* file. Refero reads *the world's files*. Together they give an agent both the design system context (Figma MCP) and real-world pattern benchmarks (Refero) before generating anything.

**What Refero gives ARDS:**
- Visual direction: search 2,000+ DESIGN.md style profiles to establish aesthetic direction before `system-setup` runs
- Pattern benchmarks: pull real screens from Stripe, Linear, Notion, Figma, and comparable products to inform `asset-generation` references
- In-Figma reference: insert matched production screens directly into a Figma file via the Figma plugin
- Flow reference: access 6,000+ real user flows to validate step count and structure against industry patterns

**The handoff:**
```
Refero DESIGN.md search → visual direction brief → ARDS system-setup
Refero screen search → reference selection → ARDS asset-generation Step 2
Figma plugin → insert reference screens directly into Figma file
```

**MCP setup:** Refero has its own MCP. Connect it alongside the Figma MCP. First call opens a browser sign-in; subsequent calls are automatic. Works with Claude Code, Cursor, Gemini CLI, Lovable, and any MCP-compatible agent.

**Figma plugin:** Install from Figma Community — search "Refero". Provides in-Figma search across 100,000+ production screens with one-click insert.

**URLs:** [refero.design](https://refero.design) · [styles.refero.design](https://styles.refero.design) · [refero.design/mcp](https://refero.design/mcp)

**Status:** Wired (peer MCP + Figma plugin)

---

### Lovable ✦ Planned (v0.3.0)

**What it is:** An AI-powered full-stack web app builder. You describe what you want, and Lovable generates a running React/Vite app with Supabase backend, deployed to a live URL.

**Why ARDS and Lovable belong together:**
Lovable builds. ARDS brands. Lovable's stack (React + Tailwind + shadcn/ui) is exactly what ARDS targets with its token architecture. The DTCG tokens ARDS generates map directly to a Tailwind theme config and a shadcn CSS variable file — near-zero-friction handoff.

**What ARDS gives Lovable:**
- A `tailwind.config.js` theme extension with brand colors, typography scale, and spacing
- A shadcn CSS variable block (`globals.css`) with light and dark mode values
- UX copy blocks ready to paste into Lovable prompts
- A brand brief summary formatted as a Lovable system prompt preamble

**The handoff:**
```
ARDS system-setup → tailwind.config.js + globals.css → paste into Lovable project
ARDS copy-generation → copy blocks → paste into Lovable prompts
```

**Status:** Planned for v0.3.0

---

### n8n ✦ Orchestration Layer (Tier 1)

**What it is:** An open-source workflow automation platform that connects Claude to 1,000+ apps through a single MCP integration. Unlike point-to-point integrations, n8n acts as a middleware layer — ARDS sends one structured instruction, n8n fans it out to Lovable, Ideogram, Canva, Stripe, Tally, and any other connected app simultaneously.

**Why it belongs at Tier 1:**
n8n changes the integration model entirely. Instead of ARDS needing individual MCPs for every tool, n8n becomes the single integration that unlocks the full business factory stack. One connection in `.mcp.json`; reach to 1,000+ destinations.

**What ARDS gives n8n:**
- Brand brief + token system → triggers Lovable project creation with brand context pre-loaded
- Component specs → triggers Ideogram image generation with style parameters
- Copy blocks → triggers Canva template population
- Product description + pricing → triggers Stripe product + payment link creation
- Waitlist copy → triggers Tally form creation and embed

**The handoff:**
```
ARDS system-setup output → n8n webhook → fan-out to Lovable + Ideogram + Canva + Tally + Stripe
ARDS asset-generation JSON → n8n → Lovable design spec import
ARDS copy-generation output → n8n → Canva template text injection
```

**Setup:** n8n MCP server connects Claude Desktop directly to your n8n instance (self-hosted or cloud). Workflows are pre-built per output type and triggered via webhook from ARDS.

**Architecture pattern:** `Claude → MCP → n8n → {target apps}` — never `Claude → 20 separate MCPs`.

**URL:** [n8n.io](https://n8n.io)

**Status:** Tier 1 (orchestration backbone for the full business factory stack)

---

### Tokens Studio for Figma ✦ Planned (v0.3.0)

**What it is:** A Figma plugin that manages design tokens as JSON and syncs them to GitHub.

**What ARDS gives Tokens Studio:**
ARDS outputs DTCG-format tokens. In v0.3.0, ARDS will output a Tokens Studio-compatible `.json` file directly.

**The handoff:**
```
ARDS token file (DTCG) → [v0.3.0 transform] → Tokens Studio JSON → import into Figma plugin → sync to GitHub
```

**Status:** Planned for v0.3.0

---

### Tailwind CSS ✦ Wired

**What it is:** The utility-first CSS framework underlying Lovable, v0, Skiper UI, Cult UI, and most modern React/shadcn stacks. ARDS already generates a Tailwind-compatible output as part of the Lovable handoff — this entry makes it a first-class target on its own, independent of any specific builder.

**Why it belongs as its own entry:**
The `tailwind.config.js` transform isn't unique to Lovable. Any Tailwind-based project — a hand-coded Next.js app, a v0 generation, a Skiper UI or Cult UI install — can consume the same theme extension and CSS variable block ARDS already produces. Documenting it separately means a user doesn't have to route through Lovable to get Tailwind output.

**What ARDS gives Tailwind:**
- A `tailwind.config.js` theme extension (colors, typography scale, spacing, radius) generated directly from the DTCG token file
- A CSS variable block (`:root` / `.dark`) for projects using Tailwind's CSS-variable-driven theming (v4-style or shadcn-style setups)
- Token names from `system-audit` mapped to their Tailwind utility class equivalents (e.g. `color.brand.primary` → `bg-brand-primary`)

**The handoff:**
```
ARDS token file (DTCG) → tailwind.config.js theme extension + CSS variables → drop into any Tailwind project
```

**Setup:** No separate connection needed — this is a direct transform of the existing ARDS token output, not a new MCP or API. Ask for Tailwind-config format explicitly when Lovable isn't the target.

**URL:** [tailwindcss.com](https://tailwindcss.com)

**Status:** Wired (transform of existing token output; builder-agnostic)

---

## Tier 2 — Builder & Agent Integrations

### Ideogram ✦ Brand Image Generation

**What it is:** An AI image generation API with a strong emphasis on typography, consistent style, and brand-directed outputs. Unlike general-purpose image generators, Ideogram handles text-in-image accurately — making it usable for ad creatives, social graphics, and product shots.

**What ARDS gives Ideogram:**
- Brand brief (tone, aesthetic, color palette, imagery style from `system-setup`) → becomes the style prompt seed
- Art direction notes from `asset-generation` Step 5 → become the image generation prompt
- Consistent style parameters maintained across a project's full creative suite

**The handoff:**
```
ARDS system-setup (aesthetic) + asset-generation (art direction note) → Ideogram API prompt → brand imagery
n8n workflow → auto-triggers Ideogram on project creation with ARDS style params
```

**Output types:** Landing page hero images, social post graphics, ad creatives, product lifestyle shots, brand illustrations.

**URL:** [ideogram.ai](https://ideogram.ai) · API available at `api.ideogram.ai`

**Status:** Tier 2 (direct API or via n8n)

---

### Canva ✦ Marketing Asset Creation

**What it is:** Design platform with an Apps SDK and Connect APIs that allow programmatic template population, design creation, and asset export. ARDS uses Canva for the marketing tier — social posts, ad templates, email headers — not for the product design system (that stays in Figma).

**What ARDS gives Canva:**
- Brand token values → Canva brand kit colors and fonts
- Copy blocks from `copy-generation` → injected into Canva template text layers
- Imagery direction → paired with Ideogram outputs for fully composed social assets

**The handoff:**
```
ARDS copy-generation → Canva Connect API → template text injection → export-ready social post
ARDS system-setup (brand colors + fonts) → Canva brand kit → applied to all templates automatically
n8n workflow → auto-creates Canva designs on ARDS project completion
```

**Boundary:** Canva is the **marketing tier** output tool. Product screens, component specs, and design system artifacts stay in Figma. Don't conflate the two.

**URL:** [canva.com/developers](https://www.canva.com/developers/)

**Status:** Tier 2 (via Canva Connect API or n8n)

---

### Tally ✦ Forms, Waitlists & Lead Capture

**What it is:** A no-code form builder with a clean API, webhook support, and native integrations with n8n, Zapier, and Make. Used for waitlist creation, lead capture, onboarding surveys, and contact forms.

**What ARDS gives Tally:**
- Waitlist copy from `copy-generation` → form headline, description, CTA, confirmation message
- Brand colors and fonts → applied via Tally's customization options
- Form fields derived from the user story persona (Step 0 in `asset-generation`)

**The handoff:**
```
ARDS copy-generation (waitlist copy) → Tally API → live form with embed code
n8n workflow → auto-creates Tally form on project launch, connects submissions to Airtable/Notion/email
```

**URL:** [tally.so](https://tally.so)

**Status:** Tier 2 (via Tally API or n8n)

---

### Stripe ✦ Monetization

**What it is:** The payment infrastructure layer. ARDS uses Stripe to go from product concept to live revenue — creating products, pricing, subscriptions, and payment links as part of a launch workflow.

**What ARDS gives Stripe:**
- Product name and description from the brand brief (Step 0 `system-setup`)
- Pricing model (subscription / one-time / freemium) inferred from the product brief
- Payment link that can be embedded in the Lovable-built landing page immediately

**The handoff:**
```
ARDS system-setup (product description + pricing signal) → Stripe API → product + payment link
n8n workflow → auto-creates Stripe product on project creation → embeds payment link in Lovable page
```

**Launch sequence:**
```
1. ARDS extracts brand + product from URL
2. Lovable builds the landing page
3. Tally creates the waitlist form
4. Stripe creates the payment link
5. n8n wires form submissions → CRM + email
6. Business is live
```

**URL:** [stripe.com/docs/api](https://stripe.com/docs/api)

**Status:** Tier 2 (direct Stripe API or via n8n)

---

### Manus ✦ Agent Orchestration Layer

**What it is:** An autonomous AI agent platform. Unlike a chatbot, Manus takes a high-level goal and executes it end-to-end — browsing, coding, researching, writing — without supervision. Each step is visible in its side panel.

**Why it belongs with ARDS:**
Manus can run a full ARDS workflow autonomously. Hand it a brand brief and a target URL and it can run `system-setup`, generate tokens, source templates, and produce output files — without the user managing each step. ARDS becomes the intelligence layer; Manus becomes the execution layer.

**The handoff:**
```
User provides brand brief → Manus runs ARDS system-setup + asset-generation → delivers token file + design spec
```

**URL:** [manus.im](https://manus.im)

**Status:** Ecosystem (use as agent runner for ARDS workflows)

---

### Skiper UI ✦ shadcn Code Connect Target

**What it is:** An extension of shadcn/ui providing uncommon components not found in the standard shadcn library. Installable via the shadcn registry.

**Why it belongs with ARDS:**
When the Figma MCP's `add_code_connect_map` is used to map Figma components to code, Skiper UI components are valid targets for shadcn-based projects. ARDS token files map directly to Skiper's Tailwind/shadcn architecture.

**The handoff:**
```
ARDS token file → shadcn CSS variables → Skiper UI component styling
Figma MCP Code Connect → map Figma components → Skiper UI component imports
```

**URL:** [skiper-ui.com/components](https://skiper-ui.com/components)

**Status:** Ecosystem (Code Connect target)

---

### Cult UI ✦ shadcn Code Connect Target + AI Agent Patterns

**What it is:** A shadcn/ui-compatible component library with 75+ animated components and (Pro tier) 100+ AI SDK agent UI patterns for OpenAI, Google Gemini, and Anthropic Claude.

**Why it belongs with ARDS:**
Two integration angles. First, as a Code Connect target — Cult UI's Figma-compatible shadcn architecture maps directly from the Figma MCP. Second, its AI SDK agent patterns are directly relevant when ARDS is generating screens for AI-native products.

**The handoff:**
```
ARDS token file → shadcn CSS variables → Cult UI component styling
Figma MCP Code Connect → map Figma components → Cult UI component imports
ARDS asset-generation (AI product flow) → Cult UI AI SDK patterns as component reference
```

**URL:** [cult-ui.com/docs](https://cult-ui.com/docs)

**Status:** Ecosystem (Code Connect target; AI SDK patterns reference)

---

### Trickle ✦ AI App Builder

**What it is:** An AI-powered no-code app builder with a Magic Canvas that transforms ideas into production-ready apps and websites. Includes a vibe coding prompt library.

**Why it belongs with ARDS:**
Trickle is a valid downstream target for ARDS outputs — especially when the user wants to build without code. ARDS token outputs and copy blocks can be formatted as Trickle prompt inputs. Its vibe coding prompt library also pairs with ARDS `asset-generation` when using prompt-based registries (VibeUI, MotionSites, VibecodeComponents).

**The handoff:**
```
ARDS system-setup → brand brief + token summary → formatted as Trickle system prompt
ARDS asset-generation (prompt-based registry) → layout prompts → paste into Trickle Magic Canvas
```

**URL:** [trickle.so](https://trickle.so)

**Status:** Ecosystem (prompt-based builder target)

---

### StyleUI ✦ Framework-Agnostic Environments

**What it is:** A vanilla JavaScript + CSS component library. No React, no framework dependency. Components are available via CDN or npm.

**Why it belongs with ARDS:**
Most ARDS integrations assume a React/Tailwind stack. StyleUI is the exception path — when the target environment is plain HTML/CSS (CMS-based sites, email templates, static pages), StyleUI components accept ARDS CSS custom properties directly. ARDS token files export as CSS variables that map onto StyleUI's variable architecture without transformation.

**The handoff:**
```
ARDS token file → CSS custom properties export → paste into StyleUI project root
```

**URL:** [styleui.dev](https://styleui.dev)

**Status:** Ecosystem (CSS variable target for non-React environments)

---

## Tier 3 — Reference & Workflow Resources

### Vibecoder.me ✦ Vibe Coding Workflow Reference

**What it is:** A vibe coding toolkit and blog covering tools, techniques, and workflows for building with AI instead of writing code manually.

**How ARDS uses it:**
When documenting how ARDS outputs get consumed downstream in a vibe coding workflow, vibecoder.me is the reference hub. Useful when a user is new to prompt-based building and needs orientation on the broader ecosystem that ARDS plugs into.

**URL:** [blog.vibecoder.me](https://blog.vibecoder.me)

---

### Bundlephobia ✦ Component Library Vetting Tool

**What it is:** An npm package size analyzer. Paste any package name and it returns the minified size, gzip/Brotli compressed size, estimated download time across network conditions, and the full dependency tree.

**How ARDS uses it:**
Before committing to a component registry in `asset-generation` Step 1.5, use Bundlephobia to check the bundle cost of the candidate library — especially relevant when comparing similar-purpose libraries (e.g., reactbits vs. magicui) for a performance-sensitive project. ARDS should surface the bundle size of the selected registry when the user's product tier prioritizes Core Web Vitals.

**Decision rule:** If a library exceeds ~50kb gzipped for its base install, flag it to the user and offer a lighter-weight alternative from the registry before proceeding.

**URL:** [bundlephobia.com](https://bundlephobia.com)

**Status:** Reference (vetting tool, no direct ARDS output integration)

---

## Integration Decision Framework

When evaluating a new integration request:

1. **Does ARDS produce something this tool can consume?** What format, what transform is needed?
2. **Does this serve the primary persona (independent designer) or only a niche?**
3. **Is the handoff zero-friction?** If it requires manual transformation, can ARDS produce the transformed format directly?
4. **Does this create a two-way dependency?** ARDS should always be upstream.
5. **Is the partner tool growing or declining?** Prioritize tools with active communities (Lovable, Tokens Studio, Refero) over legacy tools.

---

## Tier Summary

| Tool | Tier | Role | Status |
|---|---|---|---|
| Figma | 1 | Design system host | Wired |
| Refero / styles.refero.design | 1 | Figma peer — real-world reference MCP | Wired |
| n8n | 1 | Orchestration backbone — 1,000+ app reach | Ecosystem |
| Lovable | 1 | React app builder | Planned v0.3.0 |
| Tokens Studio | 1 | Token sync to Figma | Planned v0.3.0 |
| Tailwind CSS | 1 | CSS framework — token output target | Wired |
| Ideogram | 2 | Brand image generation + ad creatives | Ecosystem |
| Canva | 2 | Marketing asset creation (social, ads, email) | Ecosystem |
| Tally | 2 | Forms, waitlists, lead capture | Ecosystem |
| Stripe | 2 | Products, subscriptions, payment links | Ecosystem |
| v0 (Vercel) | 2 | React/Tailwind builder | Planned v0.3.0 |
| Cursor / Copilot | 2 | Code editor with CSS variables | Ecosystem |
| Storybook | 2 | Component docs | Planned v0.4.0 |
| GitHub Actions | 2 | CI audit hook | Planned v0.4.0 |
| Manus | 2 | Autonomous agent runner | Ecosystem |
| Skiper UI | 2 | shadcn Code Connect target | Ecosystem |
| Cult UI | 2 | shadcn Code Connect + AI patterns | Ecosystem |
| Trickle | 2 | No-code AI builder | Ecosystem |
| StyleUI | 2 | Framework-agnostic CSS target | Ecosystem |
| Vibecoder.me | 3 | Workflow reference | Reference |
| Bundlephobia | 3 | Library vetting tool | Reference |

---

---

## Version history

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.5 | 2026-07-01 | Kelwadis Butler | Added Tailwind CSS as a standalone Tier 1 entry (Wired) — promotes the existing `tailwind.config.js` output out of the Lovable section so it's a builder-agnostic target. Updated tier summary table. |
| 1.4 | 2026-06-24 | Kelwadis Butler | Added Business Factory Architecture section with full n8n orchestration diagram and end-to-end launch sequence. Added n8n as Tier 1 orchestration backbone. Added Tier 2 business factory stack: Ideogram (image gen), Canva (marketing assets), Tally (forms/waitlist), Stripe (monetization). Updated description frontmatter. Updated tier summary table. |
| 1.3 | 2026-06-24 | Kelwadis Butler | Added Bundlephobia as Tier 3 vetting tool with 50kb decision rule. Added Bundlephobia to tier summary table. |
| 1.2 | 2026-06-23 | Kelwadis Butler | Added Refero / styles.refero.design as Tier 1 Figma peer integration (MCP + Figma plugin). Added Tier 2 entries: Manus (agent runner), Skiper UI (Code Connect), Cult UI (Code Connect + AI SDK patterns), Trickle (no-code builder), StyleUI (framework-agnostic CSS). Added Tier 3 reference: Vibecoder.me. Updated tier summary table. Updated description frontmatter. |
| 1.1 | 2026-05-01 | Kelwadis Butler | Added Tier 2 ecosystem entries for v0, Cursor/Copilot, Storybook, GitHub Actions. Added Integration Decision Framework. |
| 1.0 | 2026-05-01 | Kelwadis Butler | Initial release. Tier 1 integrations: Figma (wired), Lovable (planned), Tokens Studio (planned). |
