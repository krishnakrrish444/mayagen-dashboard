# Logo Maker → Logo-to-Launch Flow — Microcopy v1

Owner: @content-lead  
Date: 2026-02-13

Focus: keep the suite spine explicit (**create → plan → schedule**) and make 100+ languages feel like an easy reach upgrade, not a requirement. This doc provides implementation-ready strings for the Logo Maker landing page and the in-product logo-to-launch wizard (Logo → Brand Kit → Launch Assets → Calendar / Launch Week).

---
## 1. Landing Page Microcopy

### 1.1 Hero
- **H1:** Design a logo that’s ready to launch your brand
- **Subhead:** Create a logo, build your brand kit, and schedule launch posts across your channels — all inside Mayagen.
- **Primary CTA (new users):** Design your logo & launch kit
- **Secondary CTA (returning users):** Open my brand workspace

Support line for multilingual section:
- **Multilingual teaser:** Launch your brand in 1–3 extra languages without duplicating your calendar.

### 1.2 Flow Strip (Logo → Brand kit → Templates → Scheduler)
Label the 4-step strip directly under the hero:

1. **Create** — "Design a logo that actually looks like your brand."
2. **Prepare** — "Turn it into a reusable brand kit and templates."
3. **Plan** — "Drop launch posts into a simple Launch Week calendar."
4. **Schedule** — "Publish across channels — once per post, with language variants grouped."

CTA below the strip:
- **Button:** See the logo-to-launch flow
- **Helper text:** "From first logo to first scheduled launch in about 10 minutes."

### 1.3 Multilingual Branding Section
- **Section heading:** Launch in more than one language — without more chaos
- **Body copy:**
  > Start in your main language, then add 1–3 more with a single **+ Add language** step. Mayagen keeps variants grouped under one launch so your calendar stays readable.

- **Bullets:**
  - "Create one base launch plan, not four separate calendars."
  - "Translate only the posts that matter most."
  - "See each language as a variant of the same launch — not a new project."

---
## 2. In-Product Wizard Microcopy

### 2.1 Wizard Shell
- **Wizard name:** Logo to Launch
- **Stepper labels:**
  1. Logo
  2. Brand kit
  3. Launch assets
  4. Launch Week

- **Stepper helper text (top of panel):**
  > A guided path from your first logo to a scheduled launch in about 10 minutes.

- **Exit confirmation when user tries to quit mid‑flow:**
  - **Title:** Leave the logo-to-launch flow?
  - **Body:** You can come back from the Logo Maker or Brand Kit pages. Your progress so far will be saved.
  - **Primary:** Save & exit
  - **Secondary:** Stay in flow

### 2.2 Step 1 — Logo
- **Panel header:** Design your logo
- **Helper text:**
  > Pick a style, colors, and layouts. We’ll carry your choices into your brand kit and launch assets.

- **Primary CTA (next):** Continue to brand kit
- **Secondary:** Save logo & exit

- **Empty-state hint (no logo yet):**
  > Not sure where to start? Use a preset and tweak it. You can always change your logo before launch.

### 2.3 Step 2 — Brand Kit
- **Panel header:** Turn your logo into a brand kit
- **Helper text:**
  > We’ll create colors, fonts, and basic layouts so every meme, mockup, and post looks like the same brand.

- **Key toggle label:** Use this brand kit for my launch week
- **Toggle helper text:**
  > Recommended. Your launch posts will automatically use these colors, fonts, and logo.

- **Primary CTA:** Continue to launch assets
- **Secondary:** Back to logo

### 2.4 Step 3 — Launch Assets
- **Panel header:** Create ready-to-post launch assets
- **Helper text:**
  > Generate a small set of launch visuals — logos on backgrounds, product or app mockups, and announcement graphics.

- **Checklist labels:**
  - "At least one announcement graphic"
  - "One product or app visual"
  - "One square logo lockup for avatars"

- **Hint under checklist:**
  > You don’t need a full library. Three to five strong assets are enough for launch week.

- **Primary CTA:** Continue to Launch Week
- **Secondary:** Back to brand kit

### 2.5 Step 4 — Launch Week (Planner + Scheduler)
- **Panel header:** Plan your launch week
- **Helper text:**
  > Drop 3–7 posts into a simple calendar and we’ll handle the schedule.

- **Calendar mode name:** Launch Week
- **Calendar description:**
  > A focused view of your first launch: one brand, one campaign, one week.

- **Primary CTA (once minimum posts placed):** Schedule launch week
- **Disabled CTA label (before minimum met):** Add at least 3 posts to schedule your launch

- **Checklist on the side:**
  1. "Review posts for your main language"
  2. "(Optional) Add 1–3 extra languages"
  3. "Confirm schedule & go live"

- **Post-schedule confirmation modal:**
  - **Title:** Your launch week is scheduled
  - **Body:**
    > We’ve saved this as a campaign in your planner. You can still adjust times, copy, or languages before posts go live.
  - **Primary CTA:** View launch in planner
  - **Secondary CTA:** Close

---
## 3. Multilingual Controls (Logo-to-Launch Flow)

### 3.1 Language Picker
- **Label:** Languages
- **Base-state text:** 1 language selected
- **Add-language button:** + Add language

- **Add-language dialog title:** Add launch languages
- **Dialog helper:**
  > Start with your main language, then add 1–3 more for extra reach. We’ll keep variants grouped under each post.

- **Soft limit warning (if >3 selected):**
  > For your first launch, we recommend up to 3 extra languages so your calendar stays easy to manage.

### 3.2 Language Review Modal (before scheduling)
- **Title:** Review languages before you schedule
- **Body copy:**
  > Each post will have grouped versions per language. You’ll see them as one launch item in the calendar, not four separate posts.

- **Bullets:**
  - "Main language is required for every post."
  - "Extra languages are optional and can be removed later."
  - "Edits stay in sync per post group, so you don’t have to hunt them down."

- **Primary CTA:** Looks good — continue
- **Secondary CTA:** Back to edits

---
## 4. Planner States & Empty States

### 4.1 Launch Week Empty State (before any posts)
- **Title:** Start your launch with 3–7 posts
- **Body:**
  > Drag posts from the left into your Launch Week calendar. Focus on announcements, benefits, and one clear next step.

- **Hint:**
  > You can always add more posts later. The goal now is to make sure your first launch actually happens.

### 4.2 Launch Week Filled-State Banner
- **Banner title:** Ready when you are
- **Banner body:**
  > You’ve planned enough posts for launch week. Review times and languages, then hit **Schedule launch week**.

---
## 5. Email & Notification Snippets

### 5.1 Welcome Email Snippet (Logo Maker Path)
- **Subject idea:** Your new logo is only step one
- **Body snippet:**
  > With Mayagen, your logo is the start of a full launch — not just a file to download. Use the **Logo to Launch** flow to build your brand kit, generate launch assets, and schedule your first week of posts in a few minutes.

### 5.2 Nudge Email Snippet (Stopped after logo export)
- **Subject idea:** Turn your logo into a real launch this week
- **Body snippet:**
  > You already did the hard part — you designed a logo. Next, let Mayagen help you plan and schedule a simple launch week: 3–7 posts, one brand, optional extra languages. Start where you left off and we’ll guide you through the rest.

---

This doc should be treated as the source of truth for Logo Maker + logo-to-launch microcopy. As UX and flows evolve, update strings here first, then sync to Figma and implementation.
