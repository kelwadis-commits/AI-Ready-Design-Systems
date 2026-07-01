# Template catalog

Full library of wireframe options for every template category. Each entry includes 2–4 layout options and the component-to-token mapping for brand injection.

---

## Product / UX templates

### Checkout flow

**OPTION A — Single-page progressive**
Layout: Full-width single column, 375px mobile. Order summary collapsed at top, form fields stack below, sticky CTA at bottom.
Key sections: Progress indicator → Collapsed order summary (expandable) → Delivery details form → Payment method selector → Sticky "Place order" CTA
Best for: Mobile-first, impulse purchases, low cart complexity
Complexity: Medium

**OPTION B — Step-by-step (3-step wizard)**
Layout: Full-width, top progress bar with step labels. One form section visible per step. Back/Next navigation anchored to bottom.
Key sections: Step bar (Delivery / Payment / Review) → Active section content → Back + Next CTAs → Persistent mini order summary in sidebar (desktop) or drawer (mobile)
Best for: High-value purchases, complex shipping options, enterprise checkout
Complexity: High

**OPTION C — Split panel (desktop)**
Layout: Two-column 60/40 split. Left: form fields. Right: sticky order summary with line items, discount input, and total.
Key sections: [Left] Breadcrumb nav → Section headers → Form fields → CTA | [Right] Order summary card → Promo code → Totals breakdown → Security trust badges
Best for: Desktop-first e-commerce, B2B purchasing
Complexity: High

**OPTION D — Guest-first express**
Layout: Full-width single column. Guest vs. account choice presented immediately. Payment options (Apple Pay, Google Pay, card) shown before form fields.
Key sections: Guest / Sign in toggle → Express payment buttons → Divider → Standard form fields → CTA
Best for: High-conversion consumer apps, returning users
Complexity: Low

**Token mapping:**
- Frame background → `color.surface.default`
- Section header text → `color.text.primary` / `typography.size.lg` / `typography.weight.semibold`
- Input border → `color.border.default` (idle), `color.border.focus` (focused), `color.semantic.danger` (error)
- Input background → `color.surface.subtle`
- Helper text → `color.text.secondary` / `typography.size.sm`
- Primary CTA → `color.brand.primary` fill / `color.text.on-dark` text / `radius.lg` / `spacing.4` padding-y
- Secondary CTA → `color.surface.default` fill / `color.brand.primary` text / `color.border.default` stroke
- Progress bar active → `color.brand.primary`
- Progress bar inactive → `color.palette.neutral.200`
- Trust badge text → `color.text.secondary` / `typography.size.xs`

---

### Authentication flow

**OPTION A — Centered card (universal)**
Layout: Full-bleed background (brand color or image). Centered card, 400px wide on desktop / full-width on mobile. Logo at top, form below, footer links at bottom.
Key sections: Logo → Headline + subhead → Email + password fields → Primary CTA → Divider → Social auth → Sign up / Forgot password links
Best for: SaaS apps, consumer products
Complexity: Low

**OPTION B — Split-screen (desktop)**
Layout: Left panel: brand illustration or photography with tagline. Right panel: centered auth form.
Key sections: [Left] Brand image + tagline | [Right] Logo → Form → CTAs → Footer
Best for: Marketing-forward products, design-heavy brands
Complexity: Medium

**OPTION C — Full-page minimal**
Layout: No card. Form fields centered vertically on the page. Logo top-left. Help link top-right.
Key sections: Logo → Headline → Fields → CTA → Sign up link
Best for: Enterprise tools, productivity apps, minimal brands
Complexity: Low

**OPTION D — Progressive disclosure (magic link first)**
Layout: Single email field presented first. After submission: confirmation state with secondary option to use password.
Key sections: Logo → Headline → Email field → "Send magic link" CTA → [Second state] Confirmation message + "Use password instead" link
Best for: Modern consumer apps, email-first auth
Complexity: Medium

**Token mapping:**
- Card background → `color.surface.raised` / `elevation.3` / `radius.xl`
- Page background → `color.surface.subtle`
- Brand panel background → `color.brand.primary`
- Brand panel text → `color.text.on-dark`
- Input fields → same as Checkout mapping above
- Divider → `color.border.default`
- Social auth button → `color.surface.default` / `color.border.default` / `radius.md`

---

### Onboarding flow

**OPTION A — Step-by-step with progress (task-based)**
Layout: Full-screen per step. Large progress indicator at top. Central content area. Back/Next at bottom.
Key sections: Step counter (e.g., "2 of 5") → Illustration or icon → Headline → Subhead → Input or selection → Next CTA → Skip link
Best for: Setup wizards, feature configuration, account personalization
Complexity: Medium

**OPTION B — Checklist (progressive completion)**
Layout: Dashboard-style. Checklist of tasks with completion states. Each item expands inline or routes to a focused sub-screen.
Key sections: Welcome headline → Progress bar (X of Y complete) → Checklist items (icon / title / description / CTA) → "What's next" section
Best for: Products with multiple setup tasks, power users
Complexity: Medium

**OPTION C — Slideshow (value proposition)**
Layout: Full-screen carousel. One value prop per slide. Skip button persistent top-right.
Key sections: [Per slide] Illustration → Headline → Body (≤30 words) → Slide indicators → Next / Skip CTAs
Best for: Consumer apps, first-time brand impression, app store feel
Complexity: Low

**OPTION D — Conversational (single question per screen)**
Layout: Full-screen. One question per view, large type, binary or multi-select answers. Feels like a quiz.
Key sections: Question headline → Answer options (large touch targets) → Back chevron → Progress dots
Best for: Personalization flows, preference collection, high-engagement products
Complexity: Medium

**Token mapping:**
- Step indicator active → `color.brand.primary`
- Step indicator inactive → `color.palette.neutral.200`
- Illustration background → `color.brand.secondary`
- Headline → `typography.size.3xl` / `typography.weight.bold` / `color.text.primary`
- Subhead → `typography.size.lg` / `typography.weight.regular` / `color.text.secondary`
- Answer option card → `color.surface.raised` / `color.border.default` / `radius.lg` / selected: `color.brand.secondary` fill + `color.brand.primary` border
- Skip link → `color.text.secondary` / `typography.size.sm`

---

### Dashboard / Home screen

**OPTION A — Summary cards + activity feed**
Layout: Top greeting bar. Row of 3–4 KPI cards. Full-width activity feed below.
Key sections: Greeting + date → KPI cards row (metric / label / trend) → Section header → Activity feed list → Empty state (if no activity)
Best for: Analytics tools, CRMs, admin panels
Complexity: Medium

**OPTION B — Navigation-forward (sidebar layout)**
Layout: Persistent left sidebar (240px). Top bar with search + user menu. Main content area with widget grid.
Key sections: [Sidebar] Logo → Nav items → User account | [Main] Page title → Filter bar → Widget grid (2–3 columns) → Data table
Best for: Enterprise SaaS, desktop-first products
Complexity: High

**OPTION C — Mobile home screen (card feed)**
Layout: Full-width mobile. Top bar with greeting + avatar. Horizontal scroll for primary actions. Vertical card feed below.
Key sections: Top bar → Quick action row (horizontal scroll) → "For you" section → Card feed → Bottom nav bar
Best for: Consumer mobile apps, fintech, health apps
Complexity: Medium

**OPTION D — Goal / progress dashboard**
Layout: Full-width. Large hero progress ring or bar at top. Supporting metrics below. Recommended actions at bottom.
Key sections: Progress hero (ring + percentage + label) → Supporting stats row → Timeline or history chart → Recommended actions list
Best for: Fitness, finance, learning, habit-tracking apps
Complexity: Medium

**Token mapping:**
- KPI card → `color.surface.raised` / `elevation.2` / `radius.lg`
- KPI metric → `typography.size.3xl` / `typography.weight.bold` / `color.text.primary`
- KPI label → `typography.size.sm` / `color.text.secondary`
- Positive trend → `color.semantic.success`
- Negative trend → `color.semantic.danger`
- Nav item active → `color.brand.primary` text + `color.brand.secondary` background
- Nav item inactive → `color.text.secondary`
- Widget grid gap → `spacing.4`
- Section header → `typography.size.sm` / `typography.weight.semibold` / `color.text.secondary` / letter-spacing wide

---

### Empty states

**OPTION A — Illustration-forward**
Layout: Centered vertically and horizontally. Large illustration above. Headline + subhead below. CTA below that.
Key sections: Illustration (brand-art-directed) → Headline (≤6 words) → Subhead (≤20 words) → Primary CTA → Optional secondary link
Best for: First-use moments, encouraging action
Complexity: Low

**OPTION B — Icon + action (minimal)**
Layout: Centered. Icon (from token icon library). Headline. CTA inline or below.
Key sections: Icon (48px) → Headline → CTA button
Best for: Dense UI, secondary sections, list empty states
Complexity: Low

**OPTION C — Inline empty (no centered layout)**
Layout: In-place within a list or table. Dashed border container. Short message + action.
Key sections: Dashed border container → Icon (optional) → Message → Inline CTA link
Best for: Tables, sidebars, list items, feed areas
Complexity: Low

**OPTION D — Educational empty (with tips)**
Layout: Centered. Headline + body explaining the feature. 2–3 tip cards or a short list below. CTA at bottom.
Key sections: Headline → Intro body → Tip cards (icon / tip title / tip body) → Primary CTA
Best for: Complex features with a learning curve, new users
Complexity: Medium

**Token mapping:**
- Illustration background → `color.brand.secondary`
- Container (Option C) → `color.border.default` (dashed, 1px) / `radius.md`
- Headline → `typography.size.xl` / `typography.weight.semibold` / `color.text.primary`
- Subhead → `typography.size.md` / `color.text.secondary`
- Tip card → `color.surface.raised` / `radius.md` / `elevation.1`
- CTA → same as Checkout primary CTA mapping

---

### Settings / account management

**OPTION A — Grouped list (mobile)**
Layout: Full-width mobile. Section headers above grouped rows. Each row: label left, value or control right.
Key sections: Page title → Section group (header + rows) → Destructive zone (account deletion) at bottom
Best for: Mobile apps, iOS/Android native feel
Complexity: Low

**OPTION B — Sidebar nav + content panel (desktop)**
Layout: Left settings nav (200px). Right content panel with forms per section.
Key sections: [Nav] Settings categories | [Panel] Section title → Form fields → Save CTA
Best for: Desktop SaaS, complex settings
Complexity: Medium

**Token mapping:**
- Row separator → `color.border.default`
- Section header → `color.text.secondary` / `typography.size.xs` / letter-spacing wide / uppercase
- Row label → `color.text.primary` / `typography.size.md`
- Row value/secondary → `color.text.secondary` / `typography.size.md`
- Destructive text → `color.semantic.danger`
- Toggle on → `color.brand.primary`
- Toggle off → `color.palette.neutral.300`

---

## Marketing templates

### Landing page

**OPTION A — Hero + features (SaaS standard)**
Layout: Full-width sections stacked. Large hero with headline, subhead, CTA. Feature grid below. Social proof. Pricing. Footer CTA.
Key sections: Nav → Hero (headline / subhead / CTA pair / hero image or video) → Logos bar → Features (3-column grid) → Testimonials → Pricing table → Final CTA → Footer
Best for: SaaS product launches, lead capture
Complexity: High

**OPTION B — Problem → solution narrative**
Layout: Full-width storytelling. Sections alternate image-left/right with text. Strong visual rhythm.
Key sections: Nav → Hero → "The problem" section → "The solution" section → How it works (numbered) → Social proof → CTA → Footer
Best for: New category products, high-education sales
Complexity: Medium

**OPTION C — Waitlist / launch**
Layout: Single-screen or minimal scroll. Centered, bold. Email capture is the only CTA.
Key sections: Logo → Headline (bold, large) → Subhead (1–2 sentences) → Email input + CTA → Social proof (logos or testimonial count) → Footer
Best for: Pre-launch, beta signups, limited access
Complexity: Low

**Token mapping:**
- Hero background → `color.brand.primary` or `color.surface.default`
- Hero headline → `typography.size.5xl` / `typography.weight.bold` / appropriate on-color text token
- Section alternating bg → `color.surface.default` and `color.surface.subtle`
- Feature icon → `color.brand.primary`
- Feature card → `color.surface.raised` / `radius.lg` / `elevation.1`
- Primary CTA → same as product CTA tokens
- Testimonial card → `color.surface.raised` / `radius.xl` / `elevation.2`

---

### Email campaign

**OPTION A — Announcement**
Layout: Single column, 600px wide. Header logo. Hero image. Headline + body. CTA. Footer.
Key sections: Header (logo) → Hero image → Headline → Body (2–3 short paragraphs) → Primary CTA button → Secondary link → Footer (unsubscribe / address)
Best for: Product launches, feature announcements, company news
Complexity: Low

**OPTION B — Promotional**
Layout: Single column. Hero with offer headline (large, bold). Product grid or feature highlights. CTA. Urgency element (countdown or "limited").
Key sections: Header → Offer hero → Product highlights (2-column grid) → Primary CTA → Urgency note → Footer
Best for: Sales, promotions, seasonal campaigns
Complexity: Medium

**OPTION C — Digest / newsletter**
Layout: Single column. Multiple content blocks separated by dividers. Categorized sections.
Key sections: Header → Intro note → Section 1 (title + excerpt + link) → Divider → Section 2 → ... → Footer
Best for: Weekly digests, roundups, curated content
Complexity: Medium

**Token mapping for email (inline CSS — no external stylesheets):**
- Container max-width: 600px, background: resolved `color.surface.default` hex
- Heading color: resolved `color.text.primary` hex
- Body text color: resolved `color.text.secondary` hex
- CTA button bg: resolved `color.brand.primary` hex
- CTA button text: resolved `color.text.on-dark` hex
- CTA button border-radius: resolved `radius.md` px value
- Footer text: resolved `color.text.secondary` hex, `typography.size.xs` px value

Note: Email templates output as HTML with inline styles, not Figma plugin scripts. Generate a self-contained `.html` file instead.
