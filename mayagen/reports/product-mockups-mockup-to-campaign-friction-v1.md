# Product Mockups → Campaign Mode UX Friction Audit (v1)

## Scope

Flow under review:

> User lands in Product Mockups → creates first mockup → adds it to an ad/template → schedules an initial campaign via planner/scheduler (including multilingual variants).

Goal: Make "idea → mockup → scheduled campaign" feel achievable in ~5–10 minutes for a first-time user, without them getting stuck in export/download dead-ends or overwhelmed by planner/scheduler complexity.

---

## 1. Entry & First-Time Orientation

### Observed / Likely Friction
- Landing page and in-app entry points still feel like "asset generator" tools rather than a campaign starting point.
- First-time users may not realize there is a guided path from mockups into ads and a campaign-focused planner view.
- Language around "Download" or "Export" tends to dominate mental models, encouraging users to leave the app after saving files.

### Concrete Changes
1. **Reframe entry copy & UI as campaign-first**
   - Primary CTA: `Create product mockups & launch ads` (vs. generic "Create mockups").
   - Subtext: "Go from new visuals to a scheduled campaign in minutes."
   - Add a short **3-step explainer strip** near the hero:
     1. Design scroll-stopping mockups
     2. Turn them into ready-to-run ads
     3. Schedule a full campaign in your calendar

2. **Introduce a visible "Campaign Mode" affordance**
   - On first entry, show a brief modal/side panel: "New: Mockups to Campaign Mode" with a one-sentence promise and `Start with a campaign` vs `Just create mockups` options.
   - Persist a small pill or toggle inside Product Mockups labeled `Campaign Mode` so users can re-enter the guided flow later.

---

## 2. Mockup Creation Screen

### Observed / Likely Friction
- After creating a mockup, the most obvious actions are usually `Download`, `Duplicate`, or `Edit`.
- There may be no strong visual or textual nudge that this mockup is the **first step of a campaign**, not the final result.

### Concrete Changes
1. **Promote "Use in ads" as the primary next step**
   - In the mockup success state and editor header, make the main CTA: `Use in ads & campaign`.
   - Demote `Download` to a secondary/ghost button or menu item.

2. **Batch selection for ad sets**
   - Allow quick multi-select on generated mockups with a prominent `Create ad set` button.
   - Show inline guidance: "Pick 2–5 mockups for this campaign" with a small hint that variety helps performance.

3. **Time expectation microcopy**
   - Under the main CTA: "2–3 minutes to wrap these into ready-to-run ads."

---

## 3. Mockups → Ads Wizard (Step 2)

### Observed / Likely Friction
- Users can get overwhelmed if they must pick formats, placements, and copy variants all at once.
- Without strong defaults, they may drop off before reaching the planner.

### Concrete Changes
1. **Opinionated defaults per primary use case**
   - Based on selected use case (ecommerce / SaaS / launch announcement), pre-select:
     - 2–3 key layouts (e.g., square feed, story/reel, landscape).
     - A single suggested message frame (e.g., "New arrival", "Limited-time offer").
   - Let advanced users expand an `Advanced options` panel for deeper control.

2. **Single-field copy first, variants later**
   - Ask for one primary message (headline/body) up front.
   - Generate alternative lines automatically and show them as suggestions, not required inputs.

3. **Inline preview of the campaign set**
   - Right-hand pane: preview strip of selected mockups across formats with a simple label like `Campaign: Summer drop (3 ads)`.

4. **Clear handoff to scheduling**
   - Primary CTA at the end of this step: `Continue to schedule campaign`.
   - Microcopy: "1–2 minutes to place these on your calendar." 

---

## 4. Campaign-Focused Planner View

### Observed / Likely Friction
- Generic planners can feel heavy: full-month views, all brands, all posts mixed together.
- A first-time user may not know how many posts to schedule, or on which days.
- Multilingual controls can explode complexity if every language shows as a separate tile.

### Concrete Changes
1. **Scoped "Campaign Mode" calendar**
   - Show a **focused, pre-filtered view**: only this campaign's posts, over a recommended window (e.g., 7–14 days).
   - Default to a simple horizontal strip or week view with recommended slots pre-filled.

2. **Recommended schedule template**
   - Offer 1–2 templates like:
     - `Standard`: 1 post/day for 7 days.
     - `Launch push`: Heavier cluster at launch, then 2–3 follow-ups.
   - Default to one template and let users adjust by dragging posts.

3. **Single CTA to commit**
   - Above the calendar, show a clear CTA: `Schedule this campaign` that:
     - Confirms all proposed times.
     - Surfaces any missing channels/links.

4. **Simplified editing**
   - In this mode, prioritize:
     - Moving posts by drag-and-drop.
     - Toggling channels (e.g., IG, FB, LinkedIn) via simple checkboxes.
   - Hide global planner complexity (filters, multiple brands, etc.) behind a `Exit Campaign Mode` action.

---

## 5. Multilingual UX

### Observed / Likely Friction
- Adding languages can feel like multiplying work, especially if each language appears as its own post tile.
- Users may fear "explosion" when they toggle 3–4 languages on.

### Concrete Changes
1. **Base post + language variants model**
   - Treat each scheduled slot as a **base post** with nested language variants.
   - In the campaign planner, show a single tile per time slot; clicking it opens variants like `English`, `Spanish`, `Hindi` as entries.

2. **Constrained language control**
   - In the wizard or planner sidebar, add:
     - `Base language` dropdown.
     - `+ Add language` button with a short explanation: "We’ll keep all languages grouped in one slot so your calendar doesn’t explode."
   - Cap the suggested number of languages (e.g., gently recommend 1–2 extra).

3. **Variant health indicators**
   - Use small inline badges on the base post tile:
     - `EN +1` or `EN +2` to show how many localized versions exist.
     - Warning if a variant is missing required fields.

4. **Language-aware previews**
   - In the campaign summary and previews, allow quick toggling between language views via a segmented control.

---

## 6. Confirmation, Feedback & Return Path

### Observed / Likely Friction
- After scheduling, users may not fully trust that their campaign is "real".
- If there is no obvious place to review/edit the campaign later, they may feel lost.

### Concrete Changes
1. **Strong success state**
   - After `Schedule this campaign`, show a confirmation:
     - Title: `Your campaign is scheduled`
     - Summary: `7 posts • 3 formats • EN +1 language over 10 days`
     - Visual preview of the timeline.

2. **Dedicated campaign summary page**
   - Provide an explicit `View campaign summary` link with:
     - Calendar snapshot.
     - Per-post previews.
     - Edit/cancel/reschedule controls.

3. **Dashboard re-entry**
   - On the main dashboard, surface a `Campaigns` section with cards for active/recent campaigns.
   - Each card should have `View details` and `Duplicate campaign` actions.

4. **Analytics hooks**
   - Ensure events such as `mockup_created`, `mockup_added_to_ad_set`, `campaign_mode_opened`, `campaign_scheduled`, and `campaign_scheduled_multilingual` are wired.
   - These metrics will let @analytics and @product-ux identify drop-offs and validate whether the simplified flow reduces friction.

---

## 7. Prioritization & Next Steps

### High-Impact, Low-Risk Changes
- Re-label CTAs and microcopy around mockup completion to emphasize "Use in ads & campaign" over download.
- Introduce the scoped Campaign Mode calendar view with a single `Schedule this campaign` action.
- Implement the base-post + grouped language variants model in the planner.

### Medium-Term Enhancements
- Add recommended schedule templates and use-case-based defaults.
- Build the campaigns dashboard section for re-entry and iteration.

### Suggested Ownership
- @product-ux: Lead UX flows for Campaign Mode calendar, grouped language variants, and success/summary screens.
- @analytics: Define and instrument the key events for this funnel.
- @content-lead: Refine microcopy and empty states to keep the experience clear and encouraging.