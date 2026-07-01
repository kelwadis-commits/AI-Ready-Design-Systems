# Alias rules

This document defines the three-tier alias architecture that all token files in this system must follow. These rules are enforced on every token update.

## The three tiers

### Tier 1 — Primitive tokens
Raw values. The only place in the token system where hex codes, pixel values, and raw strings live.

```json
{
  "color": {
    "palette": {
      "brand": {
        "500": { "$value": "#3d5afe", "$type": "color" }
      }
    }
  }
}
```

**Rules:**
- May contain raw values.
- Named by scale (50–900 for colors, or descriptive for non-color).
- Never referenced directly by component or feature code — always through a semantic alias.

---

### Tier 2 — Semantic tokens
Named by purpose, not by appearance. Must alias to a primitive — never contain raw values.

```json
{
  "color": {
    "brand": {
      "primary": { "$value": "{color.palette.brand.500}", "$type": "color" },
      "primary-hover": { "$value": "{color.palette.brand.600}", "$type": "color" }
    },
    "text": {
      "primary": { "$value": "{color.palette.neutral.900}", "$type": "color" },
      "secondary": { "$value": "{color.palette.neutral.600}", "$type": "color" }
    },
    "surface": {
      "default": { "$value": "{color.palette.neutral.0}", "$type": "color" },
      "subtle": { "$value": "{color.palette.neutral.50}", "$type": "color" }
    }
  }
}
```

**Rules:**
- Must alias to a Tier 1 primitive using `{category.group.name}` syntax.
- Named for what the token *means*, not what it looks like. "primary" not "blue". "danger" not "red".
- Changing which primitive a semantic token points to is a semantic-level change (minor version bump).

---

### Tier 3 — Component tokens
Named by component and property. Must alias to a semantic token — never to a primitive.

```json
{
  "component": {
    "button": {
      "primary": {
        "background": { "$value": "{color.brand.primary}", "$type": "color" },
        "background-hover": { "$value": "{color.brand.primary-hover}", "$type": "color" },
        "text": { "$value": "{color.text.on-dark}", "$type": "color" },
        "border-radius": { "$value": "{radius.md}", "$type": "dimension" },
        "padding-x": { "$value": "{spacing.4}", "$type": "dimension" },
        "padding-y": { "$value": "{spacing.2}", "$type": "dimension" }
      }
    }
  }
}
```

**Rules:**
- Must alias to a Tier 2 semantic token. Never skip to Tier 1.
- Named by component, variant, and property: `component.button.primary.background`.
- This tier is where two components can share a semantic value but diverge in their component-level expression.

---

## Alias syntax

DTCG alias syntax uses curly braces and dot notation:

```
{category.group.subgroup.name}
```

Examples:
- `{color.palette.brand.500}` — primitive color
- `{color.brand.primary}` — semantic color
- `{spacing.4}` — spacing primitive
- `{radius.md}` — radius primitive
- `{typography.size.md}` — typography primitive

**Important:** The alias path must exactly match the JSON key structure. A typo in an alias path silently breaks the token — the toolchain will either throw an error or fall through to a default.

---

## Dark mode aliases

Dark mode is expressed as a second mode value on the same token, not as a separate set of tokens. In DTCG, this is done with the `$extensions` field or via a parallel mode structure depending on the toolchain.

When writing dark mode values, always reference a different primitive — not a raw value:

```json
{
  "color": {
    "surface": {
      "default": {
        "$value": "{color.palette.neutral.0}",
        "$type": "color",
        "$extensions": {
          "mode": {
            "dark": "{color.palette.neutral.900}"
          }
        }
      }
    }
  }
}
```

---

## Common alias mistakes to catch and correct

| Mistake | Why it's wrong | Fix |
|---|---|---|
| `"$value": "#3d5afe"` in a semantic token | Raw value in Tier 2 | Alias to `{color.palette.brand.500}` |
| `"$value": "{color.palette.brand.500}"` in a component token | Skipped Tier 2 | Alias to `{color.brand.primary}` |
| `"$value": "{color.brand.primary}"` in a primitive | Aliasing in Tier 1 | Remove alias, use raw value |
| Token renamed in JSON but not updated in Figma | Drift between token file and Figma | Add to Figma update checklist |
| Token deleted without audit | Silent breaks downstream | Always audit dependents before deleting |

---

## Version bump rules

| Change | Version bump |
|---|---|
| Raw value change in primitive | Patch (`0.1.0` → `0.1.1`) |
| Semantic token points to new primitive | Minor (`0.1.0` → `0.2.0`) |
| New token added (any tier) | Patch (`0.1.0` → `0.1.1`) |
| New token category added | Minor |
| Token renamed | Major (`0.1.0` → `1.0.0`) |
| Token deleted | Major |
| Alias structure reorganized | Major |
