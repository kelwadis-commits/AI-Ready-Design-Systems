# Ideas Backlog — AI-Ready Design Systems

Purpose: Holds every idea that isn't in the current shipped release, so nothing gets lost. Nothing here is deleted — only reprioritized or promoted to DECISION_LOG.md / 06_ROADMAP.md.
Last Updated: 2026-07-08
Related Documents: 01_PRD.md, 02_INFORMATION_ARCHITECTURE.md, 03_DATABASE.md, DECISION_LOG.md
Version: 0.1

---

## B-001 — brand-strategy skill (9-layer discovery workflow)

**Title:** Built-in brand strategy discovery skill
**Description:** A 9-layer brand strategy workflow (foundational discovery, market positioning, audience definition, brand narrative, creative direction, go-to-market, long-term evolution) as its own skill, rather than assuming brand strategy already exists when `system-setup` runs.
**Source:** README.md "Skills planned for future releases."
**Priority:** High — `system-setup` Step 1 currently has to fall back to a placeholder-labeled neutral system when no brand strategy exists; this closes that gap at the source.
**Complexity:** Unknown — no target version or scoped step sequence exists yet in any source doc.
**Dependencies:** None blocking.
**Questions Remaining:** Does this become its own skill, or a new Step 0 inside `system-setup`? What's the minimum viable layer count for v1 vs. all 9?
**Status:** Backlog

---

## B-002 — Tokens Studio export format

**Title:** `.json` export compatible with Tokens Studio for Figma
**Description:** ARDS currently outputs DTCG-format tokens; Tokens Studio needs its own compatible JSON shape to sync tokens to GitHub via its Figma plugin.
**Source:** `skills/integrations/SKILL.md`, status "Planned for v0.3.0."
**Priority:** Medium — named Tier 1 integration, currently blocked on the transform not existing yet.
**Complexity:** Low-Medium — a format transform of an artifact ARDS already produces (see `03_DATABASE.md` artifact #2), not new token logic.
**Dependencies:** None blocking.
**Questions Remaining:** None stated in source docs.
**Status:** Backlog

---

## B-003 — Lovable handoff template (shadcn config + Tailwind theme)

**Title:** Direct Lovable project handoff
**Description:** A `tailwind.config.js` theme extension and shadcn CSS variable block (`globals.css`) generated directly from the token file, plus a brand brief formatted as a Lovable system-prompt preamble.
**Source:** `skills/integrations/SKILL.md`, status "Planned for v0.3.0." Note: the Tailwind CSS transform itself already shipped and was promoted to its own standalone Tier 1 entry per integrations v1.5 (2026-07-01) — what remains open is the Lovable-specific system-prompt preamble packaging.
**Priority:** Medium-High — Lovable is named as the primary React/Tailwind/shadcn builder target and pairs directly with the existing token architecture.
**Complexity:** Low — mostly packaging of an existing output in a different wrapper.
**Dependencies:** None blocking.
**Questions Remaining:** None stated in source docs.
**Status:** Backlog

---

## B-004 — v0 (Vercel) integration

**Title:** v0 as a named builder target
**Description:** Document v0 as a first-class integration target, similar to the Lovable and Tailwind CSS entries.
**Source:** `skills/integrations/SKILL.md` tier summary table, status "Planned v0.3.0."
**Priority:** Low-Medium — currently only listed in the tier summary table, no dedicated entry or handoff spec written yet (unlike Lovable and Tailwind CSS, which have full sections).
**Complexity:** Likely low, similar shape to the Tailwind CSS entry.
**Dependencies:** None blocking.
**Questions Remaining:** Does v0's output format need its own transform, or does the existing Tailwind CSS transform (B-003 sibling) already cover it?
**Status:** Backlog

---

## B-005 — GitHub Actions integration (CI token compliance check)

**Title:** Wire `system-audit`'s token compliance check as a CI step
**Description:** Run the token/alias compliance layer of `system-audit` automatically on PRs via GitHub Actions, rather than only on-demand in a Claude session.
**Source:** `skills/integrations/SKILL.md` tier summary table ("Planned v0.4.0") and `skills/virtual-pm/SKILL.md` Later roadmap.
**Priority:** Medium — real value for teams with a CI pipeline, but requires ARDS logic to run outside a live Claude session, which is a different execution model than anything shipped today.
**Complexity:** High — `system-audit` currently runs as an interactive Claude skill, not a standalone script; this would need a non-conversational execution path.
**Dependencies:** Needs a decision on how (or whether) ARDS logic runs outside a Claude session at all.
**Questions Remaining:** Does this require extracting the audit rubric into a standalone script, separate from the SKILL.md instructions?
**Status:** Backlog

---

## B-006 — Storybook export

**Title:** Component documentation stubs from the design system config
**Description:** Generate Storybook-compatible component doc stubs from the client configuration block and token file.
**Source:** `skills/integrations/SKILL.md` tier summary table and `skills/virtual-pm/SKILL.md` Later roadmap, both "Planned v0.4.0."
**Priority:** Low-Medium — useful for teams already on Storybook, but no named urgency in source docs.
**Complexity:** Unknown — depends on how much of a real component library (vs. tokens only) ARDS would need to model.
**Dependencies:** Likely depends on `asset-generation`'s Claude Design JSON format being stable.
**Questions Remaining:** None stated in source docs.
**Status:** Backlog

---

## B-007 — Multi-client workspace

**Title:** Manage multiple client configuration blocks in one session
**Description:** Today, one client config block (see `03_DATABASE.md` artifact #1) exists per engagement/conversation. This would let a user hold several client engagements' state simultaneously.
**Source:** `skills/virtual-pm/SKILL.md` Later roadmap.
**Priority:** Medium — directly serves the Independent Designer persona's stated pain (running multiple engagements at once), but that persona itself is unvalidated (see `07_USER_RESEARCH.md`).
**Complexity:** Medium-High — every skill currently assumes a single config block in context; this would need explicit client-switching logic across all 8 skills.
**Dependencies:** Core single-client flow (shipped) should be well-tested first.
**Questions Remaining:** Is this a session-scoped feature (name the client each time) or does it require actual persistence between sessions, which ARDS doesn't have today?
**Status:** Backlog

---

## B-008 — Figma plugin companion (direct variable write-back)

**Title:** A dedicated Figma plugin for writing tokens directly into Figma variables
**Description:** Today, `system-setup` Step 5 either calls `mcp__Figma__get_variable_defs` (read/diff only) or outputs a structured text spec a human applies manually. A companion plugin could write variables directly.
**Source:** `skills/virtual-pm/SKILL.md` Parking Lot.
**Priority:** Low (explicitly "evaluate after traction" in source doc).
**Complexity:** High — new artifact type (an actual Figma plugin, not a markdown skill), outside ARDS's current all-markdown architecture (see `00_CLAUDE_INSTRUCTIONS.md`).
**Dependencies:** Real usage signal that manual Figma variable entry is a significant friction point.
**Questions Remaining:** None stated in source docs — flagged explicitly as post-traction only.
**Status:** Backlog (parking lot)

---

## B-009 — Webflow variable export

**Title:** Token export targeting Webflow's variable system
**Description:** A transform of the DTCG token file into whatever format Webflow's design variables consume.
**Source:** `skills/virtual-pm/SKILL.md` Parking Lot.
**Priority:** Low (explicitly "evaluate after traction").
**Complexity:** Unknown — Webflow's variable API/format wasn't researched as part of this doc pass; needs its own investigation before scoping.
**Dependencies:** None blocking.
**Questions Remaining:** What does Webflow's variable format actually require? Not yet researched.
**Status:** Backlog (parking lot)

---

## B-010 — Figma-to-token reverse engineering

**Title:** Generate a DTCG token file from an existing Figma file's variables, instead of the other way around
**Description:** Today ARDS only goes token file → Figma variable spec. This would run the pipeline backward: existing Figma variables → DTCG token file, for clients who already have a Figma system and want it formalized into ARDS's token architecture.
**Source:** `skills/virtual-pm/SKILL.md` Parking Lot.
**Priority:** Low (explicitly "evaluate after traction").
**Complexity:** Medium — `mcp__Figma__get_variable_defs` already exists and is used for diffing today, so the read capability is partly there; the gap is mapping arbitrary existing Figma variable names into ARDS's primitive/semantic/component alias structure, which isn't a mechanical transform.
**Dependencies:** None blocking.
**Questions Remaining:** How does this handle a Figma file that doesn't already follow a three-tier alias structure — does it force-fit, or flag for manual review?
**Status:** Backlog (parking lot)
