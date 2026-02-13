# Logo Maker → Logo-to-Launch Planner & Multilingual UX – Focused Change List v2

_Last updated: 2026-02-13 — Shuri (@product-ux)_

This document narrows in on the **planner + scheduler + multilingual** parts of the Logo Maker logo-to-launch flow and specifies concrete UI behavior that keeps the experience close to:

> Idea → logo → launch assets → **scheduled posts in 5–10 minutes**, including 1–3 extra languages without calendar chaos.

It builds on:
- `/mayagen/reports/logo-maker-landing-ux-v1.md`
- `/mayagen/reports/logo-maker-logo-to-launch-flow-v1.md`
- `/mayagen/reports/logo-maker-logo-to-launch-friction-v1.md`


---
## 1. "Launch Week" Planner Mode (Scoped, Friendly Calendar)

**Goal:** When users arrive from Logo Maker, the planner should feel like a small, safe sandbox for a single launch—not the full, intimidating calendar.

### 1.1 Entry behavior

- Deep link: `/planner?mode=launch-week&brand=BRAND_ID&source=logo-launch`
- Auto-apply filters:
  - View: **Week** (7-day window starting today or next Monday).
  - Brand filter: **current Brand Kit** only.
  - Campaign filter: `Logo launch` (implicit if we don’t have full campaign objects yet).
- Non-essential chrome is minimized or collapsed by default:
  - Hide advanced filters, campaign list, analytics sidebars, etc.
  - Keep only: date range selector, channel toggles, and language toggle.

### 1.2 Visual framing

Top-of-screen banner:
- Title: `Plan your launch week`
- Supporting copy: `We’ve dropped 3–7 launch posts onto this week. Review them, add languages, and schedule in a couple of clicks.`
- Primary CTA: `Schedule launch week`
- Secondary actions (text links): `Adjust times` • `Edit posts`

Right-side **Launch Week checklist**:
- [ ] Review your launch posts
- [ ] Add languages
- [ ] Confirm schedule

Clicking a checklist item:
- Scrolls/focuses the relevant part of the UI (e.g., highlights posts, opens language dialog).
- Marks item as complete when the corresponding key action occurs:
  - Review → user opens at least one post detail/editor.
  - Add languages → user confirms at least one additional language.
  - Confirm schedule → user schedules at least one post.

### 1.3 Default post layout & times

- Pre-generate **3–5 posts** based on the Logo → Brand Kit → Launch Assets spec:
  - Day 1: primary announcement.
  - Day 3–4: story/behind-the-logo.
  - Day 5–7: reminder/promo.
- Suggested send times:
  - Opinionated defaults per channel (e.g., per Growth v2 heuristics).
  - All times editable via drag-and-drop or time picker, but editable controls are secondary to the `Schedule launch week` shortcut.

### 1.4 `Schedule launch week` behavior

When user clicks **Schedule launch week**:
- If some posts are missing times, auto-assign sensible defaults within the current week.
- Transition all draft posts in this "launch week" view to **scheduled**.
- Show inline progress state on the button: `Scheduling…` → `Launch week scheduled`.
- Fire analytics event: `logo_launch_week_scheduled` with:
  - `num_posts`
  - `num_languages`
  - `time_to_first_scheduled_post_ms`


---
## 2. Base Post + Multilingual Variant Model

**Goal:** Let users add 1–3 languages quickly without exploding the calendar into a mess of duplicated tiles.

### 2.1 Data & visual model

- Introduce a **Base Post** entity representing the canonical content for a time slot.
- Each Base Post can have **Language Variants** (EN, HI, ES, etc.).
- In Launch Week mode, **the calendar row/tile represents the Base Post**, not each individual variant.

Visual representation in week view:
- Each Base Post card shows:
  - Thumbnail visual.
  - Short label: `Announcement`, `Behind the logo`, `Reminder`, etc.
  - Channel icons.
  - Language chips row: `EN` (primary) + additional chips for variants: `EN  ·  HI  ·  ES`.
- Interactions:
  - Clicking the card opens the **Base Post editor** with tabs for each language.
  - Clicking a language chip jumps directly to that variant within the editor.

### 2.2 `+ Add language` entry point

Placement:
- Top-right of Launch Week banner row near date range: `+ Add language`.

Behavior:
1. Click opens **Add languages** dialog:
   - Title: `Add languages to your launch`
   - Copy: `We’ll keep your visuals and timing, and adapt the copy for each language.`
   - Control: multi-select of languages with search.
   - Soft limit: primary language + up to **3 additional** in this flow.
   - Microcopy under selector: `You can always add more from the full calendar later.`
2. On confirm:
   - For each Base Post in this Launch Week view, create Language Variants in the selected languages.
   - Pre-fill copy using translation + light localization from the primary language.
   - Mark the checklist item “Add languages” as complete.
   - Emit analytics event: `logo_launch_languages_added` with `num_languages_added`.

### 2.3 Variant review UX

After adding languages, the user should see an obvious next step:

- Show a small nudge toast or inline banner: `Language variants ready – review & tweak copy` with CTA `Review languages`.
- CTA opens a **Language Review modal**:
  - Steps through each Base Post in sequence.
  - For each Base Post, display stacked sections:
    - EN (primary) at top.
    - Each additional language below with side-by-side or stacked textareas.
  - Quick controls:
    - `Approve all` for this post.
    - Per-language `Approve` / `Edit` toggle.
  - Progress indicator: `Post 1 of 4`.

Exit behavior from modal:
- If user clicks `Done`, return to Launch Week calendar with language chips highlighted briefly.


---
## 3. Microcopy & Guardrails for Multilingual Simplicity

**Goal:** Make multilingual feel like a small, optional power-up—not a commitment to manage dozens of posts.

### 3.1 Copy at entry

- `+ Add language` button hover/tooltip:
  - `Reach a few more customers in their language—without duplicating your work.`

- Dialog subheading / helper text:
  - `Start with 1–3 languages. We’ll keep visuals synced and adapt the captions.`

### 3.2 Limits & reassurance

- Enforce maximum of 3 additional languages at selection-time with inline message:
  - `For this guided launch, we recommend up to 3 extra languages. You can add more later from the full calendar.`

- If user attempts to deselect all additional languages after creation, show a gentle confirmation:
  - `Remove extra languages for this launch? You can always add them back from the calendar.`

### 3.3 Error & edge cases

- If translation/localization fails for a specific language:
  - Fallback copy: `We couldn’t adapt this caption automatically. Start from the original text below.`
  - Show EN + empty localized field, with clear label.


---
## 4. Confirmation, Return Paths & Ongoing Launch Management

**Goal:** After scheduling, users should clearly understand what’s live, in which languages, and how to get back to it.

### 4.1 Post-schedule confirmation panel

After `Schedule launch week` succeeds:

- Slide in a right-hand **Launch scheduled** panel (or modal with non-blocking backdrop):
  - Title: `Your logo launch is scheduled`
  - Summary bullets:
    - `Brand: [Brand Name]`
    - `Posts: X` (Base Posts count)
    - `Languages: EN + N others`
    - `Channels: …`
  - Primary CTA: `View launch in planner`
  - Secondary CTA: `Create more launch posts`

- "View launch in planner" behavior:
  - Opens full planner with filters applied:
    - `brand=BRAND_ID`
    - `campaign=logo-launch` (if available)
  - Keeps week view centered around the scheduled window.

### 4.2 Dashboard/home nudge

Add a **Launch card** on workspace/dashboard when a Logo-based launch is upcoming:
- Title: `[Brand Name] launch is scheduled`
- Supporting line: `X posts over Y days across EN + N languages.`
- CTA: `Review launch posts` → same deep link as above.

This card disappears or shrinks after the launch window passes, replaced by:
- `Extend your [Brand Name] launch` CTA that opens planner filtered to the brand with a suggestion to add recurring posts.


---
## 5. Analytics Hooks for Planner + Multilingual

To make the 5–10 minute journey measurable and optimizable, we should at minimum capture:

- `logo_launch_planner_opened` — when Launch Week mode first loads.
  - Props: `brand_id`, `num_draft_posts`.
- `logo_launch_languages_added` — when user confirms added languages.
  - Props: `num_languages_added`.
- `logo_launch_language_review_opened` — when Language Review modal opens.
  - Props: `num_base_posts`, `num_languages`.
- `logo_launch_week_scheduled` — when `Schedule launch week` completes.
  - Props: `num_base_posts`, `num_languages`, `time_to_first_scheduled_post_ms`.
- `logo_launch_launch_card_clicked` — when dashboard launch card CTA is used.

These should be consistent with Analytics v2 naming for other planner/scheduler events.


---
## 6. Impact on North-Star Flow

By scoping planner to a **Launch Week** mode, treating posts as **base posts with grouped language variants**, and adding explicit guidance + confirmation, this spec should:

- Reduce abandonment on the calendar step for Logo Maker users.
- Increase the share of users who:
  - Schedule at least one launch post.
  - Opt into 1–3 additional languages.
- Bring the median **logo → first scheduled post** time into the 5–10 minute window for guided flows.

This keeps the UX promise tight: users start with a logo idea and end, minutes later, with a concrete launch week scheduled in multiple languages—without ever feeling like they’re managing a complex enterprise scheduler.