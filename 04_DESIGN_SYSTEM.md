# Design System

Purpose: Defines the visual/design principles ARDS enforces in what it generates, and ARDS's own presentation identity (it has no UI of its own — this plugin is text/markdown only).
Last Updated: 2026-07-08
Related Documents: 01_PRD.md, DECISION_LOG.md
Version: 0.5

## ARDS has no UI of its own

Unlike the template this doc is adapted from (which described a product's own screens), ARDS is a Claude plugin — its only "interface" is conversation and the files it writes (JSON, markdown, HTML). There is no app to skin. What belongs in this document instead is (1) the design principles ARDS enforces on *client* outputs, and (2) ARDS's own written voice, since text is the only surface it has.

## Principles ARDS enforces on every client design system

Sourced from `skills/system-setup/SKILL.md`, `skills/token-update/SKILL.md`, and `CONNECTORS.md`:

1. **Two-tier separation** — Marketing (Tier 1: ads, email, landing pages, social, print) and Product (Tier 2: web/mobile app, components, data viz) draw from one token source of truth but must stay visually coherent, not identical. `system-audit` treats blending them as a hard failure.
2. **No raw values below the primitive tier** — every semantic and component token must alias upward; never a hardcoded hex, px, or font name outside a primitive token. Enforced as a "rule that must never be broken" in three separate skills.
3. **DTCG format, always** — W3C Design Tokens Community Group JSON format is the one token format ARDS produces. No proprietary schema.
4. **Default base system is Radix Primitives + shadcn/ui (web)** — headless, accessible, MIT-licensed, chosen specifically for Figma-variable-theming compatibility. Alternatives (React Native Paper/NativeBase for mobile, Carbon/Fluent 2 for enterprise, Blank for Figma-native workflows) are named, reasoned alternatives, not defaults — see `skills/system-setup/references/base-system-comparison.md`.
5. **Default plug points**: Heroicons (icons), Google Fonts (type), Unsplash (imagery), Recharts/Victory Native (data viz) — all swappable per client via the configuration block's `_override` fields. See `CONNECTORS.md`.
6. **Imagery follows a literalness spectrum, not a fixed rule**: photography (acquisition-facing, emotional), illustration (concept-bridging or low-stakes functional moments), real UI screenshots (proving the product works), iconography (dense/functional/data-facing). Full framework: `skills/asset-generation/SKILL.md` Step 5.
7. **8pt spacing grid** — stated as the spacing discipline in `asset-generation` Step 5.

## ARDS's own voice (from `skills/virtual-pm/SKILL.md`)

- **Never say:** "AI that designs for you" — frames AI as a replacement.
- **Always say:** "A design system architect available for every engagement" — frames it as capability augmentation.
- **Tone:** confident, specific, practitioner-to-practitioner. Not hype.
- **Trust signals:** real token files, real audit rubrics, named base systems with tradeoffs stated explicitly — never a vague claim without a concrete artifact behind it.

This voice guideline applies to README.md, this doc set, and any public-facing copy (Product Hunt listing, social posts) — see `skills/launch-playbook/SKILL.md`.

## Status

Directional and enforcement-rule level, matching what the shipped skills actually check for — not a component-level spec, because ARDS doesn't ship components; it generates them per client. Client-facing component-level specs are produced fresh per engagement by `asset-generation` and `system-setup`, not standardized here.
