# Token architecture

All design tokens follow the W3C Design Token Community Group (DTCG) format. This document defines the schema, alias conventions, and file structure for this plugin.

## File structure

```
tokens/
├── tokens.web.json       # Web platform tokens
├── tokens.mobile.json    # Mobile platform tokens
└── tokens.base.json      # Shared primitive palette (referenced by both)
```

## DTCG format

Every token is an object with at minimum a `$value` and `$type` field:

```json
{
  "color": {
    "brand": {
      "primary": {
        "$value": "{color.palette.brand.500}",
        "$type": "color"
      }
    }
  }
}
```

**Never use raw values in semantic or component tokens.** All semantic tokens must alias back to a primitive palette token using the `{category.group.name}` syntax.

## Token categories

### color
```json
{
  "color": {
    "palette": {
      "brand": {
        "50":  { "$value": "#f0f4ff", "$type": "color" },
        "100": { "$value": "#e0e9ff", "$type": "color" },
        "200": { "$value": "#c0d4ff", "$type": "color" },
        "300": { "$value": "#91aeff", "$type": "color" },
        "400": { "$value": "#6187ff", "$type": "color" },
        "500": { "$value": "#3d5afe", "$type": "color" },
        "600": { "$value": "#2541e0", "$type": "color" },
        "700": { "$value": "#1a2fb5", "$type": "color" },
        "800": { "$value": "#132190", "$type": "color" },
        "900": { "$value": "#0d1870", "$type": "color" }
      },
      "neutral": {
        "0":   { "$value": "#ffffff", "$type": "color" },
        "50":  { "$value": "#f8f9fa", "$type": "color" },
        "100": { "$value": "#f1f3f5", "$type": "color" },
        "200": { "$value": "#e9ecef", "$type": "color" },
        "300": { "$value": "#dee2e6", "$type": "color" },
        "400": { "$value": "#ced4da", "$type": "color" },
        "500": { "$value": "#adb5bd", "$type": "color" },
        "600": { "$value": "#6c757d", "$type": "color" },
        "700": { "$value": "#495057", "$type": "color" },
        "800": { "$value": "#343a40", "$type": "color" },
        "900": { "$value": "#212529", "$type": "color" },
        "1000": { "$value": "#000000", "$type": "color" }
      }
    },
    "semantic": {
      "success": { "$value": "{color.palette.green.500}", "$type": "color" },
      "warning": { "$value": "{color.palette.amber.500}", "$type": "color" },
      "danger":  { "$value": "{color.palette.red.500}", "$type": "color" },
      "info":    { "$value": "{color.palette.blue.500}", "$type": "color" }
    },
    "brand": {
      "primary":    { "$value": "{color.palette.brand.500}", "$type": "color" },
      "primary-hover": { "$value": "{color.palette.brand.600}", "$type": "color" },
      "secondary":  { "$value": "{color.palette.brand.100}", "$type": "color" },
      "on-primary": { "$value": "{color.palette.neutral.0}", "$type": "color" }
    },
    "surface": {
      "default":   { "$value": "{color.palette.neutral.0}", "$type": "color" },
      "subtle":    { "$value": "{color.palette.neutral.50}", "$type": "color" },
      "raised":    { "$value": "{color.palette.neutral.0}", "$type": "color" },
      "overlay":   { "$value": "{color.palette.neutral.800}", "$type": "color" }
    },
    "text": {
      "primary":   { "$value": "{color.palette.neutral.900}", "$type": "color" },
      "secondary": { "$value": "{color.palette.neutral.600}", "$type": "color" },
      "disabled":  { "$value": "{color.palette.neutral.400}", "$type": "color" },
      "on-dark":   { "$value": "{color.palette.neutral.0}", "$type": "color" }
    },
    "border": {
      "default":   { "$value": "{color.palette.neutral.200}", "$type": "color" },
      "strong":    { "$value": "{color.palette.neutral.400}", "$type": "color" },
      "focus":     { "$value": "{color.palette.brand.500}", "$type": "color" }
    }
  }
}
```

### typography
```json
{
  "typography": {
    "family": {
      "sans":  { "$value": "Inter, system-ui, sans-serif", "$type": "fontFamily" },
      "serif": { "$value": "Playfair Display, Georgia, serif", "$type": "fontFamily" },
      "mono":  { "$value": "JetBrains Mono, monospace", "$type": "fontFamily" }
    },
    "size": {
      "xs":  { "$value": "12", "$type": "dimension" },
      "sm":  { "$value": "14", "$type": "dimension" },
      "md":  { "$value": "16", "$type": "dimension" },
      "lg":  { "$value": "18", "$type": "dimension" },
      "xl":  { "$value": "20", "$type": "dimension" },
      "2xl": { "$value": "24", "$type": "dimension" },
      "3xl": { "$value": "30", "$type": "dimension" },
      "4xl": { "$value": "36", "$type": "dimension" },
      "5xl": { "$value": "48", "$type": "dimension" }
    },
    "weight": {
      "regular": { "$value": "400", "$type": "fontWeight" },
      "medium":  { "$value": "500", "$type": "fontWeight" },
      "semibold":{ "$value": "600", "$type": "fontWeight" },
      "bold":    { "$value": "700", "$type": "fontWeight" }
    },
    "lineHeight": {
      "tight":   { "$value": "1.2", "$type": "number" },
      "snug":    { "$value": "1.375", "$type": "number" },
      "normal":  { "$value": "1.5", "$type": "number" },
      "relaxed": { "$value": "1.625", "$type": "number" },
      "loose":   { "$value": "2", "$type": "number" }
    },
    "letterSpacing": {
      "tight":  { "$value": "-0.025em", "$type": "dimension" },
      "normal": { "$value": "0em", "$type": "dimension" },
      "wide":   { "$value": "0.025em", "$type": "dimension" },
      "wider":  { "$value": "0.05em", "$type": "dimension" },
      "widest": { "$value": "0.1em", "$type": "dimension" }
    }
  }
}
```

### spacing
```json
{
  "spacing": {
    "0":   { "$value": "0", "$type": "dimension" },
    "1":   { "$value": "4", "$type": "dimension" },
    "2":   { "$value": "8", "$type": "dimension" },
    "3":   { "$value": "12", "$type": "dimension" },
    "4":   { "$value": "16", "$type": "dimension" },
    "5":   { "$value": "20", "$type": "dimension" },
    "6":   { "$value": "24", "$type": "dimension" },
    "8":   { "$value": "32", "$type": "dimension" },
    "10":  { "$value": "40", "$type": "dimension" },
    "12":  { "$value": "48", "$type": "dimension" },
    "16":  { "$value": "64", "$type": "dimension" },
    "20":  { "$value": "80", "$type": "dimension" },
    "24":  { "$value": "96", "$type": "dimension" }
  }
}
```

### radius
```json
{
  "radius": {
    "none": { "$value": "0", "$type": "dimension" },
    "sm":   { "$value": "4", "$type": "dimension" },
    "md":   { "$value": "8", "$type": "dimension" },
    "lg":   { "$value": "12", "$type": "dimension" },
    "xl":   { "$value": "16", "$type": "dimension" },
    "2xl":  { "$value": "24", "$type": "dimension" },
    "full": { "$value": "9999", "$type": "dimension" }
  }
}
```

### elevation (shadow)
```json
{
  "elevation": {
    "0": { "$value": "none", "$type": "shadow" },
    "1": { "$value": "0 1px 2px rgba(0,0,0,0.05)", "$type": "shadow" },
    "2": { "$value": "0 2px 4px rgba(0,0,0,0.08)", "$type": "shadow" },
    "3": { "$value": "0 4px 8px rgba(0,0,0,0.1)", "$type": "shadow" },
    "4": { "$value": "0 8px 16px rgba(0,0,0,0.12)", "$type": "shadow" },
    "5": { "$value": "0 16px 32px rgba(0,0,0,0.15)", "$type": "shadow" }
  }
}
```

### motion
```json
{
  "motion": {
    "duration": {
      "instant":  { "$value": "0ms", "$type": "duration" },
      "fast":     { "$value": "100ms", "$type": "duration" },
      "normal":   { "$value": "200ms", "$type": "duration" },
      "slow":     { "$value": "300ms", "$type": "duration" },
      "slower":   { "$value": "500ms", "$type": "duration" }
    },
    "easing": {
      "default":    { "$value": "cubic-bezier(0.4, 0, 0.2, 1)", "$type": "cubicBezier" },
      "in":         { "$value": "cubic-bezier(0.4, 0, 1, 1)", "$type": "cubicBezier" },
      "out":        { "$value": "cubic-bezier(0, 0, 0.2, 1)", "$type": "cubicBezier" },
      "spring":     { "$value": "cubic-bezier(0.34, 1.56, 0.64, 1)", "$type": "cubicBezier" }
    }
  }
}
```

## Dark mode

Dark mode tokens are defined as a separate mode in the token file using DTCG's `$extensions` field or as a parallel token set (depending on toolchain). For Figma variables, dark mode is a second mode within the same variable collection.

Key reversals in dark mode:
- `surface.default` → `{color.palette.neutral.900}`
- `text.primary` → `{color.palette.neutral.50}`
- `border.default` → `{color.palette.neutral.700}`
- Semantic colors shift to lighter palette stops (e.g., `danger` → `{color.palette.red.400}` instead of `500`)

## Alias rules

1. Primitive tokens (palette) contain raw values. These are the only tokens that may contain hex codes, px values, or raw strings.
2. Semantic tokens alias to primitives: `{color.palette.brand.500}`.
3. Component tokens alias to semantic tokens: `{color.brand.primary}`.
4. Never skip a level — a component token must not alias directly to a primitive.
