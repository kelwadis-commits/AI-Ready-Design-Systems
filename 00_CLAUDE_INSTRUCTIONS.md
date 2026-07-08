# Claude Build Instructions

Purpose: Implementation-partner instructions for whoever (human or AI) is writing or editing content in this repo.
Last Updated: 2026-07-08
Related Documents: CLAUDE_PLAYBOOK_INSTRUCTIONS.md
Version: 0.1

## What this repo actually is

AI-Ready Design Systems (ARDS) is a Claude Code / Claude Cowork **plugin**, not an application. There is no frontend, no backend, no database, and no build step. The entire product is:

- Markdown skill files (`skills/*/SKILL.md`) — these ARE the product logic. A skill's behavior is whatever its SKILL.md says, in plain instructions to Claude.
- Reference files (`skills/*/references/*.md`) — supporting detail a skill loads mid-task (rubrics, schemas, comparison tables).
- A plugin manifest (`.claude-plugin/plugin.json`) — name, version, description, author, keywords.
- An MCP wiring file (`.mcp.json`) — currently wires the Figma MCP.
- Documentation (`README.md`, `CONNECTORS.md`, and this doc set) — describes the product and governs how it's built.

There is nothing to compile, deploy, or run a server for. "Shipping a change" means editing a markdown file, testing it in a live Claude session, and committing.

## Principles

- Documentation-first — every skill change should be reflected in its SKILL.md's `## Version history` table before it's considered done, and root-level docs (this set) kept current.
- Every SKILL.md must produce something usable, not just advice — a token file, a JSON spec, an audit report, a copy block. This is stated explicitly inside several SKILL.md files and applies as a repo-wide rule.
- Never hardcode values that should be tokens. This rule is enforced inside `system-setup`, `token-update`, and `asset-generation` — treat it as a repo-wide constraint on any new skill that touches design output.
- Two-tier separation (Marketing vs. Product) is load-bearing across `system-setup`, `system-audit`, and `README.md`. Do not blur it when adding new skill content.
- Figma is the one wired, required integration (`.mcp.json`). Every other external tool is a documented plug point (see `CONNECTORS.md`) — swappable per client, not hardcoded into a skill's core logic.
- Keep frontmatter (`name`, `description`) trigger phrases exhaustive and current — the `description` field is literally how Claude decides whether to invoke a skill. An undocumented trigger phrase is a missed activation, not a cosmetic gap.
- Maintain a version history table at the bottom of every SKILL.md that has shipped more than once. Increment on any behavioral change, however small.
- Never break an existing skill's documented output format without a version history entry explaining the migration and, if the change is breaking, a note in DECISION_LOG.md.

## Where facts live (don't duplicate, point instead)

- Product vision, personas, and current scope: `01_PRD.md`
- Repo/skill file structure: `02_INFORMATION_ARCHITECTURE.md`
- Token/config data model: `03_DATABASE.md`
- Design principles ARDS enforces in its outputs: `04_DESIGN_SYSTEM.md`
- Real skill pipelines (the actual step-by-step logic): `05_PROMPT_ARCHITECTURE.md`
- What shipped, what's next, changelog, bugs: `06_ROADMAP.md`
- Persona validation status: `07_USER_RESEARCH.md`
- Why we built it this way: `DECISION_LOG.md`
- What we're not building yet: `IDEAS_BACKLOG.md`
- Product-management judgment calls (OKRs, pricing, positioning): `skills/virtual-pm/SKILL.md`
- Launch/GTM execution detail: `skills/launch-playbook/SKILL.md`

If you're about to restate a fact that already lives in one of these, link to it instead.
