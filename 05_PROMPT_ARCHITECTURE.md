# Prompt Architecture

Purpose: Defines how each ARDS skill actually reasons step-by-step, and how the client configuration block persists context across skills — the ARDS equivalent of "Project DNA."
Last Updated: 2026-07-08
Related Documents: 01_PRD.md, 03_DATABASE.md, DECISION_LOG.md
Version: 0.5

## The persistence principle

ARDS has no session memory of its own beyond the conversation. What makes outputs stay consistent across skills within one client engagement is the **client configuration block** (see `03_DATABASE.md` artifact #1) — generated once by `system-setup`, read by every other skill, and never regenerated from scratch mid-engagement. This is the direct equivalent of a "Project DNA" concept: later skill calls stay consistent with earlier decisions because they read the same block, not because ARDS remembers anything on its own.

## system-setup pipeline

`Step 0` Extract brand from URL (if provided) via `mcp__workspace__web_fetch` → structured extraction report → user confirms → `Step 1` check/collect brand strategy context, optional Refero visual-direction pull → `Step 2` recommend base design system, wait for confirmation → `Step 3` generate the client configuration block → `Step 4` generate DTCG token files (web + mobile) → `Step 5` generate Figma variable spec (live via MCP if connected, else structured text) → `Step 6` generate a self-contained HTML style guide from the token values.

Hard rule across all steps: never generate tokens or recommendations without at least a minimal brand brief; label placeholder output explicitly when the user opts to skip inputs.

## token-update pipeline

`Step 1` load and parse the existing token file, diff against live Figma variables if connected → `Step 2` classify the requested change by type and ripple impact (primitive/semantic/new/rename/delete/dark-mode-only) → `Step 3` apply the change following the primitive→semantic→component alias chain, with special-cased sub-flows for gradients (decompose into primitive color stops first) and renames/deletions (list dependents before acting) → `Step 4` output the complete updated file with a `_meta` block and a semver bump → `Step 5` explain the resulting Figma variable impact.

## asset-generation pipeline

`Step 0` capture a confirmed user story (persona/action/benefit) — nothing proceeds without this → `Step 1` select a transactional flow from a fixed menu (onboarding, auth, checkout, etc.) → `Step 1.5` select a component registry from a 17-entry aesthetic-to-library table, which also determines whether output later becomes JSON or copy-pasteable prompts (for prompt-based registries) → `Step 2` source real-world template references from up to 5 external sources (Uizard, Figma Community, Sprrrint, Envato Elements, Awwwards) → `Step 3` confirm brand context (token file/config, platform, Figma variable collection name) → `Step 4` present 2–4 wireframe options, no output generated before a selection → `Step 5` inject the brand system across tokens/copy/imagery/spacing, using the photography-vs-illustration-vs-iconography framework for imagery → `Step 6` generate Claude Design JSON with mandatory token binding on every visual property → `Step 7` deliver a human-readable component spec.

## system-audit pipeline

`Step 1` establish both the subject (asset/copy) and the reference (token file/brand strategy/config block) — refuses to proceed on either being missing → `Step 2` determine which audit layers apply (token compliance, tier separation, voice & tone, copy mechanics, alias integrity) based on what's being reviewed → `Step 3` run each applicable layer, producing severity-classified findings (Critical/High/Medium/Low) → `Step 4` summarize and prioritize into a single status (Clean / Needs attention / Blocked from shipping) → `Step 5` output the specific fix for every Critical/High finding.

## copy-generation pipeline

Operates on three declared layers before writing anything: **Voice** (brand character, from the config block's `copy_mechanics.voice`), **Tone** (contextual modulation via a fixed situation→register table), **Mechanics** (structural rules — reading level, sentence length, capitalization, active voice — see `references/copy-mechanics.md`). `Step 1` resolve brand context or fall back to labeled defaults → `Step 2` identify copy type and map to tone register → `Step 3` state the Voice/Tone/Mechanics declaration before any output — non-negotiable → `Step 4` generate 2–3 labeled variants → `Step 5` flag any intentional mechanic violation in a selected variant.

## What's still a sequence, not a formal spec

Each pipeline above is documented at the step level inside its SKILL.md, but there is no cross-skill orchestration layer — a user (or Claude) manually decides to run `system-setup` before `asset-generation`, for example. Nothing enforces run order except the "ask for the config block if missing" fallback each skill has individually. Sequencing the full engagement (which skill runs when) is currently implicit, driven by the user's request pattern — not a documented state machine. This is the ARDS-equivalent of the "sequence, not a spec" caveat the original template flagged for its own AI pipeline.
