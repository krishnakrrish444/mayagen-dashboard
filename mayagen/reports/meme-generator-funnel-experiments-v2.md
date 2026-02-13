# Meme Generator Funnel Experiments — v2 (Analytics v2 Aligned)

**Owner:** @seo-growth  
**Last updated:** 2026-02-13

This v2 updates the original Meme Generator experiment suite so it cleanly plugs into the **Analytics & Tracking Plan v2** and the dedicated **Meme Generator Analytics & Metrics v1** spec.

North-star context:
- Meme Generator is a **free, high-intent entry tool** into the suite.
- Its job is not just memes; it is to reliably drive the workflow:
  > **SEO visit → first meme → first scheduled post → weekly planner habit**
- All experiments must be wired into:
  - Analytics v2 north stars (W-CWAC, WAC, A2S, PASR)
  - Meme-specific funnel metrics and dashboards.

---

## 1. Canonical Funnel & Metrics (Aligned to Analytics v2)

We treat Meme Generator as a **workflow source** into the global event model.

### 1.1 Canonical Funnel (per user, 7–14 day window)

Events (from `meme-generator-analytics-and-metrics-v1`):
1. `meme_generator_landing_viewed`
2. `meme_tool_opened`
3. `meme_created`
4. `meme_action_selected` with `action = "use_in_social_post"`
5. `post_composed_from_meme`
6. `planner_item_created_from_meme`
7. `post_scheduled_from_meme`
8. `user_weekly_active_planner` with `first_activation_source = "meme_generator"`

Bridges into Analytics v2 entities:
- Each `meme_created` should map to a **tool asset**:
  - emit/attach a `tool_asset_created` (or equivalent) with `asset_id`, `origin = "mayagen_tool"`, and `source = "meme_generator"`.
- Each `planner_item_created_from_meme` should correspond to a `planner_post_created` or `planner_slot_filled` with the same `asset_id` and `source = "meme_generator"`.
- Each `post_scheduled_from_meme` should map to `schedule_created` (and later `schedule_published`) with `asset_id` and `asset_origin = "mayagen_tool"`, `source = "planner" | "tool"`, and `source_detail = "meme_generator"` if available.

Key ratios (same structure as v1, but explicitly tied to Analytics v2):
- **Landing → Tool Start**  
  `meme_tool_opened / meme_generator_landing_viewed`
- **Tool Start → Meme Created**  
  `meme_created / meme_tool_opened`
- **Meme → Planner Add**  
  `planner_item_created_from_meme / meme_created`
- **Planner Add → Scheduled**  
  `post_scheduled_from_meme / planner_item_created_from_meme`
- **First Scheduled → Weekly Habit (Meme Source)**  
  `users_with user_weekly_active_planner & first_activation_source="meme_generator" / users_with first post_scheduled_from_meme`

How this rolls up into Analytics v2 north stars:
- **W-CWAC / WAC:** users whose first `tool_asset_created` + `schedule_created` path originates from `source = "meme_generator"`.
- **A2S:** Meme-driven `asset_id` should have the same 30-day assets-to-schedule conversion treatment as any other tool, but segmented by `source = "meme_generator"`.
- **PASR:** For meme-originated schedules, track the share where `source = "planner"` (vs scheduler-only) — we want Meme Generator to teach the planner habit, not bypass it.

Segmentation:
- `source` ("seo", "direct", "referral", "paid")
- `language_count` bucket (1 vs 2–3 vs 4+), aligned with multi-language modeling in Analytics v2
- `is_returning_visitor`

---

## 2. Experiments A–D (Analytics v2 Aligned)

The experiment ideas stay close to v1 but now carry **explicit event, metric, and dashboard wiring** so implementation is unambiguous.

All experiments share:
- Assignment event: `meme_experiment_variant_assigned`
  - `experiment_name`
  - `variant`
- Analysis: primary + guardrail metrics drawn from the canonical funnel and Analytics v2 north stars.

### Experiment A — Hero CTA Focus (Landing → Tool Start)

**Hypothesis**  
A single, focused hero CTA — **"Create your first meme"** — with the planner/scheduler story explained in visuals and subtext (not competing buttons) will increase **Landing → Tool Start** without hurting downstream scheduling.

**Implementation**
- Surfaces: `/meme-generator/` hero section + immediate below-the-fold flow strip.
- Variants (via feature flag):
  - **Control:** current/copy-v2 layout with multiple CTAs (e.g., "Create meme", "Plan posts").
  - **Test:**
    - One primary CTA: **"Create your first meme"**.
    - Subcopy: "Then send it straight into your social calendar in one click."
    - Flow strip showing: **Meme → Social post → Planner → Calendar**.
- Events:
  - `meme_experiment_variant_assigned` with `experiment_name = "meme_hero_cta_focus"`.
  - `meme_generator_landing_viewed` (already defined).
  - `meme_tool_opened` with `entry_point` ("hero_cta", "other").

**Primary metric**
- **Landing → Tool Start rate**, sliced by experiment variant:  
  `meme_tool_opened / meme_generator_landing_viewed`.

**Guardrails**
- **Meme → Planner Add rate** and **Planner Add → Scheduled rate** to ensure we arent front-loading low-intent users:
  - `planner_item_created_from_meme / meme_created`
  - `post_scheduled_from_meme / planner_item_created_from_meme`
- Founder dashboard impact: watch W-CWAC / WAC from `source = "meme_generator"` for any degradation.

---

### Experiment B — Post-Creation Nudge to Planner (Meme → Planner Add)

**Hypothesis**  
A prominent **"Use in social post"** option with a tight benefit line in the post-creation panel will increase the share of users who send their meme to the planner versus only downloading.

**Implementation**
- Surface: Meme Generator post-creation panel.
- Variants:
  - **Control:** existing layout (download primary, planner as secondary text/link).
  - **Test:** two clearly ranked actions:
    1. **"Download image"** (secondary)
    2. **"Use in social post"** (primary, highlighted)
  - Copy: "Schedule this meme and 2–3 more posts in under 60 seconds."
- Events:
  - `meme_experiment_variant_assigned` with `experiment_name = "meme_post_creation_nudge"`.
  - `meme_action_selected` with `action` = "download" | "use_in_social_post".
  - `post_composed_from_meme`, `planner_item_created_from_meme`, `post_scheduled_from_meme`.

**Primary metric**
- **Meme → Planner Add rate:**  
  `planner_item_created_from_meme / meme_created`, by variant.

**Secondary metrics**
- **Meme → Compose rate:**  
  `post_composed_from_meme / meme_created`.
- **Planner Add → Scheduled rate:**  
  `post_scheduled_from_meme / planner_item_created_from_meme`.

**Guardrails**
- Share of `meme_action_selected` with `action = "download"` should not collapse; we want to *re-route* a meaningful portion into planner, not block simple one-off downloads.
- Monitor **time_to_first_scheduled_post_seconds** from `meme_created` to ensure the flow remains within the Growth v2 target (~5–10 minutes to first scheduled post).

---

### Experiment C — 3-Post Planner Nudge (First Scheduled → Weekly Habit)

**Hypothesis**  
After a user schedules their first meme-based post, a **lightweight nudge** to add 2–3 more posts (using quick suggestions) will increase:
- Posts scheduled in the first 7 days, and
- The probability they show up as **user_weekly_active_planner** in subsequent weeks.

**Implementation**
- Trigger: first `post_scheduled_from_meme` event for a user.
- Surface: planner sidebar or inline panel.
- Variant (on):
  - Prompt: "Youre on a roll. Fill out this week with 2–3 more posts?"
  - Quick-add suggestions based on the original meme + templated posts.
- Events:
  - `meme_experiment_variant_assigned` with `experiment_name = "meme_3_post_nudge"`.
  - `meme_3_post_nudge_viewed`, `meme_3_post_nudge_accepted`.
  - Downstream: `planner_item_created_from_meme`, `post_scheduled_from_meme`, `user_weekly_active_planner` (with `first_activation_source`).

**Primary metrics**
- **First-week scheduled posts per user** (meme-sourced):  
  For users with a `post_scheduled_from_meme` in week 0, compare average number of scheduled posts (any source) in the next 7 days by variant.
- **First Scheduled → Weekly Habit (Meme Source)**:  
  `user_weekly_active_planner` (with `first_activation_source = "meme_generator"`) / users with first `post_scheduled_from_meme`, by variant.

**Guardrails**
- Do not materially increase cancellation rate (`schedule_canceled`) on posts created via the nudge.
- Keep time-to-first-scheduled-post distribution similar; the nudge is **after** first schedule and should not delay the first success moment.

---

### Experiment D — Language Preview Strip (Non-English Landing → Tool Start)

**Hypothesis**  
Showing a compact, credible language preview (2–3 examples) on the Meme Generator landing page and/or in the meme-to-post panel will improve **Landing → Tool Start** for non-English users and increase multi-language adoption without harming core funnel conversion.

**Implementation**
- Surfaces:
  - `/meme-generator/` landing: language strip near hero or flow strip.
  - Meme-to-post panel: small language selector preview.
- Treatment:
  - Display 2–3 highlighted languages (e.g., English, Spanish, Hindi) with sample captions.
  - Copy: "Plan posts in 100+ languages without making your calendar messy." (ties into grouped-variant UX specs).
- Events:
  - `meme_experiment_variant_assigned` with `experiment_name = "meme_language_preview_strip"`.
  - `meme_language_preview_interacted` with `surface` = "landing" | "post_panel"; `selected_language`.
  - Standard funnel: `meme_tool_opened`, `meme_created`, `planner_item_created_from_meme`, `post_scheduled_from_meme` with `language_count`.

**Primary metrics**
- **Landing → Tool Start for non-English traffic:**  
  `meme_tool_opened / meme_generator_landing_viewed` where `language != 'en'`.
- **Multi-language adoption rate:**  
  Share of meme-originated scheduled posts with `language_count >= 2`.

**Guardrails**
- **Overall First Scheduled → Weekly Habit (Meme Source)** should not degrade for non-English users; the calendar must stay manageable even with more languages.
- Monitor planner/scheduler friction metrics from Analytics v2 (e.g., time-to-first-scheduled-post, cancellations) by `language_count` bucket.

---

## 3. Dashboard & Analytics Wiring

To make these experiments decision-ready, wire them into both the **Founder** and **PM/UX** views:

### 3.1 Founder View Additions

- Add a **Meme Generator Source** segment to:
  - W-CWAC / WAC breakdown by `first_activation_source`.
  - A2S, filtered to `source = "meme_generator"`.
- Add an **Experiments A–D summary tile**:
  - For each active experiment, show primary metric uplift vs control with a simple label: `Winning / Losing / Inconclusive`.

### 3.2 PM/UX View Additions

- Step drop-off and time-to-value charts specifically for Meme Generator-sourced workflows:
  - Funnels and path analysis filtered to `source = "meme_generator"`.
- Multi-language impact section:
  - Distribution of `language_count` for posts scheduled from Meme Generator.
  - Conversion and retention by `language_count` bucket, to validate the language preview strip.

---

## 4. Implementation Notes & Checklist

For engineering/analytics:

- [ ] Ensure Meme Generator events (`meme_*`) carry `source = "meme_generator"` and, where applicable, map to core Analytics v2 events: `tool_asset_created`, `planner_post_created` / `planner_slot_filled`, `schedule_created`, `schedule_published`.
- [ ] Implement `meme_experiment_variant_assigned` with a consistent schema (`experiment_name`, `variant`) and log it once per session/experiment.
- [ ] Define PostHog cohorts for `first_activation_source = "meme_generator"` based on first `post_scheduled_from_meme` mapped to `schedule_created`/`schedule_published`.
- [ ] Add Meme Generator experiment tiles to the central "Experimentation" dashboard, referencing these primary metrics and guardrails.

This keeps Meme Generator tightly connected to the global **create → plan → schedule → weekly habit** story and makes it trivial to compare its impact to other free tools like Logo Maker and Product Mockups.
