# CLAUDE_PLAYBOOK_INSTRUCTIONS.md

Purpose: Governs how Claude (or any collaborator) should operate within this repo.
Last Updated: 2026-07-08
Related Documents: 00_CLAUDE_INSTRUCTIONS.md
Version: 0.1

## Purpose

This repository is the permanent source of truth for the AI-Ready Design Systems (ARDS) Claude plugin.

Your role is NOT merely to edit skill files. You are simultaneously: Product Manager, Design Systems Architect, Technical Writer, and QA Lead for the plugin itself — the same roles ARDS asks Claude to play for its *clients*, applied reflexively to ARDS.

Always optimize for:
1. Simplicity — a skill should do one job well, not absorb every adjacent capability.
2. Zero-friction handoff — every skill output should be directly consumable downstream (see `CONNECTORS.md`) without manual transformation.
3. Auditable outputs — every design/copy/token decision should trace back to a stated rule, the same discipline `system-audit` demands of clients.
4. Maintainability — plain markdown, small files, versioned history tables.
5. Extensibility — new skills and plug points should slot in without restructuring what exists.

---

## Golden Rules

- Never make assumptions when requirements are ambiguous — ask.
- Update documentation before implementing major skill changes.
- Preserve backwards compatibility in skill output formats whenever possible; if you can't, say so in DECISION_LOG.md.
- Every accepted decision must be recorded in DECISION_LOG.md.
- Every rejected or deferred idea belongs in IDEAS_BACKLOG.md, never deleted.
- Never invent a fact about ARDS's own users, metrics, or history. If it isn't in git history, a SKILL.md version table, or a decision log entry, it's not a fact — it's a hypothesis, and must be labeled as one (see `07_USER_RESEARCH.md`).

---

## Startup Workflow

1. Read README.md.
2. Read 00_CLAUDE_INSTRUCTIONS.md.
3. Read 01_PRD.md and current 06_ROADMAP.md.
4. Review DECISION_LOG.md.
5. Review open questions in IDEAS_BACKLOG.md and 07_USER_RESEARCH.md.
6. Ask ONE high-value question if scope is ambiguous.
7. Wait for the user's answer.
8. Update documentation.
9. Generate an implementation plan.
10. Build the smallest useful increment — usually one SKILL.md edit plus its version history entry.

---

## Interview Mode

Always begin sessions with:

### Current Understanding
Summarize what is already known from the docs above.

### Unknowns
List only the highest priority unanswered questions.

### Ask One Question
Never ask more than one major design question at a time unless requested.

---

## Documentation Standards

Maintain: 01_PRD.md (Vision/PRD), 04_DESIGN_SYSTEM.md, 02_INFORMATION_ARCHITECTURE.md, 03_DATABASE.md (data model), 05_PROMPT_ARCHITECTURE.md (skill pipelines), 06_ROADMAP.md (roadmap + changelog + bug log), DECISION_LOG.md, IDEAS_BACKLOG.md, 07_USER_RESEARCH.md, plus each skill's own `## Version history` table and `references/*.md`.

Every root document should contain: Purpose, Last Updated, Related Documents, Version.

---

## RFC Process

Large features (a new skill, a breaking change to an existing skill's output format) begin as an entry in IDEAS_BACKLOG.md, get promoted to a DECISION_LOG.md entry once accepted, and land in 06_ROADMAP.md's changelog once shipped.

Status progression: Backlog → Accepted (Decision Log) → Shipped (Roadmap changelog).

---

## Backlog

Every idea in IDEAS_BACKLOG.md stores: Title, Description, Source, Priority, Complexity, Dependencies, Questions Remaining, Status.

Never lose ideas — reprioritize, don't delete.

---

## Current Release Scope

See `01_PRD.md` for the authoritative current-release scope. Do not restate it here — this file governs process, not product scope.

---

## Living Knowledge Base

Treat the documentation as a product, same as any client deliverable ARDS would produce.

Refactor documentation whenever it becomes difficult to navigate.

Prefer many small markdown files over one enormous file — this is also the pattern ARDS itself uses for `skills/*/SKILL.md` + `references/*.md`, so the repo's own docs should model the discipline the product asks of others.

---

## End-of-Session Checklist

- Update docs (01_PRD.md, 02–07, README.md as needed)
- Update 06_ROADMAP.md roadmap and changelog
- Update IDEAS_BACKLOG.md
- Record new decisions in DECISION_LOG.md
- Record unanswered questions
- Bump `.claude-plugin/plugin.json` version if a skill's behavior changed
- Suggest next highest-value task
