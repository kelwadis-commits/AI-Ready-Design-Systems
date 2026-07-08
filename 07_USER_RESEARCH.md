# User Research — AI-Ready Design Systems

Purpose: Tracks the validation status of ARDS's target personas. As of this writing, **no primary or secondary user research has been conducted** for ARDS itself. Everything below is a hypothesis log, not a findings report — treat it accordingly.
Last Updated: 2026-07-08
Related Documents: 01_PRD.md, 02_INFORMATION_ARCHITECTURE.md, 03_DATABASE.md, 05_PROMPT_ARCHITECTURE.md, DECISION_LOG.md, IDEAS_BACKLOG.md
Version: 0.1

---

## Status: Unvalidated

I have no interview transcripts, survey data, published articles, or usage analytics about ARDS's actual users to draw on. Every persona, pain point, and "gain" statement below originates from `skills/virtual-pm/SKILL.md`, which reads as product reasoning (informed judgment about who this ought to serve) rather than sourced research. This document exists so that distinction stays visible and doesn't quietly become treated as validated fact over time.

I'm not going to invent interviews, quotes, or citations to fill this in — if you want this doc to hold real findings, it needs actual interviews, survey responses, or GitHub/community usage data once the plugin has real users (see `skills/launch-playbook/SKILL.md` for the launch plan that would generate that signal).

---

## Hypothesized Personas (unvalidated)

**1. The Independent Designer (primary, hypothesized)**
Assumed pain: rebuilds tokens/copy voice/audit rubric from scratch per client engagement.
Assumed gain: install once, configure per client, deploy consistently.

**2. The AI-Native Founder (secondary, hypothesized)**
Assumed pain: ships on generic defaults (Tailwind blue, system fonts, placeholder copy) for lack of brand infrastructure.
Assumed gain: a real design system from day one.

**3. The Design Manager at a Growing Startup (tertiary, hypothesized)**
Assumed pain: no dedicated design-systems engineer, no governance tooling.

None of these three have been validated against an actual person in this role. They're carried over verbatim from `skills/virtual-pm/SKILL.md` — see that file for the full pain/gain framing as currently written into the product.

---

## Open Questions to Validate

1. Does the "rebuild from scratch per client" pain actually describe how independent designers work, or do most already have a personal starter-kit/boilerplate that makes this less acute than assumed?
2. Do AI-native founders using Lovable/Cursor/v0 actually reach for a *separate* design-system tool, or do they expect brand/token setup to be a built-in step of the builder tool itself?
3. Is the Design Manager persona meaningfully different in needs from the Independent Designer persona, or is it currently just a headcount variation of the same job-to-be-done?
4. What does a real user's first session with `system-setup` actually look like — does the URL-extraction flow (Step 0) match how people actually start, or do most people start from a blank brief?
5. Once the plugin has GitHub stars/installs/issues (see `skills/launch-playbook/SKILL.md` success metrics), does real usage data support the "two-tier architecture" and "audit intelligence" differentiators claimed in `skills/virtual-pm/SKILL.md`, or do users primarily use one or two skills and ignore the rest?

---

## How to close this gap

Real research inputs that would upgrade this document from hypothesis log to findings report: direct interviews with 3–5 people who match each persona, a review of actual GitHub issues/discussions once the repo is public, or session transcripts from real client engagements once the plugin has been deployed a few times. Until one of those exists, don't cite this document as evidence that the personas are correct — cite it as evidence of what's currently assumed.
