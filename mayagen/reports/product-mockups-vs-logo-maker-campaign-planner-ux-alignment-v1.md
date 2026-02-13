# Product Mockups vs Logo Maker — Campaign Planner & Multilingual UX Alignment v1

**Author:** @product-ux  
**Date:** 2026-02-13  
**Scope:** Align planner + scheduler UX for campaign-style flows that start in **Product Mockups** (Campaign Mode) and **Logo Maker** (Launch Week / logo-to-launch), so that "idea → graphic → scheduled posts in ~5–10 minutes" feels consistent and learn-once across tools.

---

## 1. Shared Mental Model

Across both entry points, the planner/scheduler should teach a single, consistent mental model:

1. **You are in a short guided flow, not the full planner.**
   - First-run header: clearly labeled step and expected time.
   - Mini-stepper: `1. Create` → `2. Assets` → `3. Schedule` (labels may vary, structure should not).

2. **You are confirming a small, pre-built plan.**
   - Opinionated defaults: 3–7 days worth of posts prefilled.
   - One **campaign-level primary CTA**: `Schedule this campaign` / `Schedule launch week`.

3. **Multilingual is a small, optional reach upgrade.**
   - Base-post + grouped language variants (never rows of duplicated posts).
   - Single `+ Add language` entry point with a soft 1–3 language recommendation.

If a user learns this model in Logo Maker, Campaign Mode from Product Mockups should “feel the same,” and vice versa.

---

## 2. First-Run Header & Stepper (Alignment)

### 2.1 Header copy pattern

- **Logo Maker / Launch Week**
  - Title: **"Schedule your launch week"**
  - Subtitle: **"You’re on step 3 of 3 — review and schedule your launch posts. ~2 minutes."**

- **Product Mockups / Campaign Mode**
  - Title: **"Schedule your Product Mockups campaign"**
  - Subtitle: **"You’re on step 3 of 3 — review and schedule these posts. ~2 minutes."**

Both should:
- Include `step 3 of 3` language.
- Include a time expectation ("~2 minutes" or "~5 minutes"; pick one global standard).
- Show a campaign/launch name pill with `Edit name`.

### 2.2 Stepper shape

Use the same 3-step visual stepper in both flows, with only labels swapped:

- Logo Maker: `1. Logo` → `2. Brand kit & assets` → `3. Launch schedule`
- Product Mockups: `1. Mockups` → `2. Ads` → `3. Schedule`

Design requirement: **identical component** (same positions, same icons, same completion marks) so that users immediately recognize it as the same guided flow.

---

## 3. Planner Surface: Scoped View & Primary CTA

### 3.1 Scoped planner window

For both flows:
- Show a **scoped, minimal planner surface**, not the full product:
  - Time range: 7 days by default (Launch Week and Campaign Mode both use the same 7-day window for v1).
  - Channels: only those chosen in the upstream step.
  - View: list/strip view focused on the posts in this flow.
- Dim everything outside the 7-day window.
- Hide advanced controls (filters, recurring rules, bulk tools) behind `More options`.

### 3.2 Single primary CTA

Both flows must share this pattern:

- Sticky primary button bottom-right:
  - Logo Maker: **`Schedule launch week`**
  - Product Mockups: **`Schedule this campaign`**

- Secondary, supporting actions (link style):
  - `Adjust posts` (scrolls to first post / expands details)
  - `Add languages` (opens multilingual dialog; see §4)

There should **never** be a situation in these guided modes where the most visually prominent CTAs are per-post. Those stay as edit affordances only.

---

## 4. Multilingual UX: One Shared Pattern

Both flows should rely on the same underlying multilingual pattern:

1. **Base post with grouped language variants**
   - One tile per base post on the planner surface.
   - Language badges inside the tile (`EN`, `ES`, `+2`).
   - Click/hover reveals a list of variants; never duplicates the tile on the main view.

2. **Optional `+ Add language` control**
   - Surface in the same place:
     - In the right-hand checklist and near the primary CTA.
   - Behavior:
     - Opens the same 2-step modal:
       1. Choose 1–3 extra languages (soft limit messaging).
       2. Confirm language additions; explain that the calendar will stay tidy via grouping.

3. **Language review**
   - `Review languages` link opens the same compact table for both flows:
     - Rows: base posts.
     - Columns: languages.
     - Cells: status + quick edit.

4. **Copy alignment**
   - Shared explainer text (adapt labels but keep structure):
     - "Add 1–3 extra languages for more reach. We’ll group languages under each post so your calendar stays tidy."

This ensures that a user who learned multilingual in Launch Week immediately understands it in Campaign Mode, and vice versa.

---

## 5. Checklists & "I’m Done" Moment

### 5.1 Checklist pattern

Use the same 3-item checklist component in both flows:

1. `Review posts and days`
2. `Choose channels` (auto-checked when coming from assets/ads step)
3. `Optional: Add languages`

Differences between flows are in microcopy only (e.g., "launch" vs "campaign"), not in component structure.

### 5.2 Confirmation layer

After scheduling in either flow:

- Full-screen confirmation layer over the planner:
  - Title variants:
    - Logo Maker: **"Your launch week is scheduled!"**
    - Product Mockups: **"Your campaign is scheduled!"**
  - Summary bullets:
    - `X posts scheduled over Y days`
    - `Channels: ...`
    - `Languages: EN (+N more)` or `Languages: EN only`.

- Same three follow-up CTAs:
  1. `View this campaign in the calendar` (for Logo Maker, replace "campaign" with "launch week"; behavior identical).
  2. `Create another campaign` / `Plan another launch` (routes back to the originating tool).
  3. `Back to dashboard`.

Consistency here is critical so that "I scheduled something" always feels like the same, reliable finish line.

---

## 6. Analytics & Instrumentation Notes

To measure friction and keep these flows aligned over time, both should emit a shared core set of events with a `source` dimension:

- `guided_campaign_mode_opened`  
  - `source = "logo_maker" | "product_mockups"`
  - `first_time = true/false`

- `guided_campaign_languages_dialog_opened`  
  - `source = ...`

- `guided_campaign_languages_added`  
  - properties: `languages_added_count`, `total_languages_count`, `source`.

- `guided_campaign_checklist_completed`  
  - which items were completed; `source`.

- `guided_campaign_scheduled`  
  - `source`, `languages_count`, `posts_count`, `time_to_scheduled_seconds`.

Dashboards should slice by `source` but otherwise treat the flows as variants of the same pattern. This makes it easy to spot if, for example, Logo Maker’s Launch Week flow is slower or leakier than Product Mockups’ Campaign Mode.

---

## 7. Open Questions / Next Steps

1. **Time expectation copy:** decide whether we standardize on "~2 minutes" vs "~5 minutes" in headers; UX preference is a single global phrase so users build a consistent mental model of effort.
2. **Shared components:** confirm with design/engineering that the header, stepper, checklist, multilingual modal, and confirmation layer are implemented as shared components with per-flow theming rather than bespoke versions.
3. **First-run vs returning behavior:** align thresholds (e.g., first 2 campaigns/launches show the full guided chrome, subsequent ones show a slim header by default with a `Show guidance` toggle).

If we implement this alignment, a user who has ever scheduled a Logo Maker launch should feel instant familiarity when scheduling a Product Mockups campaign, and the combined friction across planner + multilingual UX should drop significantly for cross-tool users.
