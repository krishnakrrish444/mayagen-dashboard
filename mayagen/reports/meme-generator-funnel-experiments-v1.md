# Meme Generator Funnel Experiments — v1

**Owner:** @seo-growth  
**Last updated:** 2026-02-13

## 1. Funnel & Metrics

Primary funnel (per user, 7-day window):
1. **Landing view**: `/meme-generator/` page_view
2. **Tool start**: `meme_tool_opened`
3. **Meme created**: `meme_created` (with variant: downloaded vs sent to planner)
4. **Post composed**: `post_composed_from_meme`
5. **Added to planner**: `planner_item_created_from_meme`
6. **Scheduled**: `post_scheduled_from_meme`
7. **First week habit**: `user_weekly_active_planner` (≥1 scheduled post in 7 days)

Core metrics:
- **Landing → tool start rate** = meme_tool_opened / page_view
- **Tool start → meme created** = meme_created / meme_tool_opened
- **Meme created → planner add** = planner_item_created_from_meme / meme_created
- **Planner add → scheduled** = post_scheduled_from_meme / planner_item_created_from_meme
- **First scheduled → 7-day habit** = user_weekly_active_planner / users_with_first_post_scheduled

Segment by:
- New vs returning users
- Traffic source (SEO / direct / social / referral)
- Language count (1 vs multi-language memes)

## 2. Experiment Themes

### Experiment A — Hero CTA Focus

**Hypothesis:** A single primary CTA ("Create your first meme") in the hero, with the planner/scheduler flow explained visually but not as competing CTAs, will increase landing → tool start rate.

- **Variant A (control-ish):** Current or copy-v2 layout with multiple CTAs (e.g., "Create meme", "Plan posts", etc.).
- **Variant B (test):**
  - One main hero CTA: **"Create your first meme"**.
  - Subtext: "Then send it straight into your social calendar in one click."
  - Flow strip below hero illustrates meme → social post → planner → calendar.

**Primary metric:** Landing → tool start rate.  
**Guardrail:** Meme created → planner add rate (should not drop meaningfully).

### Experiment B — Post-Creation Nudge to Planner

**Hypothesis:** A dedicated "Use in social post" panel with a clear benefit line will increase meme_created → planner_item_created_from_meme.

- **Control:** Simple "Download" + smaller secondary link to planner.
- **Variant:**
  - Two primary options after meme creation:
    1. **"Download image"**
    2. **"Use in social post"** (highlighted).  
  - Copy near the planner option: "Schedule this meme and 2–3 more posts in under 60 seconds."

**Primary metric:** Meme created → planner add rate.  
**Secondary:** Planner add → scheduled rate.

### Experiment C — 3-Post Planner Nudge

**Hypothesis:** A lightweight suggestion to add 2–3 more posts once the first meme is in the planner will increase the first-week habit metric.

- Trigger: After the user schedules their first meme from the Meme Generator.
- UX: Inline prompt in planner sidebar:  
  "You’re on a roll. Add 2–3 more posts to fill your week?" with quick-add suggestions using:
  - Auto-variations of the original meme
  - Caption ideas for other days

**Primary metric:** First scheduled → 7-day habit.  
**Secondary:** Average scheduled posts per user (7-day window).

### Experiment D — Language Preview Strip

**Hypothesis:** Showing a small language preview (2–3 example translations) on the landing and/or in the meme-to-post panel will increase landing → tool start, particularly for non-English traffic.

- **Variant:** Language strip with 2–3 sample markets (e.g., English, Spanish, Hindi) and note:  
  "Plan posts in 100+ languages without leaving your calendar."

**Primary metric:** Landing → tool start rate for non-English locales.  
**Guardrail:** Overall conversion to first scheduled post.

## 3. Implementation Notes

- Wire events into Analytics v2 north-star plan where possible (e.g., mark all planner events with `source = meme_generator`).
- Use feature flags for experiments A–D so they can be rolled out independently.
- Target a minimum sample size per variant that gives directional confidence before shipping broadly; exact thresholds depend on traffic levels to `/meme-generator/`.
