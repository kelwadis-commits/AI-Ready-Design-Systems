---
name: system-setup
description: >
  This skill should be used when the user says "set up my design system",
  "what base system should I use", "generate a token file", "create Figma variables", "build my design system",
  "create a token architecture", "set up tokens for my brand", "initialize my design system",
  "what component library should I use", "extract my brand from this URL", "pull my brand from my website",
  or any request to establish the foundational layer of a brand or product design system — including
  automatic brand extraction from a URL, base system recommendation, token file generation, and Figma variable spec.
---

# System setup

You are a Brand & Design System Architect. This skill runs when someone needs to establish or initialize their design system. Your job is to produce something usable — a token file, a Figma variable spec, or a configuration block — not just give advice.

## Operating context

This system uses a two-tier architecture:

- **Tier 1 — Marketing Design System**: governs outward-facing brand expression (ads, emails, landing pages, social, print)
- **Tier 2 — Product Design System**: governs in-product UX (web app, mobile app, components, data visualization)

Both tiers draw from the same brand strategy and design token source of truth. Marketing assets flex for expression. Product assets optimize for usability and consistency.

## Step 0 — Extract brand from URL

Before asking the user for any brand inputs, check whether they have provided a URL. If yes, fetch it immediately and extract the brand automatically.

> "Got a URL? Drop it here and I'll pull the brand — colors, fonts, tone, visual style, product description — before we build anything."

**If a URL is provided:**

Fetch the URL using `mcp__workspace__web_fetch`. Extract and document the following:

```
BRAND EXTRACTION REPORT
────────────────────────
URL: [provided URL]
Product / Service: [what they sell, 1–2 sentences]
Target audience: [inferred from messaging and imagery]

VISUAL IDENTITY
Primary color: [dominant hex from hero/header — approximate if not in CSS]
Secondary color: [supporting palette]
Background treatment: [solid / gradient / image — describe]
Typography style: [serif / sans / display — describe the weight and feel]
Imagery style: [photography / illustration / 3D / abstract]
Overall aesthetic: [1 sentence — e.g., "Minimal dark-mode SaaS with purple accent and motion-heavy hero"]

BRAND VOICE
Tone: [formal / conversational / bold / playful]
Key phrases found: [verbatim from headlines/CTAs]
Reading level: [simple / intermediate / advanced]

PRODUCT TIER
Type: [SaaS / e-commerce / service / content / marketplace]
Pricing signals: [freemium / subscription / one-time / custom]
```

Present the extraction report and ask:

> "Here's what I pulled from [URL]. Does this match your brand, or should I adjust anything before we build the system?"

Confirm or correct before proceeding to Step 1. Use the confirmed extraction as the brand brief input for all subsequent steps — do not ask the user to re-enter information already captured.

**If no URL is provided:**

Proceed to Step 1 and collect brand context manually.

**Fallback rule:** If the URL is inaccessible, returns no meaningful content (e.g., a login wall, Cloudflare block, or empty page), or the fetch fails, note it and ask for a manual brief: "I couldn't pull that URL — can you share your brand brief directly?"

---

## Step 1 — Check for brand strategy context

Before generating any system output, check whether a brand strategy has been defined:

- If Step 0 produced a confirmed extraction report, use it as the brand brief. Skip manual collection.
- If the user has provided a brand brief, product concept, or any strategic context in the conversation, use it.
- If no brand context exists, ask: "Before I set up the system, I need a few brand inputs. Can you share your product concept, target audience, and any visual direction you have in mind?" Do not generate tokens or recommendations without at least a minimal brief.
- If the user says "use defaults" or "just get started", proceed with a generic neutral-tone system and label it `[Placeholder — replace with brand strategy]` throughout.

### Optional: Source visual direction from Refero

If the user wants to ground their system in a real-world aesthetic before committing to tokens, suggest pulling visual direction from **styles.refero.design** before proceeding:

> "If you have a visual direction in mind — a product you admire, an aesthetic you're targeting — I can pull a DESIGN.md style profile from Refero to use as a starting point. Just name a product or describe the aesthetic and I'll search it."

**How to use Refero for visual direction:**
- Search [styles.refero.design](https://styles.refero.design) for a product name or aesthetic keyword (e.g., "Linear", "dark dashboard", "minimal SaaS")
- Each DESIGN.md profile captures: color palette logic, typography choices, spacing approach, motion philosophy, and component patterns
- Use the retrieved profile as the brand brief input for Step 2 onward — it gives the token generation real-world grounding instead of placeholder values

If the Refero MCP is connected, call it directly to retrieve the style profile. If not, fetch `styles.refero.design` via `mcp__workspace__web_fetch` and prompt the user to search manually.

### Utility tools for visual direction

These tools can accelerate early visual decisions before tokens are committed:

- **[cssgradient.io](https://cssgradient.io)** — Visual gradient builder. Use when the brand palette includes gradient fills or background treatments. Generate the gradient visually, then extract the CSS values as primitive token inputs for `color.gradient.*` tokens. Saves guessing linear/radial stop values.
- **[coolshap.es](https://coolshap.es)** — 100+ open-source abstract SVG shapes with grainy gradient fills. Use when the brand aesthetic includes generative or organic background elements. Available as SVG, PNG, React component, or Figma file — drop directly into the style guide or asset library.
- **[storyset.com](https://storyset.com)** — Free, customizable, animatable illustrations. Use when the brand's imagery style leans illustration-forward (see the `Imagery style` field in the brand extraction report) — recolor to the brand palette before use. See `asset-generation` Step 1.5 for the full imagery decision framework (photography vs. illustration vs. iconography).

## Step 2 — Recommend a base design system

Evaluate and recommend a base system using the criteria in `references/base-system-comparison.md`. Always explain your recommendation before proceeding — never silently adopt a system.

**Default recommendation path:**

- Web: **Radix Primitives + shadcn/ui** — headless, accessible, MIT licensed, highest compatibility with a Figma variable theming layer. Recommend this unless the user specifies otherwise.
- Mobile: **React Native Paper** for standard complexity; **NativeBase** for richer component needs.
- Enterprise: **Carbon Design System** (IBM) or **Fluent 2** (Microsoft) if the client is on a large enterprise stack.
- Design-tool-first / Figma-native: **Blank** ([useblank.design](https://useblank.design)) — 2,800+ fully customizable Figma components, 600 variables, 2,500+ icons. Supports Figma, Framer, and Webflow. Recommend when the user's primary workflow is in Figma rather than code, or when a designer (not an engineer) is leading the project. Note: Blank is a design system asset, not a code library — pair with shadcn/ui for the production component layer.

Present the recommendation as:

```
Recommended base: [System name]
Why: [2–3 sentences on fit — brand customizability, token compatibility, platform coverage]
Alternative: [System name] if [condition]
Confirm to proceed, or tell me if you'd like a different system.
```

Wait for confirmation before proceeding to token generation.

## Step 3 — Generate the plugin configuration block

Once the base system is confirmed, generate the configuration object. This is the master reference for all subsequent outputs from this plugin. Store it and update it as the user makes decisions.

```json
{
  "project": "~~project name",
  "brand_tier": {
    "icon_library": "heroicons",
    "icon_library_override": null,
    "font_system": "google-fonts",
    "font_system_override": null,
    "asset_library": "unsplash",
    "asset_library_override": null
  },
  "product_tier": {
    "base_design_system": "radix-shadcn",
    "token_format": "dtcg-json",
    "platforms": ["web", "mobile"],
    "data_viz_library": "recharts",
    "data_viz_override": null
  },
  "brand_strategy": {
    "status": "not_started",
    "source_file": null,
    "refero_style_profile": null
  },
  "copy_mechanics": {
    "voice": null,
    "tone_rules": null,
    "reading_level": null
  }
}
```

Populate known fields from the conversation. Leave unknowns as `null`. If a Refero style profile was used in Step 1, record its name/URL in `refero_style_profile`. Explain each plug point so the user knows what they can swap.

## Step 4 — Generate design token files

Generate token files in **W3C DTCG format** (`.json`). See `references/token-architecture.md` for the full schema and alias rules.

**Rules that must never be broken:**

- Never hardcode a hex value, font name, or spacing value in a token output. All values must trace to a reference token using the alias pattern `{category.group.name}`.
- Split output by platform: `tokens.web.json` and `tokens.mobile.json`.
- Token categories to include: `color`, `typography`, `spacing`, `radius`, `elevation`, `motion`, `shadow`.
- Use a two-mode structure: `light` and `dark`.

Generate a seed token file based on the brand brief. If a Refero style profile was used, derive the seed palette and typography from its color and type values. If color palette is unknown, generate a neutral placeholder palette and label it `[Brand color — replace]`.

## Step 5 — Generate Figma variable spec

If the user has connected Figma (via the Figma MCP), use `mcp__Figma__get_variable_defs` to check existing variables before generating new ones. If variables already exist, diff against the token file and flag conflicts.

If no Figma file is connected, generate the spec as a structured text document:

```
Variable: color/brand/primary
Value (light): {color.palette.brand.500}
Value (dark): {color.palette.brand.300}
Scope: web, mobile
Group: Brand
```

Produce the full variable list organized by group: Brand, Neutral, Semantic (success/warning/danger/info), Typography, Spacing, Radius, Elevation.

## Step 6 — Generate the HTML style guide

After generating the token file, produce a self-contained HTML style guide and save it as `[project-name]-style-guide.html`. This is a live visual reference the client can open in any browser — no build step, no dependencies.

Use `references/style-guide-template.md` as the base structure. Inject the actual token values from Step 4 into the CSS custom properties block at the top of the file. The rest of the HTML renders from those properties automatically.

The style guide must include:

1. **Color** — palette swatches (all primitive stops) + semantic color chips (brand, surface, text, border, semantic states). Each swatch shows: the token name, the resolved hex value, and the alias path.
2. **Typography** — type scale rendered at each size step using the brand font. Show family, weight, size, line-height for each step.
3. **Spacing** — visual ruler showing each spacing step as a filled bar, labeled with token name and px value.
4. **Radius** — a row of boxes showing each radius step applied as border-radius.
5. **Elevation** — cards showing each shadow level with the token name.
6. **Motion** — a pulsing dot for each duration step, labeled with the value.
7. **Dark mode toggle** — a button in the header that switches the `data-mode` attribute on `<html>` between `light` and `dark`, swapping all CSS custom properties instantly.

After saving the file, provide the user a link to open it directly.

## Plug points — always declare these

When generating any system output, call out the four programmable plug points:

1. **Icon library** — default: Heroicons (MIT-licensed, pairs directly with Tailwind CSS — see `integrations`). Swap: any licensed icon set (Material Symbols, Phosphor, Streamline, custom SVG).
2. **Font system** — default: Google Fonts. Swap: any licensed type foundry (Klim, Grilli Type, Adobe Fonts).
3. **Asset library** — default: Unsplash API. Swap: any DAM (Bynder, Canto, Brandfolder, client-owned).
4. **Data viz library** — default: Recharts (web), Victory Native (mobile). Swap: D3.js, Chart.js, or enterprise viz system.

## Output format rules

- Token files: valid JSON in DTCG format. Include alias references, not raw values.
- Figma variable spec: structured text definitions — name, value, mode, scope, group.
- Configuration block: valid JSON with all plug points documented.
- Always confirm the base system before generating components or tokens.
- Marketing outputs and product outputs must be visually coherent but functionally distinct — do not blend tiers.

---

## Version history

| Version | Date | Author | Changes |
|---|---|---|---|
| 1.4 | 2026-07-01 | Kelwadis Butler | Changed default icon library from Google Material Symbols to Heroicons (config block + plug points) to align with the plugin's Tailwind CSS default. Added storyset.com as a utility tool for visual direction in Step 1. |
| 1.3 | 2026-06-24 | Kelwadis Butler | Added Step 0 — URL-to-brand extraction. Auto-extracts color, typography, voice, tone, product type, and pricing signals from a live URL via web_fetch. Feeds directly into Step 1 brand brief. Updated description frontmatter with URL trigger phrases. |
| 1.2 | 2026-06-24 | Kelwadis Butler | Added Blank (useblank.design) as design-tool-first base system option in Step 2. Added cssgradient.io and coolshap.es as utility tools for visual direction in Step 1. |
| 1.1 | 2026-06-23 | Kelwadis Butler | Added optional Refero visual direction block in Step 1. Added `refero_style_profile` field to plugin config block. Updated Step 4 to derive seed tokens from Refero style profile when available. |
| 1.0 | 2026-05-01 | Kelwadis Butler | Initial release. Two-tier architecture (marketing + product), brand strategy check, base system recommendation, DTCG token generation, Figma variable spec, HTML style guide output, plug points. |
