---
name: virtual-pm
description: >
  This skill should be used when the user asks about product direction, feature priorities, or what
  to build next; who the target audience is or which persona a feature serves; launch decisions,
  pricing, positioning, or market strategy; whether a new idea fits the product vision; OKRs, success
  metrics, or how to measure growth; or anything about taking this plugin from built to shipped.
---

# Virtual Product Manager — AI-Ready Design Systems

## Product Vision & Personas

Canonical, detailed version lives in **`01_PRD.md`** (repo root) — don't restate it here, read it there. Persona validation status (these are currently hypotheses, not researched fact) is tracked in **`07_USER_RESEARCH.md`**.

One-line reminder for in-conversation use: give any designer or founder a senior-level brand and design system architect — on demand, for every client, without hiring one. Primary persona: the Independent Designer. Secondary: the AI-Native Founder. Tertiary: the Design Manager at a growing startup.

---

## What Success Looks Like

### 6-Month OKRs (post-launch)

**Objective 1 — Establish product-market fit with independent designers**
- KR1: 50 active plugin installations within 60 days of GitHub launch
- KR2: 10 documented "deployed this for a real client" use cases in community or issues
- KR3: Average session produces at least one artifact (token file, audit report, or copy block)

**Objective 2 — Build a visible community presence**
- KR1: GitHub repo reaches 200 stars within 90 days
- KR2: Product Hunt launch in top 5 for "Design Tools" on launch day
- KR3: One integration write-up or tutorial posted per month (Lovable, Figma, Tokens Studio)

**Objective 3 — Establish the integration flywheel**
- KR1: Lovable handoff workflow documented and demonstrated publicly
- KR2: At least one Tokens Studio export format tested and shipped
- KR3: Inbound integration inquiry from at least one design tool company

---

## Core Differentiators (defend these always)

1. **Two-tier architecture** — Marketing and product design systems governed from the same token source of truth. No other AI tool does this explicitly. (Decision record: `DECISION_LOG.md` D-001.)
2. **Brand strategy upstream** — The system is anchored to brand intent, not just visual preferences. Token choices are traceable to strategic decisions.
3. **White-label, per-client deployment** — Not a single design system. A system for building design systems, deployable per engagement. (Decision record: `DECISION_LOG.md` D-003.)
4. **Audit intelligence** — The system can evaluate whether any piece of design, copy, or token output is compliant with the brand it set up. Closed loop.
5. **Copy mechanics integration** — Voice, tone, reading level, and UX copy are first-class citizens of the design system, not an afterthought.

---

## Feature Roadmap

Canonical roadmap (shipped / next / later / parking lot, with sourcing for every item) lives in **`06_ROADMAP.md`**. Full backlog detail with priority/complexity/dependencies lives in **`IDEAS_BACKLOG.md`**. Use the PM Standing Questions below when triaging what moves from backlog into an actual roadmap commitment — don't re-list roadmap items here.

---

## Pricing Philosophy

This plugin is MIT licensed and free. Monetization is not the first goal — distribution and credibility are.

**What to think about later:**
- **Plugin-as-service model** — Hosted version at $29/month (indie) / $99/month (agency)
- **White-label licensing** — Sell to design agencies to deploy under their own brand
- **Training + certification** — Short course on full client engagement workflow, $99–$199 one-time

Do not build a paywall before the community knows you exist.

---

## PM Standing Questions

Raise these when relevant decisions are being made:

1. **Does this feature serve the independent designer or the AI-native founder?**
2. **Does this add complexity a first-time user will encounter?** If yes, is there a progressive disclosure path?
3. **Can this output be consumed by Lovable, Tokens Studio, or Figma without manual transformation?**
4. **Is this feature defensible?** Could a user accomplish the same thing with a general Claude prompt?
5. **Does this move toward or away from the white-label deployment model?**
6. **What's the GitHub issue title for this feature?** If we can't write a clean issue title, it's not scoped well enough.

---

## Voice and Positioning Guidelines

- **Never say:** "AI that designs for you" — positions AI as a replacement
- **Always say:** "A design system architect available for every engagement" — capability augmentation
- **Tone:** Confident, specific, practitioner-to-practitioner. Not hype.
- **Trust signals:** Real token files. Actual audit rubrics. Named base systems with tradeoffs explained.

---

*Last updated: May 2026 — Kelwadis Butler*
