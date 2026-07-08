# Information Architecture

Purpose: Defines the file/skill structure of the ARDS plugin.
Last Updated: 2026-07-08
Related Documents: 01_PRD.md, 03_DATABASE.md, DECISION_LOG.md
Version: 0.5

## Repo structure (verified against the actual filesystem, 2026-07-08)

```
ai-ready-design-systems/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── system-setup/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── base-system-comparison.md
│   │       ├── style-guide-template.md
│   │       └── token-architecture.md
│   ├── copy-generation/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── copy-mechanics.md
│   ├── token-update/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── alias-rules.md
│   ├── system-audit/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── audit-rubric.md
│   ├── asset-generation/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── figma-plugin-generator.md
│   │       └── template-catalog.md
│   ├── integrations/
│   │   └── SKILL.md
│   ├── launch-playbook/
│   │   └── SKILL.md
│   └── virtual-pm/
│       └── SKILL.md
├── .mcp.json
├── .gitignore
├── CONNECTORS.md
├── README.md
└── [this doc set: 00–07, CLAUDE_PLAYBOOK_INSTRUCTIONS.md, DECISION_LOG.md, IDEAS_BACKLOG.md]
```

**Correction made 2026-07-08:** README.md's "File structure" section previously listed only 4 of the 8 shipped skills (`system-setup`, `copy-generation`, `token-update`, `system-audit`) and omitted `asset-generation`, `integrations`, `launch-playbook`, and `virtual-pm` — all of which exist on disk and are documented elsewhere in the same README (the "Skills" section lists 5; `virtual-pm`, `integrations`, and `launch-playbook` weren't listed there either, despite existing). README.md has been updated to match what's actually on disk.

## Skill routing (how a skill gets invoked)

There is no central router file. Each `skills/*/SKILL.md` has YAML frontmatter (`name`, `description`) — the `description` field is an exhaustive list of trigger phrases and intents. Claude matches the user's request against these descriptions to decide which skill to invoke. This means the frontmatter `description` block is a functional part of the IA, not documentation — see `00_CLAUDE_INSTRUCTIONS.md`.

## Two-tier content split (cuts across the file structure)

The plugin's product-facing IA isn't the file tree above — it's the two-tier model every skill operates inside:

- **Tier 1 — Marketing Design System**: ads, emails, landing pages, social, print
- **Tier 2 — Product Design System**: web app, mobile app, component library, data visualization

Both tiers read from one client configuration block and one token file (see `03_DATABASE.md`). `system-audit` explicitly checks for tier-boundary violations (a marketing pattern appearing in a product component, or vice versa) as one of its audit layers.

## Reference file pattern

`references/*.md` files are loaded by their parent skill mid-task, not by the user directly. They hold content that would bloat SKILL.md if inlined: comparison tables (`base-system-comparison.md`), schemas (`token-architecture.md`, `alias-rules.md`), rubrics (`audit-rubric.md`), catalogs (`template-catalog.md`, `copy-mechanics.md`), and templates (`style-guide-template.md`). Three skills currently have no `references/` folder — `integrations`, `launch-playbook`, `virtual-pm` — because their content is self-contained within SKILL.md and doesn't need mid-task lookup tables.

## Status

This is a structural map, not a content spec — for what's actually inside each reference file's schema, see `03_DATABASE.md` (data model) and `05_PROMPT_ARCHITECTURE.md` (skill pipelines).
