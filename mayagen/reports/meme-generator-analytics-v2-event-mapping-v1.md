# Meme Generator → Planner/Scheduler — Analytics v2 Event Mapping (v1)

This doc maps the Meme Generator–specific funnel and experiments onto the shared Analytics v2 event dictionary so implementation, analytics, and experimentation can speak the same language.

It sits on top of:
- `/mayagen/reports/meme-generator-analytics-and-metrics-v1.md`
- `/mayagen/reports/meme-generator-funnel-experiments-v2.md`

The goal: **one consistent set of events and properties** that lets us read:
- Free tool entry → first asset
- Asset → first post in planner
- First post → first scheduled post
- Scheduled post → weekly planner habit

All specifically attributable to `first_activation_source = "meme_generator"`.

---

## 1. Canonical Events & Properties

We reuse Analytics v2 primitives wherever possible and add source-specific properties rather than inventing new, tool-specific events.

### 1.1 Core Events

**Asset creation**
- `tool_asset_created`
  - `tool_id = "meme_generator"`
  - `asset_type = "image"`
  - `template_id` (if applicable)

**Planner post creation (from Meme Generator)**
- `planner_post_created`
  - `source = "meme_generator"`
  - `entry_mode = "from_tool_cta" | "from_tool_autonudge"`
  - `language_count` (integer, includes base language)

**Planner slot filled / updated**
- `planner_slot_filled`
  - `source = "meme_generator"`
  - `language_count`
  - `has_variants = true|false` (for multi-language posts)

**Schedule created / updated**
- `schedule_created`
  - `source = "meme_generator"`
  - `schedule_scope = "single_post" | "launch_week" | "ad_campaign"`
  - `language_count`

- `schedule_published`
  - `source = "meme_generator"`
  - `schedule_scope`
  - `language_count`

**Weekly habit / retention**
- `user_weekly_active_planner`
  - `first_activation_source = "meme_generator" | ...`
  - `has_multilingual_posts = true|false`
  - `planner_sessions_this_week`

### 1.2 Supporting Events (Meme Generator UI)

**Landing & engagement**
- `marketing_page_viewed`
  - `page_slug = "meme-generator"`

- `marketing_cta_clicked`
  - `page_slug = "meme-generator"`
  - `cta_id = "hero_primary" | "hero_secondary" | "suite_strip_meme" | ...`

**In-tool funnel**
- `meme_editor_opened`
  - `entry_source = "landing" | "internal_nav" | "shared_link"`

- `meme_draft_saved`
  - `asset_id`
  - `template_id`

- `meme_created`
  - `asset_id`
  - `template_id`

**Bridging into planner/scheduler**
- `tool_cta_clicked`
  - `tool_id = "meme_generator"`
  - `cta_id = "use_in_social_post" | "add_to_planner" | "schedule_post"`

These supporting events either:
- Map to existing Analytics v2 events (`marketing_page_viewed`, `marketing_cta_clicked`, `tool_cta_clicked`), or
- Use a `meme_*` prefix but are **local to this tool** and roll up into the core planner/scheduler events via `asset_id` and `source`.

---

## 2. Funnel Definitions (Mapped to Events)

### 2.1 Free Tool → First Asset

Funnel: **Landing → Editor → Created meme**

1. `marketing_page_viewed` (page_slug = "meme-generator")
2. `meme_editor_opened` (entry_source = "landing")
3. `meme_created` (asset_id)
4. `tool_asset_created` (tool_id = "meme_generator")

Key metrics:
- View → editor open rate
- Editor open → meme created rate
- Time from first `marketing_page_viewed` to first `meme_created`

### 2.2 First Asset → First Planner Post

Funnel: **Meme created → Use in social post → Planner post created**

1. `meme_created`
2. `tool_cta_clicked` (tool_id = "meme_generator", cta_id = "use_in_social_post")
3. `planner_post_created` (source = "meme_generator")

Key metrics:
- Meme created → CTA click rate
- CTA click → planner post created rate
- Time from `meme_created` to `planner_post_created`

### 2.3 First Planner Post → First Scheduled Post

Funnel: **Planner post created → Slot filled → Schedule created/published**

1. `planner_post_created` (source = "meme_generator")
2. `planner_slot_filled` (source = "meme_generator")
3. `schedule_created` (source = "meme_generator")
4. `schedule_published` (source = "meme_generator")

Key metrics:
- Post created → scheduled-post rate
- Time-to-first-scheduled-post from Meme Generator
- Distribution of `schedule_scope` and `language_count`

### 2.4 First Scheduled Post → Weekly Habit

Funnel: **Schedule published → Weekly planner active**

1. First `schedule_published` (source = "meme_generator")
2. Subsequent `user_weekly_active_planner` (first_activation_source = "meme_generator")

Key metrics:
- % of Meme Generator–activated users with weekly planner activity
- Time lag from first scheduled post to first weekly active planner event

---

## 3. Experiments → Events (Cross-check)

From `/mayagen/reports/meme-generator-funnel-experiments-v2.md`, each experiment now references these canonical events.

Examples (non-exhaustive):

- **Experiment A — Hero CTA focus**
  - Primary: change in `marketing_cta_clicked` (cta_id = "hero_primary") rate per `marketing_page_viewed` on `/meme-generator/`.
  - Secondary: downstream impact on `meme_editor_opened` and `meme_created`.

- **Experiment B — Post-creation planner nudge**
  - Primary: change in `tool_cta_clicked` (cta_id = "use_in_social_post") per `meme_created`.
  - Secondary: change in `planner_post_created` (source = "meme_generator") per `meme_created`.

- **Experiment C — 3-post planner suggestion**
  - Primary: average `planner_slot_filled` count per user with source = "meme_generator" in first session.
  - Guardrails: no significant drop in `schedule_created` or `schedule_published` conversion.

- **Experiment D — Language preview strip**
  - Primary: adoption of multilingual via `language_count > 1` on `planner_post_created` and `schedule_created` (source = "meme_generator").
  - Guardrails: ensure no increase in drop-off from `planner_post_created` → `schedule_published`.

This alignment means engineering and analytics can:
- Implement once in the shared Analytics v2 layer.
- Attach experiments as filters/segments (e.g., feature flags, variant ids) on these standard events.

---

## 4. Open Questions / Implementation Notes

- Confirm that `tool_asset_created`, `planner_post_created`, `planner_slot_filled`, `schedule_created`, `schedule_published`, and `user_weekly_active_planner` are already part of the central Analytics v2 schema. If any differ, **rename in this doc rather than forking the schema.**
- Decide where `meme_*` events live (likely as tool-local events mapped onto core planner/scheduler events through `asset_id` and `source`).
- Ensure `first_activation_source` is computed once (activation cohorting layer), with `"meme_generator"` set when a user’s first qualifying planner/scheduler event comes from this funnel.

Once names are confirmed, this doc should be treated as the source of truth for Meme Generator event naming and referenced by both the analytics implementation and the experimentation backlog.