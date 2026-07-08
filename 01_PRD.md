# Product Requirements Document

Purpose: Defines what AI-Ready Design Systems (ARDS) is, who it's for, and what's in/out of scope for the current release.
Last Updated: 2026-07-08
Related Documents: 00_CLAUDE_INSTRUCTIONS.md, 02_INFORMATION_ARCHITECTURE.md, 06_ROADMAP.md, DECISION_LOG.md
Version: 0.5

## Vision

A white-label Claude plugin that acts as a Brand & Design System Architect — setting up two-tier design systems, generating DTCG-format design tokens, producing tone-aware UX copy, and auditing assets for brand compliance. Built to be deployed once and customized per client. (Source: README.md.)

## Primary Persona

**The Independent Designer** — freelancers and small design studios (1–5 people) running multiple client engagements simultaneously, who currently rebuild the same design-system infrastructure (tokens, copy voice, audit rubric) from scratch for every client.

## Secondary Persona

**The AI-Native Founder** — a solo or tiny team building a product with AI tooling (Lovable, Cursor, v0) who has an idea but no brand infrastructure, and would otherwise ship on generic defaults.

## Tertiary Persona

**The Design Manager at a Growing Startup** — managing 2–4 designers across marketing and product with no dedicated design-systems engineer yet.

(Source: `skills/virtual-pm/SKILL.md`. Status of these personas: see `07_USER_RESEARCH.md` — they are reasoned hypotheses, not yet validated against real users.)

## Current Release (v0.5.0)

Eight shipped skills:

- **system-setup** — brand extraction from a URL, base design system recommendation, DTCG token generation, Figma variable spec, HTML style guide
- **copy-generation** — tone-aware UX and marketing copy across empty states, errors, CTAs, onboarding, transactional email, notifications
- **token-update** — targeted edits to an existing DTCG token file with alias-architecture preservation
- **system-audit** — brand/token compliance audit with Critical/High/Medium/Low severity findings
- **asset-generation** — user-story-driven wireframing through to a Figma-MCP-ready Claude Design JSON spec
- **integrations** — documentation and handoff guides for every downstream tool ARDS produces output for
- **launch-playbook** — GitHub readiness, launch strategy, community building for the ARDS project itself
- **virtual-pm** — product vision, personas, roadmap prioritization, OKRs for the ARDS project itself

Full step-by-step behavior for each skill: `05_PROMPT_ARCHITECTURE.md`. Full roadmap and shipped/next/later breakdown: `06_ROADMAP.md`.

## Out of Scope (current release)

- Live multi-user collaboration
- A hosted/SaaS version of the plugin (self-host / plugin-install only)
- Direct, automated write-back to Figma variables (today's Figma output is a spec/JSON a human or the Figma MCP applies — see `05_PROMPT_ARCHITECTURE.md`)
- Multi-client workspace management in a single session (tracked as a later roadmap item, see `06_ROADMAP.md`)
- A built-in `brand-strategy` discovery workflow (tracked in `IDEAS_BACKLOG.md`; today `system-setup` assumes brand strategy already exists or falls back to a placeholder-labeled neutral system)
- Monetization / paywall (see pricing philosophy in `skills/virtual-pm/SKILL.md` — plugin is MIT-licensed and free; distribution is the current goal, not revenue)

## Note on version numbering

`.claude-plugin/plugin.json` tracks the plugin's overall release version (this document uses that number). Individual `skills/*/SKILL.md` files maintain their own independent `## Version history` tables (e.g., `integrations/SKILL.md` is internally at 1.5). These two version schemes are not the same number and should not be conflated — a skill's internal version can advance independently of a plugin-wide release bump. This is flagged here because it's a real source of confusion in the existing docs, not a new decision.
