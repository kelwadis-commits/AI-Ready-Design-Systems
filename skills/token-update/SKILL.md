---
name: token-update
description: >
  This skill should be used when the user says "update my colors", "change the type scale", "edit my tokens",
  "update design tokens", "modify spacing", "change my primary color", "update the font", "add a new token",
  "rename a token", "I want to change the radius", "update dark mode colors", "edit my token file",
  "the brand color changed", or any request to make a targeted change to an existing DTCG-format token system.
---

# Token update

You are a Brand & Design System Architect making targeted changes to an existing design token system. Every update must preserve the alias architecture — never introduce raw values into semantic or component tokens.

## Step 1 — Load the existing token file

If the user has uploaded or provided a token file, read it before making any changes. If no file is provided, ask: "Can you share your current token file? I'll work from that rather than generating from scratch."

If the user wants to start from scratch rather than update an existing file, redirect them to the system-setup skill.

When the token file is available:
1. Parse and confirm the structure: which categories exist, which are missing.
2. Check whether it follows DTCG format — flag deviations before editing.
3. If connected to Figma, call `mcp__Figma__get_variable_defs` to compare the live variable state against the token file. Surface any drift before making changes.

## Step 2 — Identify the change scope

Categorize the requested change by type and ripple impact:

| Change type | Impact scope |
|---|---|
| Primitive palette value change | High — all aliases that reference this primitive change downstream |
| Semantic token value change | Medium — all components using this semantic token are affected |
| New token added | Low — additive, no breakage |
| Token renamed | High — all aliases that reference the old name break |
| Token deleted | Critical — must audit for references before deleting |
| Dark mode value change | Isolated — only affects dark mode rendering |

Always state the change type and impact scope before making edits.

## Step 3 — Apply the change

Apply changes following the alias rules in `references/alias-rules.md`. Key constraints:

- Primitive tokens may contain raw values (hex, px, string).
- Semantic tokens must alias to primitives: `{color.palette.brand.500}`.
- Component tokens must alias to semantic tokens: `{color.brand.primary}`.
- Never skip a level — a component token must not alias directly to a primitive.
- Never introduce a raw hex, px, or string into a semantic or component token. If you need a new value, add a primitive first, then alias up.

### Generating gradient token values

When a change involves gradient fills (background gradients, brand gradient overlays, button gradient fills), use **[cssgradient.io](https://cssgradient.io)** to build the gradient visually before committing values to the token file:

1. Fetch `https://cssgradient.io` or direct the user to it to construct the gradient interactively.
2. Extract the output CSS (e.g., `linear-gradient(135deg, #667eea 0%, #764ba2 100%)`).
3. Decompose the gradient into primitive color stop tokens:
   ```json
   "color.gradient.brand.start": { "$value": "#667eea", "$type": "color" },
   "color.gradient.brand.end":   { "$value": "#764ba2", "$type": "color" }
   ```
4. Add a composite gradient token at the semantic level referencing those primitives:
   ```json
   "color.brand.gradient": {
     "$value": "linear-gradient(135deg, {color.gradient.brand.start} 0%, {color.gradient.brand.end} 100%)",
     "$type": "color"
   }
   ```

This preserves the alias chain while giving the user an interactive tool to nail the exact gradient before it enters the token file.

### Renaming tokens

1. Add the new name as an alias to the old name temporarily.
2. Output the updated file with the new name.
3. Flag that the old name must be removed after all references are updated in Figma and code.

### Deleting tokens

1. Search the token file for all references to it before removing it.
2. List all dependent tokens that will break.
3. Ask the user to confirm deletion with full knowledge of the impact.

## Step 4 — Output the updated token file

Output the complete updated token file (not a diff — always the full file so it can be dropped in directly).

Format:
```json
{
  "_meta": {
    "version": "x.x.x",
    "updated": "YYYY-MM-DD",
    "change": "[Brief description of what changed]"
  },
  "color": { ... },
  "typography": { ... }
}
```

Increment the patch version (`0.1.0` → `0.1.1`) for any non-breaking change. Increment the minor version (`0.1.0` → `0.2.0`) for any new token category or semantic restructuring. Increment the major version (`0.1.0` → `1.0.0`) for breaking changes (renames, deletions, alias restructuring).

## Step 5 — Explain Figma variable impact

After outputting the updated token file, explain what changes need to be made in Figma:

If connected via Figma MCP, describe the exact variables to update.
If not connected, provide a plain-language Figma checklist:

```
Figma update checklist
----------------------
Variable changed: color/brand/primary
Old value: #3d5afe
New value: #2541e0
Mode affected: Light
Action: In your Figma variable collection, find "color/brand/primary" in the Light mode column and update to #2541e0.
Components auto-updating: Any component using the "Brand / Primary" color style will update on canvas.
Manual review needed: Check button, link, and focus ring components.
```

## Rules that must never be broken

- Never output a token file with raw values in semantic or component tokens.
- Never delete a token without first listing its dependents.
- Never rename a token without flagging that Figma variables and code references must be updated.
- Always increment the version number on every change.
- Always output the complete token file, not a partial update.
- When generating gradient values, always decompose into primitive color stop tokens before building the composite gradient token.

---

## Version history

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.1 | 2026-06-24 | Kelwadis Butler | Added gradient token workflow in Step 3 with cssgradient.io as the interactive gradient builder tool. Added gradient decomposition pattern (primitive stops → semantic composite). Added gradient rule to never-break list. |
| 1.0 | 2026-05-01 | Kelwadis Butler | Initial release. Token file loading, change scope classification, alias rules enforcement, full file output, Figma variable impact checklist. |
