# Meme → Planner → Scheduler Flow Spec v1

**URL:** `/meme-generator/`
**Owner:** @seo-growth  
**Related docs:**
- SEO/structure: `/mayagen/reports/meme-generator-landing-seo-structure-v1.md`
- Copy v2: `/mayagen/reports/meme-generator-landing-copy-v2.md`
- Growth v2: `/mayagen/reports/growth-strategy-v2.md`

## 1. Funnel Overview

**Goal:** Make the path from first meme → first scheduled post obvious, fast, and repeatable.

Target milestones:
1. Visitor lands on `/meme-generator/` and creates at least one meme (no signup).
2. They click **"Use in social post"** instead of (or in addition to) Download.
3. They schedule that meme as a post inside Mayagen.
4. They see it appear in the planner/scheduler and are nudged to add 2–3 more posts.

The landing page should:
- Visually and verbally highlight **"Use in social post"** as the *default* next step.
- Show how memes live inside a **weekly planner/calendar**, not just a downloads folder.
- Make 100+ languages and Nano Banana Pro feel like an *optional power‑up* for campaigns.

---

## 2. In‑Tool Flow (After Meme Creation)

### 2.1 Primary CTAs After Generation

Once a meme is generated:
- **Primary CTA:** `Use in social post`
- **Secondary CTA:** `Download` (with watermark for free tier)

Microcopy:
- Under **Use in social post**: `Turn this into a ready‑to‑schedule post.`
- Under **Download**: `Save image only` (smaller, de‑emphasized).

Behavior:
- Clicking **Use in social post** opens a right‑hand **Post Composer Panel** without leaving the page.

### 2.2 Post Composer Panel

Fields (minimum viable):
- **Channel selector** (chips): Instagram, Facebook, LinkedIn, X, TikTok, "Other".
- **Caption** textarea with AI suggestion prefilled.
- **Hashtags** suggestions row (optional v1).
- **Publish time**:
  - Radio: `Post now` / `Schedule`.
  - If `Schedule`: date + time picker.

Actions:
- Primary button: **Schedule post**
- Secondary link: **Post now** (if they choose immediate publish instead of scheduled time).
- Tertiary: **Save as draft** (nice‑to‑have).

Copy near the bottom:
> This post will appear in your Mayagen content calendar. You can move it, duplicate it, or localize it into 100+ languages later.

Edge behavior:
- If user is **not signed in**:
  - Let them complete the form.
  - Clicking **Schedule post** triggers lightweight signup modal **after** they’ve invested effort.
  - Modal copy: `Create a free Mayagen account to save this schedule and see your calendar.`

---

## 3. Planner & Scheduler Integration

### 3.1 Post‑Schedule Confirmation State

After a successful schedule:
- Show a small confirmation panel on the meme page:

> **Your meme is on the calendar.**  
> View it in your weekly planner, or add a few more posts so your channel doesn’t go quiet.

Buttons:
- **View in planner** (primary) → opens `/social-media-scheduler/` or in‑app planner route, scrolled to that date.
- **Add another post** (secondary) → takes them back to composer with:
  - Same meme preselected but option to change channel/time.
  - OR opens a generic post composer with the meme already attached.

### 3.2 Planner View Expectations

When they land in planner from this flow:
- The scheduled meme post should be visually highlighted (e.g., pulsing outline, tooltip).
- A helper tooltip / coachmark explains:

> This is your first scheduled meme. Drag it to reschedule, or click it to duplicate across channels.

- Show + button near surrounding days with copy like:

> "Fill the week: add 2–3 more posts around this meme."

This directly supports the **weekly habit** goal from Growth v2.

---

## 4. Landing Page Sections That Reinforce the Flow

The core H2 sections already exist in copy v2. This spec clarifies how each one should make the meme → planner → scheduler flow explicit.

### 4.1 Hero (Above the Fold)

- Visual: meme editor on the left; right side shows a mini weekly calendar with the same meme tile already placed.
- Overlay copy near the calendar: `Scheduled for Tuesday, 7:30 PM`.
- Under main CTA button, add a small line:

> From first meme to scheduled campaign in a few clicks.

### 4.2 H2: Turn Your Meme Into a Social Post (In One Click)

- Include a **3‑step diagram**:
  1. `Create meme` → 2. `Use in social post` → 3. `Schedule in calendar`.
- Each step gets a short caption:
  - Create meme: `Pick a template, write your joke.`
  - Use in social post: `Open the composer with your meme attached.`
  - Schedule in calendar: `Choose a time and see it in your planner.`
- Add a micro‑FAQ snippet in this section:

> **Do I need an account to schedule?**  
> No signup needed to create memes. You’ll create a free account when you’re ready to save your schedule.

### 4.3 H2: Plan Meme Campaigns, Not One‑Off Posts

- Show a **calendar screenshot** with:
  - 2–3 meme posts.
  - 2–3 non‑meme posts (product, launch, announcement).
- Add a short narrative line:

> Start with a single meme today. By the time you leave this page, you can have a full week of posts planned.

- CTA: **Open in planner** → deep‑link to planner with a starter weekly template loaded.

### 4.4 H2: Memes in 100+ Languages With Nano Banana Pro

- Emphasize optionality:

> Optional: turn one meme into a multilingual campaign.

- Flow notes:
  - From planner, user can click a meme post → `Localize`.
  - Modal lets them pick languages and preview localized captions.
  - Localized posts inherit the same time slot or staggered schedule by default.

### 4.5 H2: Examples of Meme‑Led Campaigns

For each example card, include a **mini flow line** under the description:
- `Meme → Use in social post → Planner → Scheduled campaign`.

If a demo planner is available, link CTA as:
- **View this campaign in the calendar →** `/social-media-scheduler?demo=meme-b2b` (or similar route).

---

## 5. Analytics & Measurement Hooks

To validate this flow, instrument at least:
- `meme_created` (with source = `landing` vs. `in-app`).
- `cta_use_in_social_post_clicked`.
- `post_scheduled_from_meme` (with channel and time bucket).
- `planner_opened_from_meme_flow`.
- `additional_posts_created_after_meme` (count within 24h of first schedule).

North‑star style checks:
- % of `/meme-generator/` visitors who create a meme.
- % of meme creators who click **Use in social post**.
- % of those who complete at least one scheduled post.
- % who add 2+ additional posts within same session or 24h.

---

## 6. Implementation Notes

- Keep the meme creation experience **ungated**; push authentication to the moment of saving/scheduling.
- Make "Use in social post" keyboard‑reachable and visually dominant.
- Ensure planner/scheduler views opened from this flow load fast and highlight the newly created post so users immediately see the value.

**Status:**
- v1 funnel spec drafted by @seo-growth.
- This covers the "Add clear flow from meme creation into planner/scheduler" subtask at the UX/funnel level. Remaining work: design/engineering implementation and alignment with @content-lead & @product-ux on visuals and routing.
