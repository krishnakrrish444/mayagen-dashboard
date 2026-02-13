# Logo Maker → Brand Kit → Templates → Scheduled Launch Flow v1

_Last updated: 2026-02-13 — Shuri (@product-ux)_

This spec makes the **“new logo → brand kit → social templates → scheduled launch posts”** flow concrete, with an emphasis on:
- Fast time-to-first-scheduled-post (target: **≤ 30 minutes**, stretch: **5–10 minutes** for a guided path).
- Clear affordances into **planner + scheduler**.
- Simple, visible **multilingual** controls.

It builds on:
- `/mayagen/reports/logo-maker-landing-copy-v1.md`
- `/mayagen/reports/logo-maker-landing-ux-v1.md`

---

## 1. Target Flow (Happy Path)

User goal: "I’m launching a new brand; help me go from no logo to a full week of launch posts."

### 1.1 High-level journey

1. **Landing:** User lands on Logo Designer page.
2. **Create Logo:** User generates and chooses a logo.
3. **Brand Kit:** Guided step to confirm colors, fonts, and usage.
4. **Launch Assets:** System generates a basic launch asset pack.
5. **Calendar:** User drops 3–7 launch posts onto the calendar.
6. **Multilingual:** User adds 1–3 additional languages and reviews variants.
7. **Confirm:** User sees a confirmation panel summarizing what’s scheduled.

Success definition: 
- User ends with **at least 1 scheduled launch post** (ideal: 3–7) and understands that they can come back to this calendar to extend the campaign.

---

## 2. UX Flow Details

### 2.1 Landing → Logo creation

**Entry points**
- Primary CTA: `Design your logo & launch kit` → opens Logo Designer with the **“Launch a new brand”** preset selected.
- Secondary CTA: `See logo-to-launch flow` → scrolls to flow strip and includes a secondary button `Start this flow`.

**Key UX choices**
- Pre-fill industry + brand archetype suggestions to reduce cognitive load.
- Show a small, persistent breadcrumb: `Logo → Brand Kit → Launch Assets → Calendar` at the top of the flow.

### 2.2 Post-logo selection → Brand Kit step

After the user chooses a logo, instead of a generic “download” view, show **Step 2 of 4: Brand Kit**:

- **Headline:** `Turn this into a Brand Kit`
- **Body:** Short paragraph: “We’ll auto-generate your colors, fonts, and usage rules so every meme, mockup, and template stays on-brand.”
- **UI elements:**
  - Preview of logo on 2–3 surfaces (avatar, cover, post mockup).
  - Inline controls to tweak primary color + font pairing (simple, opinionated choices).
- **Primary CTA:** `Save Brand Kit & continue`
- **Secondary CTA:** `Skip for now` (allowed, but triggers a gentle warning about losing automation benefits).

### 2.3 Brand Kit → Launch asset pack

**Step 3 of 4: Launch Assets**

- **Headline:** `Generate your launch assets`
- **Body:** “We’ll create a starter pack for your announcement week—avatars, covers, and core posts.”
- **Defaults:**
  - 1 × profile/avatar image.
  - 1 × cover/header.
  - 3–5 social post templates (announcement, countdown/teaser, "now live").
- **Controls:**
  - Checkboxes to include/exclude certain asset types.
  - Dropdown for primary channels (e.g., Instagram, LinkedIn, X, Facebook).
- **Primary CTA:** `Create assets & open calendar`
- **Secondary CTA:** `Download only` (fallback path, but visually secondary).

On primary CTA, we:
- Generate assets in the background.
- Prepare a **proposed calendar layout** for the next 7 days (see below).

### 2.4 Calendar + Scheduler view

**Step 4 of 4: Plan your launch** (calendar view)

- **Default view:** Week view starting today or next Monday (whichever is closer to now).
- **Pre-filled draft posts:**
  - Day 1: "Announce your new brand" post.
  - Day 3–4: "Behind the logo" / story post.
  - Day 5–7: Promo or reminder posts.
- Each draft:
  - Uses a relevant visual from the launch asset pack.
  - Includes starter copy derived from brand inputs.

**UX elements:**
- Banner at top: `You’re one step away from launching your new brand.`
- Checklist sidebar:
  - [ ] Review posts
  - [ ] Add languages
  - [ ] Confirm schedule
- Primary CTA in banner: `Schedule launch week` (sets all drafts to scheduled at suggested times).
- Alternative interaction: user can drag posts to different days/times before scheduling.

### 2.5 Multilingual controls

Within the calendar step:

- **Language selector pill group** above the calendar: `EN` (active) + `+ Add language`.
- Clicking `+ Add language` opens a dialog:
  - Select 1–3 additional languages.
  - Option: "Copy visuals, adapt copy" (default) vs. "Duplicate posts unchanged".
- On confirm:
  - System creates language variants of each draft post, grouped by base post.
  - User can toggle between language tabs in the side panel to review and edit.

**UX constraints:**
- Keep the number of languages manageable (max 3 extra in this flow) to avoid overwhelming first-time users.
- Highlight that more languages can be added later from the calendar.

### 2.6 Confirmation & next steps

After scheduling:

- Show a confirmation modal or side panel:
  - "You’re all set—your new brand is scheduled to launch." 
  - List of channels + languages covered.
  - Short timeline e.g. "7 posts over 5 days".
- Provide clear next actions:
  - `View full calendar`
  - `Create more launch posts`
  - `Explore memes & mockups using your Brand Kit`

---

## 3. Key Frictions & How This Flow Addresses Them

### 3.1 Users stopping at logo download

**Risk:** Users treat Logo Maker as a one-and-done file export.

**Mitigation in this flow:**
- No standalone “download-only” screen; downloads are available but secondary.
- The primary path is a 4-step wizard that ends on the calendar, not the export.
- CTAs emphasize **Brand Kit** and **Launch assets**, not just "Download logo".

### 3.2 Weak visibility of planner + scheduler

**Risk:** Users don’t realize Mayagen can schedule their launch.

**Mitigation:**
- Breadcrumb and step labels explicitly mention **Calendar** and **Launch**.
- Landing CTAs and copy consistently reference planner + scheduler.
- The final step is literally a calendar, pre-filled with launch posts.

### 3.3 Multilingual complexity

**Risk:** Multilingual feels like an advanced feature or is too complex for first use.

**Mitigation:**
- Simple `+ Add language` entry point with clear copy: "We’ll keep visuals, adapt copy."
- Hard cap on languages in this guided flow to avoid clutter.
- Side-by-side or tabbed review that lets users quickly skim variants.

### 3.4 Cognitive overload for first-time users

**Risk:** Too many knobs and options before they see value.

**Mitigation:**
- Opinionated defaults at each step (logo presets, asset pack contents, suggested calendar layout).
- Single primary action per step, with fewer choices and strong guidance.

---

## 4. Concrete UI/UX Requirements

1. **Wizard skeleton**
   - Reusable 4-step wizard pattern with breadcrumb: `Logo → Brand Kit → Launch Assets → Calendar`.
   - Each step has a prominent primary CTA that moves the user forward.

2. **Brand Kit integration**
   - Saving the Brand Kit from this flow must:
     - Create a Brand Kit entity.
     - Mark it as the default for the current workspace.
     - Propagate it to Meme Generator, Product Mockups, and social templates.

3. **Calendar deep link**
   - The wizard should deep-link into a **filtered calendar view** that only shows the new launch posts for this brand.
   - URL-style requirement (example): `/planner?brand=BRAND_ID&view=week&source=logo-launch`.

4. **Draft vs scheduled states**
   - Pre-filled posts should start as **drafts** with a clear visual state.
   - `Schedule launch week` CTA flips all to **scheduled** and assigns times.

5. **Multilingual variant grouping**
   - Posts in different languages should be grouped so that the user understands they are variants of the same message.
   - E.g., a stack or grouped row per “base post” with language chips.

6. **Analytics hooks** (see also Analytics v2):
   - Track completion of each step in the wizard.
   - Track how many posts are scheduled from this flow.
   - Track how many languages are added in this first session.

---

## 5. Open Questions / Follow-ups

- How opinionated should the default launch-week layout be (e.g., 3 vs 5 vs 7 posts)?
- Do we need different presets for different business types (e.g., SaaS vs local business vs creator)?
- Where else should we surface the "Finish launch setup" nudge if users drop after Step 2 or 3?

---

## 6. Summary

This flow reframes Logo Maker from a **file export tool** to the **first step in a fast, guided launch journey**:

> Logo → Brand Kit → Launch Assets → Calendar (with multilingual variants)

It should materially improve:
- The share of Logo Maker users who create a Brand Kit.
- The share who schedule at least one launch post.
- The median time from **logo created → first scheduled post**, especially for multi-language brands.