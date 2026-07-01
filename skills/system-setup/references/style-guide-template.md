# Style guide HTML template

When generating the style guide, use the structure below. Replace every `/* INJECT: ... */` comment with the actual resolved values from the token file generated in Step 4. The file must be fully self-contained — no external stylesheets, no CDN links, no JavaScript frameworks.

---

## Injection points

Before writing the file, resolve these values from the token file:

| Inject point | Source |
|---|---|
| Brand palette (50–900) | `color.palette.brand.*` |
| Neutral palette (0–1000) | `color.palette.neutral.*` |
| Semantic colors | `color.semantic.*` |
| Surface colors | `color.surface.*` |
| Text colors | `color.text.*` |
| Border colors | `color.border.*` |
| Font families | `typography.family.*` |
| Font sizes | `typography.size.*` |
| Font weights | `typography.weight.*` |
| Line heights | `typography.lineHeight.*` |
| Spacing steps | `spacing.*` |
| Radius steps | `radius.*` |
| Elevation shadows | `elevation.*` |
| Motion durations | `motion.duration.*` |
| Dark mode surface/text/border overrides | dark mode values from token file |

---

## HTML template

```html
<!DOCTYPE html>
<html lang="en" data-mode="light">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>%%PROJECT_NAME%% — Style Guide</title>
<style>

/* ── TOKEN LAYER: LIGHT MODE ───────────────────────────────────── */
/* INJECT: all light-mode token values as CSS custom properties     */
:root, [data-mode="light"] {
  /* Brand palette */
  --color-palette-brand-50:   /* INJECT: color.palette.brand.50 */;
  --color-palette-brand-100:  /* INJECT */;
  --color-palette-brand-200:  /* INJECT */;
  --color-palette-brand-300:  /* INJECT */;
  --color-palette-brand-400:  /* INJECT */;
  --color-palette-brand-500:  /* INJECT */;
  --color-palette-brand-600:  /* INJECT */;
  --color-palette-brand-700:  /* INJECT */;
  --color-palette-brand-800:  /* INJECT */;
  --color-palette-brand-900:  /* INJECT */;

  /* Neutral palette */
  --color-palette-neutral-0:    /* INJECT */;
  --color-palette-neutral-50:   /* INJECT */;
  --color-palette-neutral-100:  /* INJECT */;
  --color-palette-neutral-200:  /* INJECT */;
  --color-palette-neutral-300:  /* INJECT */;
  --color-palette-neutral-400:  /* INJECT */;
  --color-palette-neutral-500:  /* INJECT */;
  --color-palette-neutral-600:  /* INJECT */;
  --color-palette-neutral-700:  /* INJECT */;
  --color-palette-neutral-800:  /* INJECT */;
  --color-palette-neutral-900:  /* INJECT */;
  --color-palette-neutral-1000: /* INJECT */;

  /* Semantic */
  --color-brand-primary:        /* INJECT */;
  --color-brand-primary-hover:  /* INJECT */;
  --color-brand-secondary:      /* INJECT */;
  --color-semantic-success:     /* INJECT */;
  --color-semantic-warning:     /* INJECT */;
  --color-semantic-danger:      /* INJECT */;
  --color-semantic-info:        /* INJECT */;

  /* Surfaces */
  --color-surface-default:      /* INJECT */;
  --color-surface-subtle:       /* INJECT */;
  --color-surface-raised:       /* INJECT */;

  /* Text */
  --color-text-primary:         /* INJECT */;
  --color-text-secondary:       /* INJECT */;
  --color-text-disabled:        /* INJECT */;

  /* Borders */
  --color-border-default:       /* INJECT */;
  --color-border-strong:        /* INJECT */;

  /* Typography */
  --font-sans:    /* INJECT: typography.family.sans */;
  --font-serif:   /* INJECT: typography.family.serif */;
  --font-mono:    /* INJECT: typography.family.mono */;

  --size-xs:  /* INJECT: typography.size.xs */px;
  --size-sm:  /* INJECT */px;
  --size-md:  /* INJECT */px;
  --size-lg:  /* INJECT */px;
  --size-xl:  /* INJECT */px;
  --size-2xl: /* INJECT */px;
  --size-3xl: /* INJECT */px;
  --size-4xl: /* INJECT */px;
  --size-5xl: /* INJECT */px;

  /* Spacing */
  --space-1:  /* INJECT: spacing.1 */px;
  --space-2:  /* INJECT */px;
  --space-3:  /* INJECT */px;
  --space-4:  /* INJECT */px;
  --space-5:  /* INJECT */px;
  --space-6:  /* INJECT */px;
  --space-8:  /* INJECT */px;
  --space-10: /* INJECT */px;
  --space-12: /* INJECT */px;
  --space-16: /* INJECT */px;

  /* Radius */
  --radius-none: 0px;
  --radius-sm:   /* INJECT: radius.sm */px;
  --radius-md:   /* INJECT */px;
  --radius-lg:   /* INJECT */px;
  --radius-xl:   /* INJECT */px;
  --radius-2xl:  /* INJECT */px;
  --radius-full: 9999px;

  /* Elevation */
  --elevation-0: none;
  --elevation-1: /* INJECT: elevation.1 */;
  --elevation-2: /* INJECT */;
  --elevation-3: /* INJECT */;
  --elevation-4: /* INJECT */;
  --elevation-5: /* INJECT */;

  /* Motion */
  --duration-fast:   /* INJECT: motion.duration.fast */;
  --duration-normal: /* INJECT */;
  --duration-slow:   /* INJECT */;
  --easing-default:  /* INJECT: motion.easing.default */;
}

/* ── TOKEN LAYER: DARK MODE ────────────────────────────────────── */
/* INJECT: dark mode overrides — only values that change           */
[data-mode="dark"] {
  --color-surface-default:  /* INJECT: dark surface.default */;
  --color-surface-subtle:   /* INJECT */;
  --color-surface-raised:   /* INJECT */;
  --color-text-primary:     /* INJECT */;
  --color-text-secondary:   /* INJECT */;
  --color-text-disabled:    /* INJECT */;
  --color-border-default:   /* INJECT */;
  --color-border-strong:    /* INJECT */;
}

/* ── BASE STYLES ───────────────────────────────────────────────── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: var(--font-sans);
  font-size: var(--size-md);
  color: var(--color-text-primary);
  background: var(--color-surface-subtle);
  line-height: 1.6;
  transition: background var(--duration-normal) var(--easing-default),
              color var(--duration-normal) var(--easing-default);
}

/* Header */
.sg-header {
  background: var(--color-surface-raised);
  border-bottom: 1px solid var(--color-border-default);
  padding: 20px 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 10;
  box-shadow: var(--elevation-1);
}
.sg-header h1 { font-size: var(--size-xl); font-weight: 600; }
.sg-header .sg-meta { font-size: var(--size-sm); color: var(--color-text-secondary); }
.sg-toggle {
  background: var(--color-surface-subtle);
  border: 1px solid var(--color-border-default);
  border-radius: var(--radius-full);
  padding: 6px 16px;
  font-size: var(--size-sm);
  font-family: var(--font-sans);
  color: var(--color-text-primary);
  cursor: pointer;
  transition: background var(--duration-fast), border-color var(--duration-fast);
}
.sg-toggle:hover { border-color: var(--color-border-strong); }

/* Layout */
.sg-content { max-width: 1100px; margin: 0 auto; padding: 48px 40px; }
.sg-section { margin-bottom: 64px; }
.sg-section-title {
  font-size: var(--size-xs);
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--color-text-secondary);
  margin-bottom: 24px;
  padding-bottom: 12px;
  border-bottom: 1px solid var(--color-border-default);
}

/* ── COLOR SECTION ─────────────────────────────────────────────── */
.sg-palette { display: flex; gap: 4px; margin-bottom: 32px; border-radius: var(--radius-lg); overflow: hidden; }
.sg-swatch {
  flex: 1;
  height: 80px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: 8px 6px 6px;
  position: relative;
}
.sg-swatch-label { font-size: 10px; font-weight: 600; opacity: 0.8; }
.sg-swatch-value { font-size: 9px; opacity: 0.7; font-family: var(--font-mono, monospace); }
.sg-palette-name {
  font-size: var(--size-sm);
  font-weight: 500;
  color: var(--color-text-secondary);
  margin-bottom: 8px;
}

.sg-semantic-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 12px; }
.sg-semantic-chip {
  border-radius: var(--radius-md);
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}
.sg-semantic-chip .name { font-size: var(--size-xs); font-weight: 600; }
.sg-semantic-chip .alias { font-size: 10px; font-family: var(--font-mono, monospace); opacity: 0.75; }

/* ── TYPOGRAPHY SECTION ────────────────────────────────────────── */
.sg-type-row {
  display: flex;
  align-items: baseline;
  gap: 24px;
  padding: 16px 0;
  border-bottom: 1px solid var(--color-border-default);
}
.sg-type-meta { width: 200px; flex-shrink: 0; }
.sg-type-meta .token-name { font-size: var(--size-xs); color: var(--color-text-secondary); font-family: var(--font-mono, monospace); }
.sg-type-meta .token-value { font-size: var(--size-xs); color: var(--color-text-secondary); }
.sg-type-sample { flex: 1; }

/* ── SPACING SECTION ───────────────────────────────────────────── */
.sg-spacing-rows { display: flex; flex-direction: column; gap: 12px; }
.sg-space-row { display: flex; align-items: center; gap: 16px; }
.sg-space-bar { background: var(--color-brand-primary); height: 24px; border-radius: var(--radius-sm); transition: width var(--duration-normal); }
.sg-space-label { font-size: var(--size-xs); font-family: var(--font-mono, monospace); color: var(--color-text-secondary); min-width: 120px; }

/* ── RADIUS SECTION ────────────────────────────────────────────── */
.sg-radius-grid { display: flex; gap: 24px; flex-wrap: wrap; align-items: flex-end; }
.sg-radius-box {
  width: 80px;
  height: 80px;
  background: var(--color-brand-secondary);
  border: 2px solid var(--color-brand-primary);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 4px;
}
.sg-radius-box .name { font-size: 10px; font-weight: 600; color: var(--color-text-primary); }
.sg-radius-box .value { font-size: 9px; font-family: var(--font-mono, monospace); color: var(--color-text-secondary); }

/* ── ELEVATION SECTION ─────────────────────────────────────────── */
.sg-elevation-grid { display: flex; gap: 32px; flex-wrap: wrap; align-items: flex-end; }
.sg-elevation-card {
  width: 120px;
  height: 80px;
  background: var(--color-surface-raised);
  border-radius: var(--radius-lg);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 4px;
}
.sg-elevation-card .name { font-size: 10px; font-weight: 600; }
.sg-elevation-card .value { font-size: 9px; font-family: var(--font-mono, monospace); color: var(--color-text-secondary); }

/* ── MOTION SECTION ────────────────────────────────────────────── */
.sg-motion-grid { display: flex; gap: 48px; flex-wrap: wrap; }
.sg-motion-item { display: flex; flex-direction: column; align-items: center; gap: 12px; }
.sg-motion-dot {
  width: 16px;
  height: 16px;
  background: var(--color-brand-primary);
  border-radius: var(--radius-full);
  animation: pulse 2s var(--easing-default) infinite;
}
@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.6); opacity: 0.5; }
}
.sg-motion-label { font-size: var(--size-xs); color: var(--color-text-secondary); text-align: center; }
.sg-motion-label .token { display: block; font-family: var(--font-mono, monospace); }

</style>
</head>
<body>

<header class="sg-header">
  <div>
    <h1>%%PROJECT_NAME%%</h1>
    <div class="sg-meta">Style guide · v%%VERSION%% · Generated %%DATE%%</div>
  </div>
  <button class="sg-toggle" onclick="document.documentElement.dataset.mode = document.documentElement.dataset.mode === 'dark' ? 'light' : 'dark'">
    Toggle dark mode
  </button>
</header>

<main class="sg-content">

  <!-- ── COLOR ─────────────────────────────────────────────────── -->
  <section class="sg-section">
    <div class="sg-section-title">Color</div>

    <!-- Brand palette: INJECT all swatches -->
    <div class="sg-palette-name">Brand palette</div>
    <div class="sg-palette">
      <!-- INJECT: one .sg-swatch per brand palette stop, background-color = resolved hex -->
      <!-- Example swatch (replicate for each stop): -->
      <!--
      <div class="sg-swatch" style="background: var(--color-palette-brand-500); color: #fff;">
        <div class="sg-swatch-label">500</div>
        <div class="sg-swatch-value">#3d5afe</div>
      </div>
      -->
    </div>

    <!-- Neutral palette: INJECT all swatches -->
    <div class="sg-palette-name" style="margin-top: 24px;">Neutral palette</div>
    <div class="sg-palette">
      <!-- INJECT: one .sg-swatch per neutral palette stop -->
    </div>

    <!-- Semantic chips: INJECT one per semantic token -->
    <div class="sg-palette-name" style="margin-top: 32px;">Semantic & brand</div>
    <div class="sg-semantic-grid">
      <!-- INJECT: one .sg-semantic-chip per semantic color -->
      <!-- Example:
      <div class="sg-semantic-chip" style="background: var(--color-brand-primary); color: #fff;">
        <div class="name">brand.primary</div>
        <div class="alias">{color.palette.brand.500}</div>
      </div>
      -->
    </div>
  </section>

  <!-- ── TYPOGRAPHY ─────────────────────────────────────────────── -->
  <section class="sg-section">
    <div class="sg-section-title">Typography</div>
    <!-- INJECT: one .sg-type-row per type size step -->
    <!-- Example row:
    <div class="sg-type-row">
      <div class="sg-type-meta">
        <div class="token-name">typography.size.5xl</div>
        <div class="token-value">48px / 400 / 1.2</div>
      </div>
      <div class="sg-type-sample" style="font-size: var(--size-5xl); line-height: 1.2;">
        The quick brown fox
      </div>
    </div>
    -->
  </section>

  <!-- ── SPACING ────────────────────────────────────────────────── -->
  <section class="sg-section">
    <div class="sg-section-title">Spacing</div>
    <div class="sg-spacing-rows">
      <!-- INJECT: one .sg-space-row per spacing step -->
      <!-- Example:
      <div class="sg-space-row">
        <div class="sg-space-label">spacing.4 — 16px</div>
        <div class="sg-space-bar" style="width: 16px;"></div>
      </div>
      -->
    </div>
  </section>

  <!-- ── RADIUS ─────────────────────────────────────────────────── -->
  <section class="sg-section">
    <div class="sg-section-title">Border radius</div>
    <div class="sg-radius-grid">
      <!-- INJECT: one .sg-radius-box per radius step -->
      <!-- Example:
      <div class="sg-radius-box" style="border-radius: var(--radius-md);">
        <div class="name">md</div>
        <div class="value">8px</div>
      </div>
      -->
    </div>
  </section>

  <!-- ── ELEVATION ──────────────────────────────────────────────── -->
  <section class="sg-section">
    <div class="sg-section-title">Elevation</div>
    <div class="sg-elevation-grid">
      <!-- INJECT: one .sg-elevation-card per elevation step -->
      <!-- Example:
      <div class="sg-elevation-card" style="box-shadow: var(--elevation-3);">
        <div class="name">elevation.3</div>
        <div class="value">0 4px 8px ...</div>
      </div>
      -->
    </div>
  </section>

  <!-- ── MOTION ─────────────────────────────────────────────────── -->
  <section class="sg-section">
    <div class="sg-section-title">Motion</div>
    <div class="sg-motion-grid">
      <!-- INJECT: one .sg-motion-item per duration step -->
      <!-- Example:
      <div class="sg-motion-item">
        <div class="sg-motion-dot" style="animation-duration: var(--duration-fast);"></div>
        <div class="sg-motion-label">
          <span class="token">motion.duration.fast</span>
          100ms
        </div>
      </div>
      -->
    </div>
  </section>

</main>
</body>
</html>
```

---

## Injection checklist

Before saving the file, verify:

- [ ] All `/* INJECT */` comments replaced with actual values from the token file
- [ ] `%%PROJECT_NAME%%` replaced with the project name
- [ ] `%%VERSION%%` replaced with the token file version
- [ ] `%%DATE%%` replaced with today's date
- [ ] Dark mode overrides populated in `[data-mode="dark"]` block
- [ ] At least one swatch per palette stop in the color section
- [ ] At least one row per size step in the typography section
- [ ] Spacing bars use actual pixel widths (not just the CSS variable) so the ruler is accurate
- [ ] File is fully self-contained — no external resource calls
