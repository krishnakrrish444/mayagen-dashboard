# Logo Maker → Logo to Launch 5-Minute Path (v1)

Goal: Make it realistically possible for a first-time user to go from **idea → logo → scheduled launch posts** in ~5 minutes, without feeling rushed or overwhelmed.

This builds on:
- `/mayagen/reports/logo-maker-logo-to-launch-flow-v1.md`
- `/mayagen/reports/logo-maker-logo-to-launch-friction-v1.md`
- `/mayagen/reports/logo-maker-logo-to-launch-planner-multilingual-ux-v2.md`
- `/mayagen/reports/logo-maker-logo-to-launch-microcopy-v1.md`

The focus here is **time-boxing, reducing choices, and clarifying the “on-rails” happy path**.

---

## 1. Time Budget & Step Targets

Target total: **≤ 5 minutes** from landing hero click to first launch post scheduled.

Recommended step budgets (for a calm but fast experience):

1. **Pick a starting point (landing → logo flow)** — ~30–45 seconds
   - User clicks a single primary CTA: **“Design your logo & launch kit”**.
   - Land inside a **pre-filtered logo template gallery** (industry guesses or generic defaults) with search but no hard requirement to use it.
   - Show a short helper line: _“Pick a template or start blank — you can change everything later.”_

2. **Edit logo basics** — ~90 seconds
   - Required fields: **brand name** (mandatory), **tagline** (optional), **primary color** (optional smart default from template).
   - Everything else (fine typography, spacing, alternates) is **advanced** and can be skipped initially.
   - Clear progress indicator: _“Step 1 of 4 — Logo basics (about 1 minute)”_.

3. **Confirm Brand Kit** — ~60 seconds
   - Auto-generate a minimal Brand Kit: logo variations, color palette, typography suggestion.
   - Show a compact summary card: _“We’ve started your Brand Kit. You can refine later.”_
   - Primary CTA: **“Continue to launch assets”**; secondary: “Download logo only” (small, de-emphasized).

4. **Launch Assets (posts & templates)** — ~60–90 seconds
   - Preselect **one launch pack**: e.g., 3–5 social posts (hero announcement, about-the-brand, behind-the-scenes/values).
   - Let users deselect posts but **don’t require** adding more.
   - Primary CTA: **“Schedule launch week”**; secondary: “Edit posts first”.

5. **Launch Week planner (calendar)** — ~60–90 seconds
   - Enter simplified **Launch Week mode** scoped to 7 days.
   - Show pre-filled posts on sensible default days/times (which users may adjust but don’t have to).
   - Clear progress indicator: _“Step 4 of 4 — Schedule launch (about 1 minute)”_.
   - Primary CTA: **“Schedule launch week”** which accepts defaults.

---

## 2. On-Rails Happy Path (Minimal Decisions)

For the 5-minute path, the user should be able to:

1. Click **one hero CTA** on the Logo Maker landing:
   - _“Design a logo and schedule your launch”_.

2. Accept smart defaults in each step:
   - **Logo step**: Pick first suggested template, type brand name, press Next.
   - **Brand Kit**: Review summary briefly, press Next.
   - **Assets**: Keep the preselected launch pack, press Next.
   - **Planner**: Glance at the 7-day view, press **“Schedule launch week”**.

3. Skip advanced editing entirely on first run:
   - Advanced logo tweaks, extra brand kit items, additional templates, multi-week campaigns, and extra languages stay discoverable but **out of the main eye-line**.

Design rule: **no more than 2 meaningful decisions per step** in the happy path.

---

## 3. Concrete UX Changes to Support This

### 3.1 Landing Page → Flow Entry

**Problems today (typical patterns):**
- Too many CTAs ("Design a logo", "Browse templates", "See examples", etc.).
- Marketing page talks about features but doesn’t show the end state (scheduled launch).

**Changes:**
- Make a single, dominant CTA above the fold:
  - **Primary:** “Design your logo & schedule launch week”
  - **Secondary:** “Just design a logo” (link-style, below the fold or in nav).
- Above the fold, show a **3-step visual strip** (with time hints):
  1. **Logo** — "1 min: Pick a starting logo"
  2. **Brand Kit & posts** — "2 min: Auto-generate launch posts"
  3. **Launch Week** — "2 min: Schedule your launch"
- Explicitly mention the 5-minute promise in subcopy: _“Go from first logo to scheduled launch posts in about 5 minutes.”_

### 3.2 Logo Editor Step

**Changes:**
- Show a **compact side panel** with just 3 required controls on first run:
  - Brand name (text input)
  - Optional tagline
  - Color theme (pre-selected from template, with 2–3 easy swatches)
- Hide advanced options (spacing, alternates, intricate layout) behind an expandable _“More design options”_ section.
- Keep **undo**, **redo**, and a simple _“Reset to starting design”_ action always visible.
- Primary CTA: **“Next: Brand Kit”** with a small _“~1 minute”_ hint.

### 3.3 Brand Kit Step

**Changes:**
- Present a **read-only summary** on first run:
  - Main logo, light/dark variations, colors, type suggestions.
- Tiny note: _“You can refine this later from Brand Kit – don’t worry about perfection now.”_
- Primary CTA: **“Continue to launch posts”**.
- Secondary CTA: “Download logo only” (smaller, ghost button).
- Add a subtle safeguard: confirmation modal if user picks **“Download logo only”**, with copy like: _“You’re skipping launch posts and calendar scheduling for now. You can always come back to set up Launch Week later.”_

### 3.4 Launch Assets Step

**Changes:**
- Show a **single recommended pack** by default, e.g.:
  - Launch announcement
  - About the brand
  - Behind the scenes/values
  - Optional teaser/reminder
- The pack appears as a short list with checkboxes, all preselected.
- Let users **preview** each post in a right panel without requiring edits.
- Primary CTA: **“Next: Schedule launch week”**.
- Secondary: “Edit text & design first” opens a more advanced editor for power users.

### 3.5 Launch Week Planner (Calendar)

**Changes:**
- Open a **scoped 7-day calendar** titled “Launch Week”.
- Pre-fill posts on default days/times (configurable by system, not user).
- Show a compact checklist in the side panel:
  1. Review posts
  2. (Optional) Add 1–3 extra languages
  3. Schedule launch week
- Make the primary CTA **“Schedule launch week”** visible at all times.
- After clicking, show a brief confirmation state:
  - _“Launch week scheduled! Your logo, brand kit, and first posts are live in your calendar.”_
  - CTAs: “View launch week”, “Tweak posts later”.

---

## 4. Multilingual: Keep It a Small Upgrade

To preserve the 5-minute path while still supporting 100+ languages:

- In the planner step, show a **single, optional control**:
  - `+ Add languages (optional)`
- When clicked, open a small dialog with:
  - Recommended local languages (based on region) plus global English.
  - Soft limit: **up to 3 extra languages** for the first launch.
- Group variants under each base post in the planner, so the calendar doesn’t explode.
- Copy framing: _“Reach a few more audiences with 1–3 extra languages. We’ll group them together so your calendar stays tidy.”_
- If the user skips this, don’t nag; treat it as a future optimization, not a requirement.

---

## 5. Analytics & Success Definition (First Pass)

For this specific 5-minute path, success metrics should include:

- **Time-to-first-scheduled-launch-post** from first Logo Maker landing view.
- **Completion rate** of the 4-step wizard on first run.
- % of users who:
  - Start from the suite-first CTA vs. “Just design a logo”.
  - Reach the planner step but don’t click “Schedule launch week”.
  - Add 1–3 extra languages.

Event examples (names to align with Analytics v2):

- `logo_to_launch_flow_started_from_landing`
- `logo_to_launch_step_completed` (with `step = logo|brand_kit|assets|planner`)
- `launch_week_scheduled_from_logo_maker` (with duration, number of posts)
- `launch_week_multilingual_enabled_from_logo_maker` (with count of languages)

These metrics should be broken down by **entry surface** (landing hero vs. in-app re-entry) and by **time buckets** (≤5 minutes, 5–10 minutes, >10 minutes) to validate whether the 5-minute promise holds in practice.

---

## 6. Summary

This spec trims the Logo Maker logo-to-launch flow down to:
- **One obvious starting CTA.**
- **Four short steps with clear time expectations.**
- **Defaults that are “good enough” for a first launch.**
- **Multilingual as a small, optional upgrade** rather than a second project.

Implementation priority should be:
1. Flow skeleton (4 steps, CTAs, scoped Launch Week mode) with current assets.
2. Time-boxed defaults and checklists.
3. Multilingual as a grouped, optional layer.
4. Analytics wiring to confirm most users can indeed get from idea → logo → scheduled launch in ~5 minutes.