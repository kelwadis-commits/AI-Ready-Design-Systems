---
name: launch-playbook
description: >
  This skill should be used when the user asks about GitHub repo readiness before going public,
  Product Hunt launch strategy or timing, where to post and how to get first users, README improvements
  or positioning copy, community building, Discord vs GitHub Discussions, what metrics to track
  post-launch, or content strategy for growing the ARDS project.
---

# Launch Playbook — AI-Ready Design Systems

## Phase 1 — GitHub Repo Readiness (pre-launch)

### Repository checklist

- [ ] Repo is public at `github.com/kelwadis-commits/AI-Ready-Design-Systems`
- [ ] README.md is the primary sales page — see README polish section below
- [ ] `LICENSE` file is present (MIT)
- [ ] `.gitignore` excludes any personal tokens or secrets
- [ ] `CHANGELOG.md` exists with v0.1.0 entry
- [ ] `CONTRIBUTING.md` exists with clear instructions for first-time contributors
- [ ] `CODE_OF_CONDUCT.md` exists (use the Contributor Covenant template)
- [ ] GitHub Topics added: `design-system`, `design-tokens`, `figma`, `claude`, `ai`, `brand-design`, `ux-copy`, `dtcg`, `tailwind`, `shadcn`
- [ ] At least 3 Issues created pre-launch with "good first issue" label
- [ ] GitHub Discussions enabled
- [ ] Repository social preview image set (1280×640px)

### README must answer five questions before the fold

1. **What is this?** — One sentence.
2. **Who is this for?** — Two sentences. Name the persona.
3. **What does it do?** — Each skill, in outcome terms (not feature terms).
4. **How do I get it?** — Installation in three steps or fewer.
5. **What does it produce?** — Show a real output: a DTCG token snippet, audit report excerpt, or copy block.

**Add a demo GIF** — a 30-second screen recording: brand brief goes in → token file comes out. This is the hook.

### Pre-launch GitHub Issues (signal activity before announcing)

1. `[Feature] Tokens Studio export format` — `enhancement`, `help wanted`
2. `[Feature] Lovable handoff: shadcn config generator` — `enhancement`
3. `[Docs] Add a full walkthrough video for system-setup` — `documentation`, `good first issue`
4. `[Feature] brand-strategy skill — discovery workflow` — `enhancement`, `roadmap`
5. `[Bug] Figma variable spec: conflict detection when variables already exist` — `bug`

---

## Phase 2 — Positioning and Messaging

### Headline options

A. "The design system architect that ships with every Claude session."
B. "Stop rebuilding your design system from scratch for every client."
C. "Brand tokens. Copy mechanics. Audit intelligence. One Claude plugin."
D. "Your AI design systems partner — for every engagement, every client."

**Recommendation:** Lead with B for Product Hunt (pain-first) and C for GitHub (feature-first).

### Positioning statement (internal use)

> AI-Ready Design Systems is a Claude plugin for independent designers and AI-native founders who need enterprise-quality brand and design system infrastructure without enterprise headcount. Unlike generic AI prompts or manual design system setups, ARDS generates structured, token-based, auditable design systems from a brand brief — and keeps them consistent across two tiers: marketing and product.

### One-liner for socials / bio

"A Claude plugin that sets up your design system, writes your UX copy, and audits your brand. MIT. Open source."

---

## Phase 3 — Launch Channels

### Product Hunt

- Launch Tuesday or Wednesday. Avoid Monday (crowded) and Friday (low engagement).
- Create Maker account and verify at least 2 weeks before launch.
- Build a "notify me" list before launch day.
- Tagline (120 chars max): use the pain-first headline.
- 3–5 screenshots: system-setup output, token file, audit report, copy block, Figma spec.
- Write the first comment yourself — explain the origin story.
- Respond to every comment on launch day.

**Target categories:** Developer Tools, Design Tools, Productivity

### Designer community channels (in priority order)

1. **Figma Community** — Post a resource or template demonstrating the plugin
2. **Dribbble / Behance** — Case study: brand brief in → full token system out
3. **Sidebar.io / Designer News** — "Show HN" style post with technical explainer
4. **Reddit: r/design, r/UI_Design, r/webdev** — Share with technical walkthrough, not self-promotion
5. **Twitter/X** — Thread: "I got tired of rebuilding design systems for every client, so I built a Claude plugin." Include real outputs.

### Developer / AI community channels

1. **Hacker News: Show HN** — "Show HN: An open-source Claude plugin that generates DTCG design tokens from a brand brief"
2. **Claude / Anthropic community forums** — First-party, high relevance
3. **Lovable Discord** — "I built a design system setup tool that hands off to Lovable. Here's the workflow."
4. **Cursor / v0 communities** — Same upstream-intelligence message

---

## Phase 4 — Content Strategy (post-launch)

| Month | Topic |
|---|---|
| 1 | Origin story + demo. Why you built it. Real outputs. |
| 2 | Integration story. "ARDS → Lovable: branded product in a day." |
| 3 | Case study. A real freelance engagement. Before/after on time spent. |
| 4 | Technical deep-dive. How DTCG token architecture works. SEO + credibility. |
| 5 | Community feature. Highlight a contributor. Signal the community is real. |
| 6 | v0.3.0 announcement. What changed and why. |

### SEO-friendly topics for wiki or companion blog

- "What is DTCG token format and why should designers care"
- "Two-tier design systems: marketing vs product explained"
- "How to hand off a design system to Lovable"
- "Why shadcn/ui + Radix is the right base for AI-generated design systems"
- "Design system governance for solo designers"

---

## Phase 5 — Community Health

**GitHub Discussions vs Discord:** Start with GitHub Discussions — zero setup, attached to the repo, where your users already are. Move to Discord only if discussion volume justifies it (typically 50+ active users).

**First 30 days rules:**
- Respond to every issue within 24 hours
- Close issues with a clear resolution note, not silently
- Thank every PR contributor by name in the merge commit message
- Pin a "Start here" discussion post

---

## Success Metrics

| Metric | Week 1 | Month 1 | Month 3 |
|---|---|---|---|
| GitHub stars | 25 | 100 | 200 |
| Plugin installs (via clone count) | 15 | 50 | 150 |
| Issues opened by others | 2 | 8 | 20 |
| Community PRs | 0 | 1 | 5 |
| Product Hunt upvotes | 50 | — | — |
| Social mentions / reposts | 5 | 20 | 50 |

---

*Last updated: May 2026 — Kelwadis Butler*
