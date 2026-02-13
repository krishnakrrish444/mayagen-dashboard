# Product Mockups → Campaign Funnel — Analytics & Metrics v1

## 1. Funnel Overview

Primary flow we care about:

1. **Landing**: Visitor arrives on `/product-mockups/`
2. **Creation**: User creates at least one mockup in the Product Mockups tool
3. **Campaign Intent**: User chooses to "Use in ads & campaign" (or equivalent CTA)
4. **Campaign Mode**: User enters Campaign Mode planner view / wizard
5. **Scheduling**: User schedules at least one post in the campaign
6. **Weekly Habit**: User returns and has at least one additional campaign or campaign post scheduled in a later week

The north star for this funnel: **"Creators who turn a mockup into a scheduled campaign and come back to schedule again"**.

---

## 2. Core Events & Properties

These events assume Analytics v2 conventions (PostHog or equivalent) and should be wired consistently with planner/scheduler and weekly habit work elsewhere.

### 2.1 Landing / Discovery

- **`product_mockups_landing_viewed`**
  - `source`: `"seo" | "direct" | "referral" | "app" | "other"`
  - `experiment_variant`: for landing-page experiments (A/B/C)
  - `cta_block`: if view is from a specific section (e.g., top hero vs campaign strip)

- **`product_mockups_start_from_landing`**
  - Fired when a user clicks the primary "Start designing" / equivalent CTA on `/product-mockups/`.
  - Properties:
    - `cta_label`
    - `experiment_variant`

### 2.2 Mockup Creation

- **`product_mockup_created`**
  - Fired when a mockup is successfully generated (not just when the editor opens).
  - Properties:
    - `mockup_type`: `"ecommerce_product" | "lifestyle" | "saas_ui" | "social_ad" | "other"`
    - `from_landing`: boolean
    - `session_mockup_count`: number of mockups created in this session

- **`product_mockup_downloaded`**
  - Properties:
    - `file_format`: `"png" | "jpg" | "svg" | ...`
    - `download_primary`: whether this was the main post-mockup CTA

### 2.3 Campaign Intent & Wizard

- **`campaign_wizard_opened_from_product_mockups`**
  - Fired when the user chooses the "Use in ads & campaign" path.
  - Properties:
    - `entry_point`: `"post_mockup" | "landing_campaign_cta" | "editor_toolbar"`
    - `mockup_count`: how many mockups are being brought into the wizard

- **`campaign_wizard_step_completed`**
  - Fired on each step of the 3-step wizard described in the UX spec.
  - Properties:
    - `step`: `"Mockups" | "Ads" | "Schedule"`
    - `completion_state`: `"success" | "skipped" | "abandoned"`

- **`campaign_mode_opened_from_product_mockups`**
  - Fired when the user enters Campaign Mode planner view from this funnel.
  - Properties:
    - `campaign_template`: name/ID of the campaign template (e.g., "Launch", "Promo Week")

### 2.4 Scheduling & Multilingual

- **`campaign_scheduled_from_product_mockups`**
  - Fired when the user schedules at least one post as part of this campaign flow.
  - Properties:
    - `post_count`
    - `channel_count`
    - `time_to_first_scheduled_post_seconds` (from first landing view or from first mockup creation; decide globally and be consistent)

- **`campaign_scheduled_multilingual_from_product_mockups`**
  - Fired when the campaign includes at least one language variant beyond the base language.
  - Properties:
    - `language_count`
    - `base_language`

### 2.5 Weekly Habit / Retention

- **`campaign_revisit_from_product_mockups`**
  - Fired when a user returns to a campaign originally started from Product Mockups.
  - Properties:
    - `days_since_first_campaign`
    - `new_posts_added`

- **`user_weekly_active_planner_from_product_mockups`**
  - Weekly rollup-style event or derived metric tagged with `source = "product_mockups"`.

---

## 3. Key Metrics & Targets

These are the core metrics to track and improve over time.

### 3.1 Conversion Through the Funnel

1. **Landing → Mockup Created**
   - Metric: `mockup_creators / landing_visitors`
   - Target: aim for **20–30%**+ for high-intent SEO traffic.

2. **Mockup Created → Campaign Intent**
   - Metric: `campaign_wizard_opened_from_product_mockups / product_mockup_created`
   - Target: get at least **25–35%** of creators to try the campaign path.

3. **Campaign Intent → Scheduled Campaign**
   - Metric: `campaign_scheduled_from_product_mockups / campaign_wizard_opened_from_product_mockups`
   - Target: **40–60%** once UX is stable (higher is better; guardrail for complexity).

4. **Scheduled Campaign → Weekly Habit**
   - Metric: share of users who have at least one additional campaign or post scheduled in a subsequent week.
   - Target: at least **30%** of first-time campaign schedulers return within 30 days.

### 3.2 Time to First Scheduled Campaign

- Metric: median `time_to_first_scheduled_post_seconds` from first Product Mockups landing to first scheduled post in a campaign.
- Goal: keep this within **10–15 minutes** for first-timers; treat significant increases as friction.

### 3.3 Multilingual as Reach Booster

- Metric: `campaign_scheduled_multilingual_from_product_mockups / campaign_scheduled_from_product_mockups`
- Target: **15–25%** adoption of multilingual campaigns once UX and language presets are good.
- Guardrail: watch for calendar overwhelm (drop-offs after adding languages or confusion in Campaign Mode).

---

## 4. Dashboard Views

### 4.1 Founder View (High Level)

Widgets/sections:

1. **Funnel Overview**
   - Bars or steps from Landing → Mockup Created → Campaign Wizard → Scheduled Campaign → Returning Campaign Users.

2. **Time to First Scheduled Campaign**
   - Median + distribution chart, segmented by source (`seo`, `direct`, etc.).

3. **Weekly Active Planner Users from Product Mockups**
   - Trend line of `user_weekly_active_planner_from_product_mockups`.

4. **Multilingual Adoption**
   - Share of campaigns that include multiple languages; by week.

### 4.2 PM/UX View (Detail)

1. **Step Drop-offs in Campaign Wizard**
   - Completion vs abandonment rates per step (`Mockups`, `Ads`, `Schedule`).

2. **Mockup Types & Campaign Conversion**
   - Conversion to scheduled campaign broken down by `mockup_type`.

3. **Experiment Comparison**
   - Compare funnel metrics by `experiment_variant` for specific A/B tests.

---

## 5. How This Connects to Weekly Habit

- Tag all planner/scheduler events spawned from this funnel with `source = "product_mockups"`.
- Ensure the same definitions of **weekly active planner user** and **scheduled post** are used across Meme Generator, Logo Maker, Product Mockups, and Weekly Content Packs.
- This lets us answer: *"Of all users whose first serious contact was Product Mockups, how many develop a weekly scheduling habit?"*

---

## 6. Next Steps

1. Align event names and properties with Analytics v2 (`/mayagen/reports/analytics-plan-v2.md`).
2. Update `/mayagen/reports/product-mockups-funnel-experiments-v1.md` to reference these metrics explicitly per experiment.
3. Once events are wired, build two dashboards: **Founder View** and **PM/UX View**, using this doc as the spec.
