# Development Roadmap

Purpose: Sequences ARDS's development and tracks changes/bugs as they happen.
Last Updated: 2026-07-08
Related Documents: 01_PRD.md, DECISION_LOG.md
Version: 0.5

## A note on version numbers before reading this doc

Two separate version schemes exist in this repo and are **not interchangeable**:
- `.claude-plugin/plugin.json` — the plugin's release version (currently 0.5.0 as of this doc set landing; was 0.4.0 before).
- Each `skills/*/SKILL.md`'s own `## Version history` table — tracks that skill's internal revisions independently (e.g. `integrations/SKILL.md` is internally at 1.5, `system-setup/SKILL.md` at 1.5, `asset-generation/SKILL.md` at 1.4, `token-update/SKILL.md` at 1.1).
`skills/virtual-pm/SKILL.md` previously referred to "Shipped (v0.2.0)" for a feature set that includes all 8 current skills — that can't be reconciled against git history (see Changelog below, only 4 commits exist, none show a 0.2.0 → 0.4.0 transition) or against the per-skill version tables (several skills are internally past v1.0). Treat that v0.2.0 label as stale/unverifiable, not as a confirmed historical fact. This doc's Shipped section below reflects the current plugin.json version (0.5.0) against what's actually on disk, not a reconstructed history that can't be verified.

## Shipped (current — v0.5.0)

- system-setup, copy-generation, token-update, system-audit, asset-generation, integrations, launch-playbook, virtual-pm — all 8 skills, verified present on disk 2026-07-08 (see `02_INFORMATION_ARCHITECTURE.md`).
- Full 11-document governance/doc set (this file and its siblings) — added 2026-07-08.

## Next

- **brand-strategy skill** — 9-layer brand strategy discovery workflow (named in README.md "Skills planned for future releases"; no target version stated in the source doc).
- **Tokens Studio export** — `.json` compatible with Tokens Studio for Figma (`skills/integrations/SKILL.md` status: "Planned for v0.3.0").
- **Lovable handoff template** — shadcn config + Tailwind theme for direct Lovable use (`skills/integrations/SKILL.md` status: "Planned for v0.3.0").
- **v0 (Vercel) integration** — listed "Planned v0.3.0" in the integrations tier summary table.

## Later

- **Multi-client workspace** — manage multiple client config blocks in one session (`skills/virtual-pm/SKILL.md`).
- **GitHub Actions integration** — token compliance check wired as a CI step (`skills/integrations/SKILL.md` status: "Planned v0.4.0"; `skills/virtual-pm/SKILL.md` also lists this).
- **Storybook export** — component documentation stubs from the design system config (`skills/integrations/SKILL.md` status: "Planned v0.4.0").

## Parking Lot (evaluate after traction)

- Figma plugin companion — write tokens directly to Figma variables via API (currently the Figma MCP handles reads/variable-defs, not a dedicated write-back plugin).
- Webflow variable export.
- Figma-to-token reverse engineering.

Full detail and priority reasoning for all of the above: `IDEAS_BACKLOG.md`.

## Changelog

Reconstructed from `git log` (verified 2026-07-08 — this is the full commit history, 4 commits total):

- **2026-07-01** — `b1ca0e2` Import ARDS plugin into version-controlled repo. (First commit — no earlier history exists in this repo to reconstruct from.)
- **2026-07-05** — `73371ad` Add Heroicons, Storyset, footer.design; swap default icon library to Heroicons; add imagery decision framework.
- **2026-07-06** — `8925ce0` Add LDRS, Bento Grids, Awwwards; add Tabler Icons as icon swap option.
- **2026-07-06** — `5ae03d6` Bump plugin version to 0.4.0; sync README version and remove stale Skills header version tag.
- **2026-07-08** — Added full 11-document governance/doc set (00–07, CLAUDE_PLAYBOOK_INSTRUCTIONS.md, DECISION_LOG.md, IDEAS_BACKLOG.md), adapted from a reusable project-constitution template and tailored to ARDS's actual skill set. Corrected a stale File Structure section in README.md (was missing 4 of 8 skills). Trimmed `virtual-pm` and `launch-playbook` SKILL.md to reference the new docs instead of duplicating vision/roadmap/GTM content. Bumped plugin version 0.4.0 → 0.5.0.

Per-skill internal version histories (dates and changes for each skill's own revisions) live at the bottom of each `skills/*/SKILL.md` — not duplicated here to avoid the two version schemes drifting further apart. See the version-numbers note above.

## Bug Log

None logged. No issue tracker currently exists for this repo (see `skills/launch-playbook/SKILL.md` pre-launch checklist — GitHub Issues/Discussions are not yet enabled as of this doc's writing).
