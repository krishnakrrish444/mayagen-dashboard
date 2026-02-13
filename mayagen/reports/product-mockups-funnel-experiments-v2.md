# Product Mockups → Campaign Funnel Experiments v2 (Analytics‑Aligned)

Owner: @seo-growth  
Last updated: 2026-02-13

Context: v1 defined the right experiments for turning Product Mockups into a **campaign entry point**. v2 makes each experiment explicitly actionable by:
- Binding it to concrete Analytics v2 events from `/mayagen/reports/product-mockups-analytics-and-metrics-v1.md`.
- Calling out the primary metric and guardrails using shared definitions.
- Making it clear how each experiment ladders up to the weekly habit story (planner usage with `source = "product_mockups"`).

Core funnel (unchanged):
1. Visitor lands on `/product-mockups/` (`product_mockups_landing_viewed`).
2. Creates ≥1 mockup (`product_mockup_created`).
3. Chooses a campaign path (`campaign_wizard_opened_from_product_mockups`).
4. Enters Campaign Mode (`campaign_mode_opened_from_product_mockups`).
5. Schedules ≥1 post in a campaign (`campaign_scheduled_from_product_mockups`).
6. Returns to planner with more scheduled posts/campaigns in later weeks (`user_weekly_active_planner_from_product_mockups`).

Primary north star for this funnel:
> Creators who turn a mockup into a scheduled campaign **and** come back to schedule again (weekly planner habit from Product Mockups).

---

## Experiment A — Campaign‑First Landing Page CTAs

**Goal**  
Reframe `/product-mockups/` as a **campaign builder**, not just a download tool, and increase the share of visitors who enter the campaign funnel.

**Change (from v1, now analytics‑bound)**
- Hero H1/H2: suite‑first, campaign‑framed (see `product-mockups-landing-seo-structure-v1.md`).
- Primary CTA in hero: **"Create mockups & start a campaign"**.
  - Fires `product_mockups_start_from_landing` with `cta_label = "create_mockups_and_start_campaign"`.
- Secondary CTA: **"Just download mockups"** (keeps current behavior; still fires `product_mockups_start_from_landing` but with different `cta_label`).
- Flow strip that visually explains **Mockups → Ads → Campaign Mode**, making the planner/scheduler spine explicit.

**Variant design**
- Control: current landing (download‑first framing, existing CTAs).
- Variant A1: campaign‑first hero copy + campaign CTA + flow strip.

**Primary metric**
- **A1.1**: `campaign_mode_opened_from_product_mockups / product_mockups_landing_viewed`
  - Interpretation: "Of visitors to `/product-mockups/`, how many actually enter Campaign Mode?"

**Secondary metrics**
- **A1.2**: `campaign_wizard_opened_from_product_mockups / product_mockup_created`  
  (does the new framing drive more mockup creators into the wizard?)
- **A1.3**: `campaign_scheduled_from_product_mockups / product_mockups_landing_viewed`.
- **A1.4 (guardrail)**: `product_mockup_created / product_mockups_landing_viewed` and scroll-depth/time‑on‑page; we must not tank core mockup creation or page engagement.

**Weekly‑habit link**
- Track `user_weekly_active_planner_from_product_mockups` by `experiment_variant` to see if campaign‑first framing leads to more sustained planner use, not just more first campaigns.

---

## Experiment B — Post‑Mockup "Use in Ads & Campaign" Nudge

**Goal**  
Shift post‑mockup behavior from "download and disappear" to "continue into ads wizard and schedule a campaign".

**Change**
- On the mockup completion screen:
  - Primary CTA: **"Use in ads & campaign"** → opens the 3‑step wizard (`campaign_wizard_opened_from_product_mockups` with `entry_point = "post_mockup"`).
  - Secondary CTA: **"Download files"** → keeps `product_mockup_downloaded` but visually demoted.
- Short explainer under the primary CTA: "Turn these mockups into a ready‑to‑schedule ad campaign in a few clicks."

**Variant design**
- Control: download‑first completion screen; mockup completion heavily emphasizes export.
- Variant B1: campaign‑first completion screen as above.

**Primary metric**
- **B1.1**: `campaign_wizard_opened_from_product_mockups / product_mockup_created`  
  (specifically among users whose latest event is `product_mockup_created` in this session).

**Secondary metrics**
- **B1.2**: `campaign_scheduled_from_product_mockups / campaign_wizard_opened_from_product_mockups`.
- **B1.3**: median `time_to_first_scheduled_post_seconds` (from first `product_mockups_landing_viewed` or first `product_mockup_created`, whichever we standardize on in Analytics v2).
- **B1.4 (guardrail)**: `product_mockup_downloaded / product_mockup_created` — we must not break the core "I just need files" path.

**Weekly‑habit link**
- Compare `user_weekly_active_planner_from_product_mockups` for users who ever clicked `entry_point = "post_mockup"` vs those who only downloaded; this tells us whether the nudge actually seeds ongoing planner behavior.

---

## Experiment C — Campaign‑Focused Planner Mode from Mockups

**Goal**  
Make scheduling from Product Mockups feel like a short, guided step rather than dropping users into a complex calendar.

**Change**
- Entering planner from the mockups ads wizard opens a scoped Campaign Mode view:
  - Emits `campaign_mode_opened_from_product_mockups` with `campaign_template` (e.g., "launch_week", "evergreen_offer").
  - Shows a 7–14 day campaign‑scoped view with pre‑filled draft posts, a persistent header/stepper, and a single primary CTA **"Schedule this campaign"**.
  - Uses the base‑post + grouped language‑variants model from `product-mockups-mockup-to-campaign-planner-multilingual-ux-v2.md`.

**Variant design**
- Control: direct jump from mockups into the full planner calendar (no scoped Campaign Mode).
- Variant C1: scoped Campaign Mode, as per the UX specs.

**Primary metric**
- **C1.1**: `campaign_scheduled_from_product_mockups / campaign_mode_opened_from_product_mockups`.

**Secondary metrics**
- **C1.2**: median `time_to_first_scheduled_post_seconds` for mockup‑origin campaigns.
- **C1.3**: average `post_count` per `campaign_scheduled_from_product_mockups`.
- **C1.4 (guardrail/insight)**: share of users who immediately exit to full calendar from Campaign Mode (via a dedicated "open_full_calendar" event or property on `campaign_mode_opened_from_product_mockups`).

**Weekly‑habit link**
- Compare `user_weekly_active_planner_from_product_mockups` and `campaign_revisit_from_product_mockups` between control and C1 to confirm that the simpler first‑run experience leads to more returning campaigns.

---

## Experiment D — Multilingual Campaign as an Optional Boost

**Goal**  
Increase multilingual adoption while keeping the calendar tidy and time‑to‑scheduled‑campaign within our 10–15 minute target.

**Change**
- In the ads wizard and Campaign Mode:
  - Default to one base language.
  - Provide a **"+ Add language (optional)"** control with sensible, low‑friction suggestions (1–3 languages) based on location/brand.
  - Group variants under each base post in Campaign Mode (shared pattern with Logo Maker).
- Copy throughout: languages are a **small reach upgrade**, not extra work.

**Variant design**
- Control: existing behavior (no explicit multilingual flow or less structured variants).
- Variant D1: optional, grouped multilingual UX as described in the planner/multilingual spec.

**Primary metric**
- **D1.1**: `campaign_scheduled_multilingual_from_product_mockups / campaign_scheduled_from_product_mockups`.

**Secondary metrics**
- **D1.2**: delta in median `time_to_first_scheduled_post_seconds` vs mono‑language campaigns.
- **D1.3 (guardrail)**: drop‑off in `campaign_scheduled_from_product_mockups` for sessions where a user opened the `+ Add language` dialog but abandoned before scheduling.

**Weekly‑habit link**
- Track whether multilingual campaign creators are more likely to become `user_weekly_active_planner_from_product_mockups` (i.e., does a successful multilingual launch correlate with stronger planner habit, or does it create too much complexity?).

---

## Experiment E — Follow‑Up Campaign Suggestions

**Goal**  
Use the moment right after a first scheduled campaign to seed the next one, building a rhythm of planning beyond a single launch.

**Change**
- After `campaign_scheduled_from_product_mockups` fires for a first‑time campaign:
  - Show a confirmation layer summarizing the campaign.
  - Suggest 2–3 follow‑up templates (e.g., "Follow‑up offer", "Retargeting", "Review request").
  - CTA: **"Add follow‑up posts"** → opens Campaign Mode pre‑filtered to 7–14 days after the scheduled campaign.
  - Emit `campaign_followup_suggestion_shown_from_product_mockups` and `followup_campaign_created_from_product_mockups` when accepted and scheduled.

**Variant design**
- Control: simple confirmation, no explicit follow‑up suggestions.
- Variant E1: confirmation + follow‑up templates as above.

**Primary metric**
- **E1.1**: `followup_campaign_created_from_product_mockups / campaign_scheduled_from_product_mockups`.

**Secondary metrics**
- **E1.2**: % of mockup‑origin users who become `user_weekly_active_planner_from_product_mockups` within 30 days.
- **E1.3 (guardrail)**: check for any negative impact on satisfaction (e.g., users closing the confirmation immediately, or support signals if tracked) when we push follow‑ups too hard.

---

## Rollout & Dashboard Integration

Recommended rollout order (unchanged, now with explicit metrics):
1. **Experiment B** — fix the download dead‑end; measure B1.1/B1.2/B1.3.
2. **Experiment C** — make Campaign Mode easy; measure C1.1/C1.2/C1.3.
3. **Experiment A** — align landing framing; measure A1.1/A1.2.
4. **Experiment D** — add multilingual reach; measure D1.1/D1.2.
5. **Experiment E** — extend into retention; measure E1.1/E1.2.

For dashboards (using the Analytics & Metrics v1 spec):
- **Founder View** should surface A1.1, B1.1, C1.1, and the final north star (share of users who both schedule a campaign and become `user_weekly_active_planner_from_product_mockups`).
- **PM/UX View** should show step drop‑offs and experiment comparisons by `experiment_variant`, with a dedicated section for mockup‑origin flows so Product Mockups feels like a first‑class campaign source.

This v2 doc supersedes v1 as the source of truth for Product Mockups growth experiments and should be used alongside the analytics spec when wiring events and dashboards.