# Base design system comparison

Use this reference when evaluating and recommending a base design system. Score each option against the criteria and present the recommendation with reasoning.

## Evaluation criteria

| Criterion | Weight | Description |
|---|---|---|
| Brand customizability | High | Is the system headless/unstyled? Can tokens fully override it? |
| Figma variable compatibility | High | Does the component structure map cleanly to Figma variable theming? |
| Token system compatibility | High | Does it support or expect a DTCG-format token layer? |
| Web + mobile coverage | Medium | Does one system cover both platforms, or do you need two? |
| Community and longevity | Medium | Active maintenance, contributor base, stability |
| License | High | MIT preferred. Avoid GPL or proprietary for commercial white-label use. |

## Systems

### Radix Primitives + shadcn/ui
- **Customizability**: Headless. Zero default styles. Brand applies 100% of visual direction.
- **Figma compatibility**: Excellent. shadcn/ui has an active Figma community kit that maps to Radix primitives.
- **Token compatibility**: Native CSS custom property system maps directly to DTCG tokens.
- **Coverage**: Web only. Pair with React Native Paper or NativeBase for mobile.
- **License**: MIT.
- **Best for**: Any brand that needs full visual control and is building on React.
- **Recommendation**: Default choice for web.

### Material Design 3 (MUI)
- **Customizability**: Styled by default. Theming is robust but fights against heavy brand overrides.
- **Figma compatibility**: Official Figma kit available. Variable support is good but opinionated.
- **Token compatibility**: Material tokens are well-documented but use Google's naming conventions, not DTCG.
- **Coverage**: Web (MUI) and mobile (Jetpack Compose / Material You on Android).
- **License**: MIT (MUI), Apache 2.0 (Material spec).
- **Best for**: Brands that are Google-ecosystem aligned or want a pre-built visual language.
- **Recommendation**: Use when speed matters more than visual differentiation.

### Carbon Design System (IBM)
- **Customizability**: Styled with a robust theming layer. Supports multiple brand themes.
- **Figma compatibility**: Excellent. IBM maintains an official, actively updated Figma library.
- **Token compatibility**: Carbon uses its own token system; DTCG mapping requires an adapter layer.
- **Coverage**: Web only (React, vanilla JS).
- **License**: Apache 2.0.
- **Best for**: Enterprise products, data-heavy dashboards, B2B SaaS.
- **Recommendation**: Use for enterprise clients with complex data UI requirements.

### Fluent 2 (Microsoft)
- **Customizability**: Highly styled. Best when building on top of Microsoft's visual language.
- **Figma compatibility**: Official Figma kit. Very good token mapping.
- **Token compatibility**: Uses JSON tokens; DTCG-compatible with minor adaptation.
- **Coverage**: Web and React Native (Fluent UI React Native).
- **License**: MIT.
- **Best for**: Microsoft 365 integrations, enterprise tools aligned with the Microsoft ecosystem.
- **Recommendation**: Use only when client is deeply Microsoft-embedded.

### React Native Paper
- **Customizability**: Material-based but easily overridable with a theme object.
- **Figma compatibility**: Community kits available; not as polished as web-first systems.
- **Token compatibility**: Accepts a flat theme object; map DTCG tokens via a build script.
- **Coverage**: Mobile only (React Native).
- **License**: MIT.
- **Best for**: Standard mobile apps with moderate UI complexity.
- **Recommendation**: Default mobile pairing with Radix + shadcn/ui on web.

### NativeBase
- **Customizability**: Utility-first, highly customizable via theme config.
- **Figma compatibility**: Community kits; variable support requires manual mapping.
- **Token compatibility**: Theme object accepts a structured token format; DTCG bridge needed.
- **Coverage**: Mobile only (React Native), with Expo support.
- **License**: MIT.
- **Best for**: Mobile apps with complex component needs, Expo-based projects.
- **Recommendation**: Use over React Native Paper when mobile UI complexity is high.

## Decision matrix

| User need | Recommended system |
|---|---|
| Full brand control, web, React | Radix + shadcn/ui |
| Full brand control, web + mobile | Radix + shadcn/ui (web) + React Native Paper (mobile) |
| Speed over differentiation | Material Design 3 (MUI) |
| Enterprise / data-heavy B2B | Carbon Design System |
| Microsoft ecosystem | Fluent 2 |
| Complex mobile UI | NativeBase |
