# Mayagen Analytics & Tracking Plan v2

_Last updated: 2026-02-12_

## 0. Purpose & Principles

This plan focuses on understanding and improving **cross-tool workflows** in Mayagen — how users move from:

> **Creation tools → Planner → Scheduler → Repeat usage**

Key principles:
- **Workflow-first**: Model complete flows ("first graphic → first scheduled post") rather than isolated feature events.
- **Meaningful activation**: Activation is defined as reaching an outcome that predicts retention (e.g., publishing a scheduled post from a generated asset), not just signing up or clicking around.
- **North-star aligned**: All metrics roll up into 3–5 north-star metrics (Section 2) that describe durable creator value.
- **Implementable**: Designed for Next.js + PostHog with a mix of front-end + backend tracking.

---

## 1. Core Concepts & Entities

Before events, we need a shared language for entities and identifiers.

### 1.1 Identities

- **`user_id` (string)**
  - Stable internal user ID from the auth system.
  - Required on all authenticated events.

- **`anonymous_id` (string)**
  - Client-level identifier (cookie/localStorage) used before login/sign-up.
  - Used to stitch pre-signup behavior to the eventual `user_id`.

- **`workspace_id` / `team_id` (optional)**
  - If Mayagen is multi-workspace or supports teams, this should be included on all events where applicable.

- **`session_id` (string)**
  - Optional but useful for journey analysis. Generated client-side per visit.

### 1.2 Content & Planner/Scheduler Entities

- **`project_id`**: Grouping of related content (optional, if exists today).
- **`asset_id`**: Any media created or imported (images, carousels, videos in future).
- **`plan_id`**: A planning artifact (e.g., a content calendar, campaign, or draft plan).
- **`schedule_id`**: A scheduled post job (single network/post combo).
- **`post_id`**: Logical content item that may fan out into multiple schedules (per platform/variant).

Where these are not yet modeled in the product, we can:
- Start with **`asset_id`** and **`schedule_id`** as minimal entities.
- Use PostHog **groups** for `workspace_id`/`project_id` later.

---

## 2. North Star Metrics

These are the 3–5 primary metrics that describe success of the tools → planner → scheduler suite.

### 2.1 Weekly Cross-Workflow Active Creators (W-CWAC)

**Definition:**
Number of distinct **users per week** who:
1. Create or import at least one **asset** _and_
2. Add at least one **post or slot** in the **planner** _and_
3. Create at least one **scheduled post**.

**Why it matters:** Measures meaningful engagement with the full workflow.

**Implementation sketch (PostHog):**
- Event cohort where a user has all of:
  - `tool_asset_created` OR `tool_asset_imported`
  - `planner_post_created` OR `planner_slot_filled`
  - `schedule_created`
within the same 7-day window.

### 2.2 Weekly Activated Creators (WAC)

**Definition:**
Weekly count of users who **successfully publish** at least one scheduled post that originated from a Mayagen-created asset.

Conditions:
- A `schedule_published` event occurs in week X
- The schedule references an `asset_id`
- That `asset_id` has prior `tool_asset_created` in Mayagen.

**Why it matters:** Strong signal of value delivery: not only using tools, but shipping content.

### 2.3 Creator Workflow Retention (CWR, 4-week)

**Definition:**
Among users who were **Activated Creators** in week 0, what percentage **again** achieve activation (WAC) in weeks 1–4?

Variants:
- **N-week rolling retention** curves for WAC cohort.

**Why it matters:** Measures whether our workflows create repeat behavior, not just one-off experiments.

### 2.4 Average Assets-to-Schedule Conversion Rate (A2S)

**Definition (per week):**
For all assets created in week X, proportion that end up attached to at least one successful `schedule_published` event within 30 days.

> `A2S = (# unique asset_id with schedule_published within 30d) / (# unique asset_id created in week X)`

**Why it matters:** Captures how effective the tools and planner are at turning creation into scheduled output.

### 2.5 Planner-Assisted Scheduling Rate (PASR)

**Definition:**
% of scheduled posts per week that were **initiated from the planner** (e.g., user clicked "Schedule" from planner view) vs ad-hoc scheduler usage.

> `PASR = (# schedule_created with source = 'planner') / (# all schedule_created)`

**Why it matters:** Indicates whether the planner is actually being used as the orchestration surface.

---

## 3. Workflow-Centric Event Model

This section defines the **event taxonomy** with an emphasis on cross-tool workflows.

### 3.1 Global Event Conventions

Every event should include:
- `user_id` (if logged in) and/or `anonymous_id`
- `distinct_id` (PostHog’s primary ID — we can use `user_id` when logged in, `anonymous_id` otherwise)
- `workspace_id` / `team_id` (if applicable)
- `session_id`
- `timestamp` (ISO8601)
- `source` (e.g., `web_app`, `api`, `integration:<name>`)
- `ui_surface` (e.g., `editor`, `planner_calendar`, `scheduler_modal`)
- `experiment_variant` (if user is in any active experiment)


### 3.2 Key Workflows & Event Chains

We’ll define 4 canonical workflows and their event chains:

1. **Creation → Planner → Scheduler → Publish**
2. **Import → Planner → Scheduler → Publish**
3. **Planner-first → Creation → Scheduler → Publish**
4. **Scheduler-only (non-ideal baseline)**

Each workflow uses the same underlying events, but we’ll analyze them as **paths/funnels**.

#### 3.2.1 Creation → Planner → Scheduler → Publish

**Goal:** User designs a graphic, plans it in the content calendar, schedules it, and it publishes.

Event chain (ideal):
1. `tool_asset_created`
2. `planner_post_created` (with `asset_id` linked) OR `planner_slot_filled`
3. `schedule_created` (with `source = 'planner'` and `asset_id`)
4. `schedule_published`

We’ll measure:
- Drop-off at each step
- Time between steps (e.g., `time_asset_to_first_planned`, `time_planner_to_first_schedule`)

#### 3.2.2 Import → Planner → Scheduler → Publish

Event chain:
1. `tool_asset_imported`
2. `planner_post_created` / `planner_slot_filled`
3. `schedule_created`
4. `schedule_published`

Distinct from creation because `origin = 'import'`.

#### 3.2.3 Planner-first → Creation → Scheduler → Publish

Event chain:
1. `planner_post_created` with `asset_id = null`
2. `tool_asset_created` later linked to that planner post
3. `planner_post_updated` (`asset_id` set)
4. `schedule_created`
5. `schedule_published`

Important for understanding planner as the **brainstorming/briefing** entry point.

#### 3.2.4 Scheduler-only (non-ideal baseline)

Event chain:
1. `schedule_created` with `asset_origin = 'external'` and no planner involvement
2. `schedule_published`

We expect this to be common early; over time we want a higher share of planner/toll-linked schedules.


### 3.3 Event Specifications

Below is a compact but concrete spec for core events.

#### 3.3.1 Tool / Asset Events

1. **`tool_opened`**
   - **When:** User opens a creation tool (e.g., image editor, template gallery, AI generator).
   - **Properties:**
     - `tool_type`: `"image_editor" | "template_gallery" | "ai_generator" | "carousel_builder" | ...`
     - `entry_point`: `"homepage" | "planner" | "template" | "direct_link" | ...`
     - `project_id` (optional)

2. **`tool_asset_created`**
   - **When:** User saves/exports a new asset from a tool for the first time.
   - **Properties:**
     - `asset_id`
     - `tool_type`
     - `template_id` (if from template)
     - `origin`: always `"mayagen_tool"`
     - `format`: `"image" | "carousel" | "video" | ...`
     - `usage_intent`: `"social_post" | "story" | "ad" | ...` (if captured)

3. **`tool_asset_edited`**
   - **When:** User re-opens and saves changes to an existing asset.
   - **Properties:**
     - `asset_id`
     - `edit_type`: high-level classification like `"text_change"`, `"layout_change"`, `"color_change"` (optional)

4. **`tool_asset_imported`**
   - **When:** User uploads/imports an external asset into Mayagen.
   - **Properties:**
     - `asset_id`
     - `origin`: `"upload" | "drive" | "dropbox" | ...`
     - `format`

5. **`tool_asset_deleted`** (optional for now)
   - Track only if relevant for understanding churn or clutter.


#### 3.3.2 Planner Events

1. **`planner_opened`**
   - **When:** User views the planner/calendar/board view.
   - **Properties:**
     - `view_mode`: `"calendar" | "list" | "kanban" | ...`
     - `timeframe`: `"week" | "month" | ...`

2. **`planner_post_created`**
   - **When:** User creates a new planned content item (even if unscheduled).
   - **Properties:**
     - `plan_id`
     - `post_id`
     - `asset_id` (nullable)
     - `platforms`: array (e.g., `["instagram", "tiktok"]`)
     - `planned_date` (if user picked a tentative date/slot)
     - `entry_point`: `"planner" | "tool" | "import"`

3. **`planner_slot_filled`**
   - **When:** User fills a previously empty slot in the planner (e.g., clicking on a date cell and adding content).
   - **Properties:**
     - `plan_id`
     - `post_id`
     - `asset_id` (nullable)
     - `slot_date`

4. **`planner_post_updated`**
   - **When:** User updates a planner item (e.g., adds an asset, changes copy).
   - **Properties:**
     - `post_id`
     - `asset_id_before`
     - `asset_id_after`
     - `planned_date_before`
     - `planned_date_after`
     - `change_type`: e.g., `"add_asset" | "date_change" | "copy_edit"`

5. **`planner_post_deleted`** (optional)


#### 3.3.3 Scheduler Events

1. **`scheduler_opened`**
   - **When:** User opens the scheduling UI.
   - **Properties:**
     - `entry_point`: `"planner" | "tool" | "library" | "direct"`
     - `post_id` (nullable)
     - `asset_id` (nullable)

2. **`schedule_created`**
   - **When:** User confirms a schedule for a post to one or more platforms.
   - **Properties:**
     - `schedule_id`
     - `post_id` (nullable)
     - `asset_id` (nullable)
     - `asset_origin`: `"mayagen_tool" | "import" | "external_link" | "unknown"`
     - `platform`: single value per event (`"instagram" | "facebook" | ..."`)
     - `scheduled_time`
     - `source`: `"planner" | "tool" | "library" | "direct"`
     - `is_first_schedule_for_asset` (boolean, computed backend-side if possible)

3. **`schedule_updated`**
   - **When:** User changes time/platform/settings of a scheduled post.
   - **Properties:**
     - `schedule_id`
     - `change_type`: `"time_change" | "platform_change" | ...`

4. **`schedule_canceled`**
   - **When:** User cancels a scheduled post before publish.
   - **Properties:**
     - `schedule_id`
     - `reason` (if captured)

5. **`schedule_published`**
   - **When:** Mayagen (or a connected integration) confirms the scheduled content was successfully posted.
   - **Properties:**
     - `schedule_id`
     - `post_id` (nullable)
     - `asset_id` (nullable)
     - `platform`
     - `publish_time`
     - `status`: `"success" | "failed"`
     - `failure_reason` (if `status = failed`)

6. **`schedule_failed_retry`** (optional)
   - For delivery reliability analysis.


#### 3.3.4 Engagement & Retention Events

1. **`app_signed_up`** / **`app_logged_in`**
   - Standard auth events for journey baselines.

2. **`app_session_started`** / **`app_session_ended`** (optional)
   - Use PostHog built-ins where possible; otherwise track page views with `session_id`.

3. **`feature_tour_completed`**, `nux_checklist_completed` (if applicable)
   - Useful for activation experiments.


### 3.4 Event Properties for Workflow Analysis

To support the cross-tool focus, ensure these properties exist where reasonable:

- **`entry_point`**: Where the action started (`planner`, `tool`, `library`, `external_link`).
- **`asset_origin`**: `mayagen_tool` vs `import` vs `external`.
- **`is_first_time_user_of_feature`**: Boolean flag set backend-side where feasible, e.g., first time opening planner.
- **`device_type`**: `desktop | mobile_web` (for UX analysis).
- **`plan_complexity`**: approximate (e.g., number of posts in plan) for certain events if cheaply computed.

---

## 4. Activation, Conversion & Retention Definitions

### 4.1 Activation Definitions

We’ll maintain **3 levels of activation**:

1. **Tool Activation (T-ACT)**
   - A user is tool-activated when they create at least **1 asset** (`tool_asset_created`) in their first 7 days after signup.

2. **Workflow Activation (W-ACT)**
   - A user is workflow-activated when within 14 days of signup they:
     - Create or import an asset **and**
     - Create at least one schedule (regardless of publish outcome).

3. **Outcome Activation (O-ACT)**
   - A user is outcome-activated when within 21 days they:
     - Successfully publish at least one scheduled post that uses a Mayagen-created asset (WAC definition).

PostHog implementation:
- Use **cohorts** with property filters on event occurrence windows relative to `app_signed_up`.


### 4.2 Conversion Funnels

We care about the following key funnels:

1. **Signup → First Asset → First Planner Post → First Schedule → First Publish**
2. **First Asset → First Schedule (with/without planner)**
3. **Planner-first Journeys:** Planner Open → Planner Post → Schedule Created → Publish

Funnel metrics to track per cohort (e.g., acquisition channel, plan type):
- Step conversion rates
- Median/95th percentile time between steps


### 4.3 Retention Metrics

- **Weekly Active Users (WAU)**
  - Users with any product event in a week.

- **Weekly Workflow Active Users (W-WAU)**
  - Users with at least 1 event from each of: tool, planner, scheduler in a week.

- **Activated Creator Retention**
  - As described in CWR; measured at 1, 4, 8, 12-week intervals.

- **Feature Retention** (Planner, Scheduler individually)
  - e.g., users who used planner in week 0 and again in week N.

---

## 5. Analytics Stack & Implementation Notes

Assumption: **Next.js frontend** + **PostHog** as primary analytics.

### 5.1 Tracking Architecture

- **Client-side (Next.js + PostHog JS SDK)**
  - Track UI interactions: `tool_opened`, `planner_opened`, `scheduler_opened`, and most create/update events where they originate from the UI.
  - Maintain `anonymous_id` & `session_id` in localStorage/cookies.

- **Server-side / Backend**
  - Track events that reflect **ground truth** state changes:
    - `tool_asset_created` (on save/commit)
    - `tool_asset_imported`
    - `schedule_created`, `schedule_updated`, `schedule_canceled`
    - `schedule_published` (from scheduler job outcomes / platform webhooks).
  - Attach enriched properties (e.g., `is_first_schedule_for_asset`, `asset_origin`, plan complexity) that are easier to compute server-side.

- **Identity resolution**
  - Use `posthog.identify(user_id)` on login/signup to tie pre-auth events (`anonymous_id`) to `user_id`.
  - Ensure `distinct_id` strategy is consistent across frontend and backend.

### 5.2 PostHog Configuration

- **Event naming**
  - Use `snake_case` verbs + nouns as spec’d above.

- **Groups (if on PostHog scale)**
  - Group type `workspace` with `workspace_id`.
  - Potential future group `project` with `project_id`.

- **Feature flags & experiments**
  - Use for variations of planner/scheduler flows (e.g., nudges to move from tool → planner instead of tool → scheduler directly).

- **Data quality**
  - Create a simple **data contract**: for each event, specify required properties and default values.
  - Use PostHog’s schema tools or a lightweight JSON schema (stored in repo) that CI can lint for.

### 5.3 Recommended Supplementary Stack (Optional)

- **Data Warehouse (e.g., BigQuery / Snowflake)** if/when:
  - Need heavy joins across entities, e.g., LTV, revenue, and content performance from social networks.

- **dbt** for modeling curated tables:
  - `fct_assets`, `fct_schedules`, `fct_planner_posts`, `fct_workflow_activations`.

- **Reverse ETL** (e.g., PostHog integrations or Hightouch) for:
  - Bringing activation or risk scores back into Mayagen for in-app messaging.

---

## 6. Dashboard Layout (PostHog)

Design dashboards around the **north stars** and their driver metrics.

### 6.1 Dashboard 1 — Executive: Workflow Health

**Purpose:** One-glance view of cross-tool workflow performance.

Widgets (cards/graphs):
1. **North Stars (top row):**
   - Weekly Cross-Workflow Active Creators (W-CWAC)
   - Weekly Activated Creators (WAC)
   - Creator Workflow Retention (CWR 4-week) as a line chart
   - Assets-to-Schedule Conversion Rate (A2S)
   - Planner-Assisted Scheduling Rate (PASR)

2. **Funnel: Signup → Publish**
   - Visual funnel chart with conversion at each step.

3. **Workflow Mix**
   - Bar/stacked area: share of publishes by workflow type:
     - Creation → Planner → Scheduler
     - Import → Planner → Scheduler
     - Planner-first
     - Scheduler-only

4. **Time-to-Value**
   - Median days: Signup → First Asset, Signup → First Schedule, Signup → First Publish.


### 6.2 Dashboard 2 — Product: Tool & Planner Effectiveness

**Purpose:** Help PM/design understand where tools/planner underperform.

Widgets:
1. **Tool Engagement**
   - WAU using any tool (`tool_opened`/`tool_asset_created`) over time.
   - Breakdown by `tool_type`.

2. **Asset Lifecycle**
   - Assets created vs assets attached to planner vs assets scheduled vs assets published.

3. **Planner Usage & Depth**
   - WAU planner users (`planner_opened`).
   - Avg number of planner posts per active planner user per week.
   - % of planner posts that get scheduled.

4. **Path Analysis**
   - Path from `tool_asset_created` to downstream events; identify common drop-offs.

5. **Cohort Analysis**
   - Retention curves for users who used planner in week 0 vs those who didn’t.


### 6.3 Dashboard 3 — Scheduler & Delivery Reliability

**Purpose:** Monitor scheduling performance and post-delivery issues.

Widgets:
1. **Schedules Created vs Published**
   - Time series of `schedule_created` and `schedule_published` counts.

2. **Success Rate by Platform**
   - % `schedule_published` with `status = success` by `platform`.

3. **Failure Reasons**
   - Breakdown of `failure_reason` for failed schedules.

4. **Planner-Assisted vs Ad-hoc Schedules**
   - Time series and breakdown feeding into PASR.

5. **Repeat Scheduling**
   - # of users per week who schedule ≥2 posts, ≥5 posts.


---

## 7. Implementation Phasing

To keep this practical, roll out in 3 phases.

### Phase 1 — Minimal Cross-Workflow Tracking

- Implement the core events:
  - `tool_asset_created`, `tool_asset_imported`
  - `planner_opened`, `planner_post_created`
  - `scheduler_opened`, `schedule_created`, `schedule_published`
- Ensure `asset_id`, `post_id`, `schedule_id`, and `user_id` are wired correctly.
- Set up Dashboard 1 with **simplified** W-CWAC, WAC, A2S, PASR.

### Phase 2 — Enrichment & Planner Depth

- Add `planner_slot_filled`, `planner_post_updated`.
- Add `asset_origin`, `entry_point`, `source` properties.
- Start analyzing workflow types and time-to-value.

### Phase 3 — Retention & Experimentation

- Configure WAC-based cohorts and CWR retention views.
- Implement experiments focused on:
  - Nudging users from tool → planner (vs tool → scheduler-only).
  - Nudging planner-only users to schedule.
- Feed insights back into onboarding and UX.

---

## 8. Open Questions & Next Steps

A few decisions needed for full fidelity:

1. **Entity modeling:** Confirm existence/plan for `project_id`, `post_id`, and `plan_id` in the backend.
2. **Social performance data:** Will we ingest engagement metrics (likes, comments, etc.)? If yes, add `post_performance_synced` events.
3. **Team/workspace model:** If many users share a workspace, we may add workspace-level north stars (e.g., Active Creator Workspaces).

Once these are clarified, we can refine this v2 plan into a more formal **event dictionary** and JSON schemas, and backfill any historical metrics in PostHog/dbt models where data already exists.
