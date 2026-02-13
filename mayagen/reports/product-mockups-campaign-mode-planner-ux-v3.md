# Product Mockups → Campaign Mode Planner UX — v3

**Author:** @product-ux  
**Date:** 2026-02-13  
**Scope:** First-time user experience of Campaign Mode in the planner for flows that start in Product Mockups.

Goal: Make the path **idea → mockups → ads → scheduled campaign** feel like a 5–10 minute guided sprint, not “learn a new calendar tool.” This focuses specifically on the planner surface and how it behaves when opened from Product Mockups.

---

## 1. Entry: Opening Campaign Mode from Product Mockups

**Current spec (v2 summary)**
- After creating mockups and selecting them for ads, users enter a 3‑step wizard (Mockups → Ads → Schedule).
- The final step opens Campaign Mode in the planner, scoped to a 7–10 day window with campaign posts pre-configured.

**Friction risks**
1. **Context jump:** Landing on a calendar can feel like being dropped into "a whole app" instead of the final step of a short flow.
2. **Unclear time cost:** Users don’t know if this is a 30-second confirm or a 10-minute planning exercise.
3. **Multilingual anxiety:** If language options are visible immediately, users may worry they’re taking on more work than they planned.

**Concrete changes**
- **1.1 First-run header strip (campaign context)**
  - At the top of Campaign Mode, show a non-dismissable header for first-time entry from Product Mockups:
  - Title: **“Schedule your Product Mockups campaign”**
  - Subtitle: **“You’re on step 3 of 3 — review and schedule these posts. ~2 minutes.”**
  - Right side: pill showing `Campaign: <Campaign name>` and a small `Edit name` link.

- **1.2 Stepper continuity**
  - Persist a mini-stepper in the header matching the wizard:
    - `1. Mockups` ✔  `2. Ads` ✔  `3. Schedule` ●
  - This reinforces that the calendar is not a new tool, but the last step.

- **1.3 First-run focus mode**
  - On first entry from Product Mockups, automatically:
    - Center the viewport on the 7–10 day campaign window.
    - Dim non-campaign days outside the window (low contrast) to reduce perceived scope.
    - Hide non-essential planner controls (filters, views, recurring rules) behind a `More options` menu.

---

## 2. Default layout: What users see first

**Friction risks**
1. **Too many posts:** If every ad+size+channel appears as a separate tile, the grid looks overwhelming.
2. **No obvious “finish” action:** If primary CTAs are per-post (e.g., `Schedule` on each tile), users don’t know when they’re done.
3. **Language clutter:** If every language variant is a separate row/tile, the calendar looks like spam.

**Concrete changes**
- **2.1 Base-post + grouped variants visual model**
  - Represent each ad/post as a **base card** with grouped variants:
    - Show one primary tile per base post on the calendar.
    - Within the tile, show small badges: e.g., `FB`, `IG`, `EN`, `ES`.
    - Hover or click reveals a popover listing all variants.
  - Visual style: compact, pill-like cards that look like a cohesive campaign set, not individual unrelated posts.

- **2.2 Single campaign-level primary CTA**
  - At the bottom-right (sticky), show a single primary button:
    - **Primary CTA:** `Schedule this campaign`
    - Secondary link-level CTAs: `Adjust posts` (scrolls to first post) and `Add languages` (opens language modal).
  - Avoid per-post “Schedule” as the main call to action; they should be edit-level actions only.

- **2.3 Guided checklist pane**
  - Right side of Campaign Mode: a small checklist panel labeled **“Before you schedule”**:
    1. `Review posts and days` (auto-checked once user scrolls through the campaign window). 
    2. `Choose channels` (auto-checked if they used the Ads step; can show a quick summary).
    3. `Optional: Add languages` (remains unchecked until they add ≥1 extra language).
  - Checkbox styling should feel light and encouraging, not like a form.

---

## 3. Multilingual UX (keeping it optional & tidy)

This builds on `/mayagen/reports/product-mockups-mockup-to-campaign-planner-multilingual-ux-v2.md` and focuses on how it *feels* in Campaign Mode.

**Friction risks**
1. **Fear of extra work:** Showing a full language picker upfront suggests more work, not more reach.
2. **Visual overload:** Multiple language rows per day make the calendar feel “busy” and hard to scan.

**Concrete changes**
- **3.1 Multilingual as a small upgrade, not a new mode**
  - In the checklist pane and near the CTA, describe multilingual as:
    - Text: **“Optional: add 1–3 extra languages for more reach. We’ll keep your calendar tidy.”**
  - Use a small informational tooltip: “Language versions are grouped under each post, not shown as separate posts on the calendar.”

- **3.2 `+ Add language` lightweight flow**
  - Button: `+ Add language` next to the language section in the checklist.
  - Clicking opens a simple modal:
    - Step 1: select up to 3 languages (checkbox list, soft limit messaging).
    - Step 2: short confirmation screen: “We’ll add translated variants to each campaign post and group them under the original.”
  - After confirmation:
    - Update tile badges (e.g., `EN`, `ES`, `FR`).
    - Provide a `Review languages` link that opens a compact table of base posts vs languages with quick edit icons.

- **3.3 Post-schedule language clarity**
  - In the post-schedule confirmation (see section 4), include a concise summary:
    - “Your campaign is scheduled in 3 languages (EN, ES, FR). All language versions are grouped under each post in the calendar.”

---

## 4. Confirmation & “I’m done” moment

**Friction risks**
1. **No sense of closure:** If clicking `Schedule this campaign` just changes tile states, users might not realize they’re done.
2. **Where do I go next?:** Users may not know whether to close the planner, edit the campaign, or just leave.

**Concrete changes**
- **4.1 Full-screen confirmation layer**
  - After pressing `Schedule this campaign` and success from the backend:
    - Show a light, full-screen confirmation layer over the planner (not a tiny toast).
    - Content:
      - Title: **“Your campaign is scheduled!”**
      - Summary bullets:
        - `X posts scheduled over Y days`
        - `Channels: <list>`
        - `Languages: EN (+2 more)` or `Languages: EN only`.
      - Illustration or simple visual representing a calendar with checkmarks.

- **4.2 Clear next-step choices**
  - Below the summary, provide three clear actions:
    1. **Primary:** `View this campaign in the calendar` (closes layer, highlights campaign posts).
    2. **Secondary:** `Create another campaign` (takes user back to Product Mockups landing or creation flow).
    3. **Tertiary:** `Back to dashboard`.

- **4.3 Return surface**
  - On dashboard and planner home, add a small card for recently scheduled campaigns:
    - “Product Mockups campaign scheduled — starts <date>.”
    - CTAs: `View campaign` and `Duplicate for later` (future iteration).

---

## 5. First-time vs returning behavior

**Friction risks**
1. **Onboarding that never ends:** If the same header/checklist appears on the 5th campaign, it becomes noise.
2. **No shortcuts for power users:** Experienced users may want to adjust timings and channels quickly without guardrails.

**Concrete changes**
- **5.1 Limit full onboarding to first 1–2 campaigns**
  - For the first 2 campaigns starting from Product Mockups:
    - Show the full header, stepper, and checklist.
  - After that:
    - Collapse to a slimmer header with campaign name and a small `Show guided checklist` link.

- **5.2 Remember preferred view**
  - If users expand `More options` (full planner controls) and schedule from there, remember that preference for subsequent campaigns.

---

## 6. Analytics hooks (UX-focused)

To verify that these UX changes actually support the “5–10 minute” goal, we should capture:

- `campaign_mode_opened_from_product_mockups` — with a `first_time` flag.
- `campaign_mode_first_run_header_seen` — ensure exposure.
- `campaign_mode_checklist_completed` — all three checklist items.
- `campaign_mode_add_language_modal_opened` and `language_variants_added_from_campaign_mode`.
- `campaign_scheduled_from_product_mockups` — with `time_to_scheduled_campaign_seconds` from opening Campaign Mode.
- `campaign_scheduled_multilingual_from_product_mockups` — with number of languages.

These support dashboards and experiments already outlined in:
- `/mayagen/reports/product-mockups-funnel-experiments-v1.md`
- `/mayagen/reports/product-mockups-analytics-and-metrics-v1.md`

---

## 7. Summary

This v3 UX pass tightens Campaign Mode as a short, guided **step 3 of 3** rather than a generic calendar tool, with:
- A first-run header and stepper that anchor the user in the mockup → ads → schedule journey.
- A single campaign-level CTA (`Schedule this campaign`) and a light checklist so it’s obvious how to finish.
- Multilingual as a small, clearly-explained upgrade with grouped variants instead of a noisy calendar.
- A strong completion moment and return surfaces that make the scheduled campaign feel real and revisitable.

Next: partner with design to translate this into specific Figma mocks (first-run Campaign Mode, checklist pane, multilingual badges, confirmation layer) and then validate time-to-scheduled-campaign and completion rates once implemented.