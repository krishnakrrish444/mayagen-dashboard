# Meme Generator Analytics & Metrics — v1

**Owner:** @seo-growth  
**Last updated:** 2026-02-13

This document ties the `/meme-generator/` landing + tool to Analytics v2 and Growth v2. It defines concrete events, funnels, and dashboards so we can measure the full flow from SEO visit → first meme → first scheduled post → weekly habit.

---

## 1. Event Taxonomy (Meme Generator → Planner/Scheduler)

Where possible, reuse/align with Analytics v2 naming. All events below should include common properties like `user_id` (if logged in), `session_id`, `anonymous_id` (pre‑signup), `plan`, `device`, and `country`.

### 1.1 Core Events

1. **`meme_generator_landing_viewed`**
   - **When:** `/meme-generator/` marketing page is viewed (SSR/SSG route).  
   - **Props:**  
     - `source` ("seo", "direct", "referral", "paid", etc.)  
     - `language` (derived from locale/Accept-Language)  
     - `is_returning_visitor` (bool)  

2. **`meme_tool_opened`**
   - **When:** User opens the Meme Generator tool UI from the landing page (hero CTA, internal link, or deep link).  
   - **Props:**  
     - `entry_point` ("hero_cta", "template_section", "internal_link", "direct_tool_route")  
     - `language`  

3. **`meme_created`**
   - **When:** User successfully generates a meme (image rendered or template + caption applied).  
   - **Props:**  
     - `creation_mode` ("template", "upload_image", "ai_from_prompt")  
     - `language_count` (1, 2, 3+; based on caption/localization variants created)  
     - `is_first_meme_this_session` (bool)  

4. **`meme_action_selected`**
   - **When:** User chooses what to do with a created meme in the post‑generation panel.  
   - **Props:**  
     - `action` ("download", "download_no_watermark", "use_in_social_post", "share", "save_template")  
     - `language_count`  
     - `is_first_meme_this_session`  

5. **`post_composed_from_meme`**
   - **When:** User opens the mini composer / full composer with a meme attached and edits/accepts caption.  
   - **Props:**  
     - `network` ("instagram", "facebook", "linkedin", "tiktok", etc.)  
     - `language_count`  
     - `composer_surface` ("inline_panel", "full_planner", "campaign_mode")  
     - `source` = "meme_generator" (key for cross‑tool analysis)

6. **`planner_item_created_from_meme`**
   - **When:** User adds at least one post using a meme into the planner (draft or scheduled).  
   - **Props:**  
     - `network`  
     - `language_count`  
     - `scheduled_status` ("draft", "scheduled")  
     - `time_to_first_planner_item_seconds` (from first `meme_created` this session)  
     - `source` = "meme_generator"

7. **`post_scheduled_from_meme`**
   - **When:** User actually schedules a post containing a meme from this funnel.  
   - **Props:**  
     - `network`  
     - `language_count`  
     - `time_to_first_scheduled_post_seconds` (from first `meme_created` this session)  
     - `source` = "meme_generator"

8. **`user_weekly_active_planner`**  
   - Already part of Analytics v2; here we care about the **subset** where `source = "meme_generator"` for first activation.  
   - **Definition:** User with ≥1 scheduled (and not cancelled) post in the last 7 days.  
   - **Props:**  
     - `first_activation_source` ("meme_generator", "logo_maker", etc.)  
     - `language_count_last_7_days` (max languages in scheduled posts).

### 1.2 Experiment-Specific Events

For the experiments defined in `meme-generator-funnel-experiments-v1.md`:

1. **`meme_experiment_variant_assigned`**
   - **When:** User is bucketed into a variant on `/meme-generator/`.  
   - **Props:**  
     - `experiment_name` (e.g., "meme_hero_cta_focus", "meme_post_creation_nudge", "meme_3_post_nudge", "meme_language_preview_strip")  
     - `variant` ("control", "test_a", "test_b", etc.)

2. **`meme_3_post_nudge_viewed` / `meme_3_post_nudge_accepted`**
   - **When:** The planner shows the suggestion to add 2–3 more posts after first scheduled meme, and when user accepts.  
   - **Props:**  
     - `network_primary`  
     - `language_count`  
     - `time_from_first_scheduled_post_seconds`

3. **`meme_language_preview_interacted`**
   - **When:** User hovers/clicks on the language preview strip on landing or in the meme‑to‑post panel.  
   - **Props:**  
     - `surface` ("landing", "post_panel")  
     - `selected_language`  

---

## 2. Funnels & Ratios

Define funnels that map cleanly to the experiments + growth goals.

### 2.1 Core Activation Funnel (Landing → Weekly Habit)

Per user, over a 7‑day window:

1. `meme_generator_landing_viewed`
2. `meme_tool_opened`
3. `meme_created`
4. `meme_action_selected` with `action = "use_in_social_post"`
5. `planner_item_created_from_meme`
6. `post_scheduled_from_meme`
7. `user_weekly_active_planner` (with `first_activation_source = "meme_generator"`)

Key ratios:
- **Landing → Tool Start** = `meme_tool_opened` / `meme_generator_landing_viewed`
- **Tool Start → Meme Created** = `meme_created` / `meme_tool_opened`
- **Meme Created → Planner Add** = `planner_item_created_from_meme` / `meme_created`
- **Planner Add → Scheduled** = `post_scheduled_from_meme` / `planner_item_created_from_meme`
- **First Scheduled → Weekly Habit** = count of users with `user_weekly_active_planner` and `first_activation_source = "meme_generator"` / users with first `post_scheduled_from_meme`

Slice by:
- `source` ("seo", "social", "referral", "paid")  
- `is_returning_visitor`  
- `language_count` bucket (1 vs 2–3 vs 4+).

### 2.2 Experiment A — Hero CTA Focus

Goal: improve **Landing → Tool Start**.

- Compare Landing → Tool Start by `experiment_name = "meme_hero_cta_focus"` and `variant`.
- Also monitor entire funnel to ensure no degradation downstream.

### 2.3 Experiment B — Post‑Creation Nudge to Planner

Goal: improve **Meme Created → Planner Add**.

- Compare `planner_item_created_from_meme` / `meme_created` across `experiment_name = "meme_post_creation_nudge"` variants.

### 2.4 Experiment C — 3‑Post Planner Nudge

Goal: improve **First Scheduled → Weekly Habit**.

- Focus on users with at least one `post_scheduled_from_meme`.
- Compare:
  - Avg scheduled posts in 7 days.  
  - Week‑2 retention (using `user_weekly_active_planner`)  
  - By `experiment_name = "meme_3_post_nudge"` variant.

### 2.5 Experiment D — Language Preview Strip

Goal: improve **Landing → Tool Start**, especially for non‑English.

- Segment by `language` and `language_count`.
- Ensure guardrails on final **First Scheduled → Weekly Habit**.

---

## 3. Dashboards

### 3.1 Founder View — High‑Level Story

Purpose: answer "Is the Meme Generator actually feeding the planner + scheduler habit?" in one screen.

Key tiles:
1. **Meme → Planner Activation Funnel (Last 7 & 28 Days)**  
   - Funnel viz of the 7 steps in 2.1.  
   - Segmented by `source` (SEO vs non‑SEO).

2. **New Users Activated via Meme Generator**  
   - # of new signups whose `first_activation_source = "meme_generator"` (weekly).  
   - Compare against other tools (logo, product mockups, etc.).

3. **Weekly Habit from Meme Generator**  
   - Count of users with `user_weekly_active_planner` where `first_activation_source = "meme_generator"`.  
   - % of total weekly active planner users.

4. **Experiments Status Snapshot**  
   - For each active experiment A–D:  
     - Variant performance vs control on its primary metric.  
     - Simple labels: "Winning / Losing / Inconclusive".

5. **Traffic & Conversion Overview for `/meme-generator/`**  
   - SEO impressions/clicks (from Search Console).  
   - Sessions and visitors (from analytics).  
   - Visitor → signup rate attributable to Meme Generator funnel.

### 3.2 PM/UX View — Flow & Friction

Purpose: help product/UX tune the flow and decide what to build next.

Key views:
1. **Step Drop‑Off by Entry Point**  
   - Funnel 2.1 broken down by `entry_point` (hero CTA vs internal modules vs direct tool).  
   - Identify weak spots (e.g., high drop between `meme_created` and `meme_action_selected` → fix post‑creation panel).

2. **Time‑to‑First Scheduled Post**  
   - Distribution of `time_to_first_scheduled_post_seconds` for users whose first activation source is Meme Generator.  
   - Goal: majority in `0–600s` bucket (≤10 minutes) per Growth v2.

3. **Language Usage & Impact**  
   - Histogram of `language_count` in posts scheduled from Meme Generator.  
   - Conversion by language_count (does multi‑language boost or hurt habit?).

4. **Path Analysis Around Post‑Creation Panel**  
   - Paths from `meme_created` → `meme_action_selected` → next events.  
   - Identify most common dead ends (e.g., `action = "download"` with no planner activity) and inform tweaks.

5. **Experiment Deep Dives**  
   - Dedicated charts for each experiment, aligned with `meme-generator-funnel-experiments-v1.md` primary metrics and guardrails.

---

## 4. Implementation Notes

- Use the same identity stitching approach as Analytics v2: tie pre‑signup `anonymous_id` to `user_id` on signup so we don’t lose the path from landing to first scheduled post.
- Ensure `/meme-generator/` and the tool route(s) are tagged consistently with `source = "meme_generator"` on all planner/scheduler events; this lets us compare funnels across tools.
- For SEO analysis, connect Search Console data (queries, impressions, CTR) for `/meme-generator/` with analytics sessions (e.g., via `gclid`, `utm`, or GSC–analytics join) to see which queries actually lead to scheduled posts vs just meme creation.
- Start with a minimal, reliable set of events; avoid premature micro‑events that create noise. Expand only when we see specific UX questions that need more granularity.
