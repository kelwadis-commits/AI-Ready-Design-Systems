# Audit rubric

This document defines the audit layers, checks, and severity rules for the system-audit skill.

---

## Layer 1 — Token compliance

Checks whether visual properties in a design map to the correct tokens in the token system, with no raw values hardcoded outside the primitive tier.

### Checks

**Color**
- Is every color value referenced from `color.brand.*`, `color.semantic.*`, `color.text.*`, `color.surface.*`, or `color.border.*`?
- Are there any hardcoded hex values that don't match any primitive token? → Critical
- Is the correct mode (light/dark) applied given the context? → High if wrong
- Are semantic colors used correctly? (e.g., `color.semantic.danger` only for error/destructive, not decorative) → Medium

**Typography**
- Are font families from `typography.family.*`? → High if hardcoded
- Are font sizes from `typography.size.*`? → Medium if arbitrary
- Are font weights from `typography.weight.*`? → Medium if arbitrary
- Are line heights from `typography.lineHeight.*`? → Low if arbitrary

**Spacing**
- Are spacing values from `spacing.*`? → Medium if arbitrary pixel values used
- Is spacing consistent within a component (no mixed scale usage)? → Low

**Radius**
- Are border radii from `radius.*`? → Medium if arbitrary
- Is radius consistent within a component? → Low

**Elevation / shadow**
- Are shadows from `elevation.*`? → Medium if arbitrary
- Is elevation consistent with component hierarchy? → Low

**Motion**
- Are durations from `motion.duration.*`? → Low
- Are easings from `motion.easing.*`? → Low

---

## Layer 2 — Tier separation

Checks whether the asset is in the correct tier (marketing vs. product) and whether elements from the wrong tier have leaked in.

### Marketing tier (Tier 1) characteristics
- Expressive typography: display sizes, mixed weights, editorial composition
- Brand photography or illustration as primary visual
- Flexible grid — asymmetric, editorial layouts are expected
- Animation and motion for engagement
- Color: full brand palette, including expressive accent colors

### Product tier (Tier 2) characteristics
- Functional typography: UI sizes, consistent weight hierarchy
- Icons and data as primary visual
- 8pt/4pt grid — structured, predictable
- Motion: purposeful micro-interactions only
- Color: semantic colors dominate; brand accents used sparingly for key moments

### Checks
- Does a product component use display-scale editorial typography? → High (Tier 1 leak)
- Does a marketing asset use a UI component (e.g., a button from the component library)? → Medium (note: design system buttons in email are sometimes intentional — flag for review, not automatic failure)
- Is brand photography used as a background in a data table or form? → High
- Are expressive animations used in a functional flow (e.g., a loading state with brand motion)? → Medium

---

## Layer 3 — Voice and tone (copy audits)

Checks whether copy conforms to the brand voice, tone register for context, and copy mechanic rules.

### Voice checks
- Does the copy sound like the brand? Evaluate against the defined voice descriptor.
- Is the person consistent (second person default)? → Medium if inconsistent
- Are contractions used or avoided consistently per brand rule? → Low

### Tone register checks
- Is the tone register appropriate for the context? (See copy-mechanics.md for the register map)
- Does an error message blame the user? → Critical
- Does a destructive confirmation dialog state the exact consequence? → Critical if not
- Is humor used in an error or destructive context? → High
- Is the empty state apologetic instead of possibility-oriented? → Medium

### Mechanics checks
- Are sentences over 20 words in UI copy? → Medium
- Is reading level above grade 8? → High for consumer products, Medium for B2B
- Is ALL CAPS used for emphasis? → High
- Are more than one exclamation points used in a single copy block? → Medium
- Is the CTA generic ("Submit", "Click here", "Learn more")? → High
- Is sentence case used throughout? → Medium if Title Case

---

## Layer 4 — Brand narrative consistency (marketing copy and visual audits)

Checks whether marketing assets reflect the correct positioning, messaging hierarchy, and visual narrative from the brand strategy.

### Checks
- Does the headline reflect the brand's primary value proposition? → High if off-message
- Is the imagery selection consistent with the art direction brief? → High if misaligned
- Are the messaging pillars reflected in the copy? → Medium if absent
- Is the visual hierarchy consistent with the brand's aesthetic intent? → Medium
- Does the asset introduce new brand claims not in the approved messaging? → Critical (legal/brand risk)

---

## Severity definitions

| Severity | Definition | Urgency |
|---|---|---|
| Critical | Breaks the brand promise, introduces legal/brand risk, or compromises token system integrity | Block from shipping |
| High | Noticeable inconsistency that a client or end user could detect | Fix this sprint |
| Medium | Minor drift from system standards; cumulative effect is harmful | Fix in next polish pass |
| Low | Stylistic preference or edge case; no user-facing impact | Flag for team awareness |

---

## Audit pass/fail criteria

| Status | Condition |
|---|---|
| Clean | Zero Critical, zero High findings |
| Needs attention | Zero Critical, one or more High findings |
| Blocked from shipping | One or more Critical findings |
