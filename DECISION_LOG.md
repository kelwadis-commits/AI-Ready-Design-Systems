# Decision Log — AI-Ready Design Systems

Purpose: Permanent record of accepted product/technical decisions and the reasoning behind them. Rejected or deferred ideas go to IDEAS_BACKLOG.md, not here.
Last Updated: 2026-07-08
Related Documents: 01_PRD.md, 02_INFORMATION_ARCHITECTURE.md, 03_DATABASE.md, 05_PROMPT_ARCHITECTURE.md
Version: 0.5

---

## D-001 — Two-tier architecture: Marketing and Product design systems, one token source of truth

**Date:** Undated in source (present since the earliest version this doc set could verify — `system-setup/SKILL.md` v1.0, 2026-05-01).
**Status:** Accepted

**Decision:** ARDS splits every design system it produces into Tier 1 (Marketing: ads, email, landing pages, social, print) and Tier 2 (Product: web/mobile app, components, data viz), governed from one shared brand strategy and token source of truth.

**Why:** Stated as the plugin's core differentiator in `skills/virtual-pm/SKILL.md`: "No other AI tool does this explicitly." `system-audit` enforces tier separation as a non-negotiable rule, treating a marketing pattern appearing in a product component (or vice versa) as a hard failure, not a style preference.

**Affected:** `README.md`, `skills/system-setup/SKILL.md`, `skills/system-audit/SKILL.md`, `04_DESIGN_SYSTEM.md`.

---

## D-002 — Token format is W3C DTCG, three-tier alias chain enforced everywhere

**Date:** `system-setup/SKILL.md` v1.0 (2026-05-01).
**Status:** Accepted

**Decision:** All generated tokens are W3C Design Tokens Community Group (DTCG) format JSON, split by platform, with a strict primitive → semantic → component alias chain. No raw values permitted below the primitive tier; no level-skipping.

**Why:** Stated as a "rule that must never be broken" independently in `system-setup/SKILL.md`, `token-update/SKILL.md`, and `system-audit/SKILL.md` — this is the mechanism that keeps generated design systems auditable and prevents drift.

**Affected:** `03_DATABASE.md`, `04_DESIGN_SYSTEM.md`.

---

## D-003 — Figma is the one wired/required integration; every other tool is a documented plug point

**Date:** `system-setup/SKILL.md` v1.0 (2026-05-01); formalized in `CONNECTORS.md`.
**Status:** Accepted

**Decision:** The Figma MCP is configured directly in `.mcp.json` and treated as required infrastructure. Icon library, font system, asset library, and data viz library are documented "plug points" — defaults are named (Heroicons, Google Fonts, Unsplash, Recharts) but swappable per client via the configuration block's `_override` fields, with no code change required.

**Why:** ARDS is explicitly designed as a white-label, per-client-deployable plugin (`README.md`), so anything client-specific has to be swappable without editing skill logic. Figma is the exception because it's the design tool the whole plugin is architected around, not a per-client preference.

**Affected:** `CONNECTORS.md`, `README.md`, `03_DATABASE.md`.

---

## D-004 — n8n adopted as the Tier-1 orchestration backbone instead of individual per-tool MCPs

**Date:** Per `skills/integrations/SKILL.md` version history, v1.4, 2026-06-24.
**Status:** Accepted

**Decision:** Rather than building or wiring a separate MCP integration for every downstream tool (Lovable, Ideogram, Canva, Tally, Stripe, etc.), ARDS documents n8n as a single Tier-1 orchestration layer: one MCP connection, 1,000+ app reach, with ARDS sending one structured instruction that n8n fans out.

**Why:** Stated in `skills/integrations/SKILL.md`: "Architecture pattern: `Claude → MCP → n8n → {target apps}` — never `Claude → 20 separate MCPs`." This is a scaling decision — it avoids linear growth in integration maintenance as more downstream tools get added.

**Affected:** `skills/integrations/SKILL.md`, `06_ROADMAP.md`.

---

## D-005 — Refero added as a Figma peer MCP (real-world reference screens), not a downstream consumer

**Date:** Per `skills/integrations/SKILL.md` version history, v1.2, 2026-06-23. Also reflected in `skills/system-setup/SKILL.md` v1.1, 2026-06-23.
**Status:** Accepted

**Decision:** Refero (styles.refero.design) is documented as operating *alongside* the Figma MCP, not downstream of it — the Figma MCP reads the user's own file; Refero reads real production screens from other products. `system-setup` Step 1 offers pulling a Refero DESIGN.md style profile as an optional grounding step before token generation.

**Why:** Gives ARDS a source of real-world pattern benchmarks (what Stripe, Linear, Notion actually do) in addition to the user's own file state — closes a gap where token generation could otherwise start from nothing but the brand brief.

**Affected:** `skills/integrations/SKILL.md`, `skills/system-setup/SKILL.md`.

---

## D-006 — Default icon library changed from Google Material Symbols to Heroicons

**Date:** git commit `73371ad`, 2026-07-05; also `skills/system-setup/SKILL.md` version history v1.4, 2026-07-01 (note: the skill's own internal version date and the git commit date don't match exactly — flagging the discrepancy rather than resolving it, since both are directly-sourced facts and I can't independently confirm which is correct).
**Status:** Accepted

**Decision:** Heroicons (MIT-licensed, ~300 icons, built by the Tailwind CSS team) became the default icon library plug point, replacing Google Material Symbols. Tabler Icons (6,100+ icons) was added as the named swap option for projects needing broader coverage than Heroicons provides.

**Why:** Stated in `system-setup/SKILL.md` v1.4: alignment with the plugin's Tailwind CSS default — both Heroicons and Tailwind come from Tailwind Labs, giving a tighter default stack.

**Affected:** `skills/system-setup/SKILL.md`, `skills/asset-generation/SKILL.md`, `CONNECTORS.md`, `04_DESIGN_SYSTEM.md`.

---

## D-007 — Adopted an 11-document governance/doc-set layer for the ARDS repo itself

**Date:** 2026-07-08.
**Status:** Accepted

**Decision:** Kel provided an 11-file "startup OS" documentation template (originally written for an unrelated costume-design product) and asked to repurpose it as ARDS's own governance layer — instructions and living documentation for whoever (human or Claude) works on the ARDS plugin. The files (00_CLAUDE_INSTRUCTIONS.md through IDEAS_BACKLOG.md) now live at repo root, tailored to ARDS's actual skill set and grounded in the plugin's real file structure, version history tables, and git log — not the original template's fictional subject matter.

**Why:** Kel decided the new root docs should be the source of truth for vision/roadmap/decisions, with `skills/virtual-pm/SKILL.md` and `skills/launch-playbook/SKILL.md` trimmed to reference them rather than duplicate content (avoiding two places for the same fact to drift apart). `07_USER_RESEARCH.md` was explicitly written as an unvalidated hypothesis log rather than presenting virtual-pm's personas as researched fact, since no real user research exists yet for ARDS.

**Affected:** All 11 root docs, `README.md` (file structure correction), `skills/virtual-pm/SKILL.md`, `skills/launch-playbook/SKILL.md`, `.claude-plugin/plugin.json` (version bump 0.4.0 → 0.5.0).
