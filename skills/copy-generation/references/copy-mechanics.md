# Copy mechanics reference

This document defines structural rules and a full catalog of copy types for the copy-generation skill. All rules are defaults — override with brand-specific rules when available.

## Default mechanic rules

| Rule | Default | Override when |
|---|---|---|
| Reading level | Grade 8 or below | Never go above grade 10 for UI |
| Sentence length | ≤20 words for UI copy | ≤30 words for email body |
| Person | Second ("You", "Your") | Third person for formal/legal |
| Contractions | Allowed | Formal register: remove |
| Capitalization | Sentence case | Brand guideline specifies otherwise |
| Voice | Active | Passive only when flagged |
| Exclamation points | ≤1 per block, celebratory only | Never in error or destructive |
| Numbers | Spell out 1–9; numeral 10+ | Measurements always numeral |
| Ellipsis in UI | Avoid — signals incompleteness | Loading states only |
| Ampersands | Avoid in prose; OK in nav labels | Use "and" in sentences |

## Copy type catalog

### Empty states

Used when a list, feed, or dashboard has no content yet.

**Structure:**
- Illustration or icon (out of scope for copy — flag for design)
- Headline: What this space is for (≤6 words)
- Subhead: What the user can do to fill it (≤20 words)
- CTA: Primary action (≤4 words)

**Tone:** Encouraging — possibility-oriented, never apologetic.

**Do:** "Your projects live here. Start your first one to see it take shape."
**Don't:** "No projects found." / "Nothing here yet."

---

### Error messages — form validation

Triggered by incorrect or incomplete field input.

**Structure:**
- Inline, beneath the field
- ≤15 words
- State what's wrong + what to do (not just what's wrong)

**Tone:** Reassuring — factual, never blaming.

**Do:** "That email doesn't look right — check for typos and try again."
**Don't:** "Invalid email." / "You entered an incorrect email address."

---

### Error messages — system errors (500, timeouts)

Triggered by server errors or unexpected failures.

**Structure:**
- Headline: Acknowledge the problem (≤8 words)
- Subhead: What the user can do (≤20 words)
- CTA: Recovery action

**Tone:** Reassuring — take ownership, give a path forward.

**Do:** "Something went wrong on our end. Try refreshing — if it keeps happening, we're on it."
**Don't:** "Error 500." / "An unexpected error occurred."

---

### 404 pages

**Structure:**
- Headline: Acknowledge the miss with brand voice
- Subhead: Offer a useful next step
- CTA: Return to a known good place

**Tone:** On-voice with light personality — not funny if brand is serious, not dry if brand is warm.

---

### Confirmation dialogs — destructive

Used before irreversible actions (delete, remove, cancel subscription).

**Structure:**
- Title: State the action, not a question (≤6 words)
- Body: State the exact consequence (≤30 words)
- Primary CTA: Confirm the action (≤4 words, matches the title verb)
- Secondary CTA: Cancel (≤2 words)

**Tone:** Serious — clear, no softening, no humor.

**Do:**
- Title: "Delete this project"
- Body: "This will permanently remove the project and all its files. You can't undo this."
- Primary: "Delete project"
- Secondary: "Cancel"

**Don't:** "Are you sure?" / "This action cannot be undone." (too generic)

---

### Confirmation dialogs — non-destructive

Used to confirm a significant but reversible action.

**Structure:**
- Title: State what's about to happen
- Body: Brief context (≤20 words, optional if action is self-evident)
- Primary CTA: Confirm
- Secondary CTA: Cancel

**Tone:** On-voice — concise, no alarm.

---

### CTAs and button labels

**Rules:**
- Verb-first: "Save changes" not "Changes saved"
- ≤4 words
- Sentence case
- Specific over generic: "Start free trial" not "Get started"
- Primary and secondary CTAs must be visually and verbally distinct

**Common mistakes to correct:**
- "Submit" → use the specific action ("Send message", "Save preferences", "Complete order")
- "Click here" → never
- "Learn more" alone → "Learn more about [feature]" or replace with a specific CTA

---

### Onboarding copy

Used across a multi-step welcome or setup flow.

**Structure per step:**
- Step label: Short verb phrase ("Connect your tools", "Set your preferences")
- Headline: The benefit of this step (not the task)
- Subhead: Brief context or permission framing (≤25 words)
- CTA: Advance the flow

**Tone:** Inviting — curious, low-pressure, forward-looking.

**Do:** "Connect your calendar. We'll surface the right context at the right time."
**Don't:** "Step 2 of 4: Calendar integration. Please authorize access to your Google Calendar."

---

### Push notifications

**Rules:**
- ≤60 characters for title (iOS truncates at ~50)
- ≤110 characters for body
- Lead with the value, not the feature name
- Personalize with `{{first_name}}` or `{{item_name}}` tokens when available

**Tone:** On-voice, energizing. Never alarmist unless genuinely urgent.

---

### In-app notifications / toasts

**Rules:**
- ≤80 characters total (title + message)
- Success toasts: celebratory but brief
- Error toasts: reassuring + action if possible
- No exclamation points on error toasts

**Format:**
- Success: "[Action] complete." or "[Thing] [past-tense verb]." (e.g., "Changes saved.")
- Error: "Couldn't [action]. [Recovery hint]." (e.g., "Couldn't save changes. Check your connection.")
- Info: Neutral statement of fact.

---

### Transactional email

**Structure:**
- Subject: ≤50 characters. Lead with the most important fact. Avoid clickbait.
- Preview text: ≤90 characters. Extend the subject, don't repeat it.
- H1: Mirrors the subject's intent, slightly expanded
- Body: Short paragraphs (≤3 sentences each). Active voice. The user's next action goes first.
- CTA: One primary action. Make it specific.

**Tone:** Professional on-voice. Transactional emails set expectations — they are not the place for heavy personality.

---

### Tooltips and helper text

**Rules:**
- Tooltips: ≤60 characters. Explain what, not why.
- Helper text: ≤80 characters. Explain constraints or format (e.g., "Must be at least 8 characters with one number").
- Never restate the field label in helper text.

---

## Voice adaptation guide

When brand voice is defined, adapt all defaults using this mapping:

| Brand voice trait | Mechanic adjustment |
|---|---|
| Playful / witty | Contractions always on; light wordplay allowed in empty states and success states |
| Formal / authoritative | Remove contractions; third person where appropriate; longer sentences allowed |
| Warm / empathetic | Lean into second person; error messages more conversational; apologies are OK |
| Bold / direct | Shorter than default (≤15 words for UI); imperative first-word construction |
| Technical / expert | Can use domain terms; reading level up to grade 10; precision over simplicity |
