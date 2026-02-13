# Product Mockups → Campaign Funnel Experiments v1

Owner: @seo-growth  
Last updated: 2026-02-13

Context: Product Mockups should be a **campaign entry point**, not a download dead-end. This doc turns the existing flow specs (`product-mockups-flow-v1`, `product-mockups-mockup-to-campaign-flow-v1`, friction audit v1) into concrete, testable experiments tied to Analytics v2.

## Core Funnel

1. Visitor lands on `/product-mockups/`
2. Creates at least one mockup
3. Adds mockup(s) into an ad set or social post template
4. Opens Campaign Mode in planner
5. Schedules first campaign (≥1 post)
6. Schedules additional posts in the same campaign and/or follow-up weeks

Primary success signals:
- **P1:** `campaign_created_from_mockups` sessions per 100 visitors to `/product-mockups/`
- **P2:** `campaign_scheduled_from_mockups` (≥1 scheduled post) per 100 visitors
- **P3:** Median time from first mockup → first scheduled post in Campaign Mode
- **P4:** % of campaigns that include ≥2 posts and ≥1 follow-up post beyond day 1

Guardrails:
- Page-level engagement (bounce, scroll depth, time on page)
- Mockup completion rate (don’t hurt the core tool)

---

## Experiment A — Campaign‑First Landing Page CTAs

**Hypothesis**  
If we reframe Product Mockups as a **campaign builder** instead of a download tool, more users will continue into planner/scheduler and schedule at least one campaign.

**Change**
- Hero H1/H2 emphasize "Product Mockups for Ad Campaigns" and the create → plan → schedule flow (as defined in `product-mockups-landing-seo-structure-v1`).
- Primary hero CTA: **“Create mockups & start a campaign”** → opens mockup flow with an explicit step 2: "Turn these into ads & schedule a campaign".
- Secondary hero CTA: **“Just download mockups”** → current behavior for users who only want assets.
- Add mid‑page flow strip visually showing: **Mockups → Ads → Campaign Mode**.

**Variant(s)**
- Control: current landing (download‑first framing).
- Variant A1: suite‑first hero copy + campaign‑first CTAs + flow strip.

**Primary metric**
- Uplift in `campaign_mode_opened_from_product_mockups_landing` per 100 visitors.

**Secondary metrics**
- `campaign_created_from_mockups`
- `campaign_scheduled_from_mockups`
- Mockup completion rate (guardrail)

**Measurement notes**
- Ensure referrer/context is tagged so we know flows originated from `/product-mockups/` hero vs other CTAs.

---

## Experiment B — Post‑Mockup "Use in Ads & Campaign" Nudge

**Hypothesis**  
After a user finishes a mockup, a prominent **“Use in ads & campaign”** CTA will move them into the ads wizard and Campaign Mode instead of stopping at export.

**Change**
- On mockup completion screen:
  - Primary action: **“Use in ads & campaign”** → opens 3‑step wizard (Mockups → Ads → Schedule) defined in `product-mockups-mockup-to-campaign-flow-v1`.
  - Secondary action: **“Download files”** (still visible but visually weaker).
- Add short explainer: "Turn these mockups into a ready‑to‑schedule ad campaign in a few clicks."

**Variant(s)**
- Control: download‑first completion screen.
- Variant B1: campaign‑first completion screen.

**Primary metric**
- Uplift in `campaign_wizard_started_from_mockups_completion` per 100 mockup completions.

**Secondary metrics**
- `campaign_scheduled_from_mockups`
- Time from completion → first scheduled post (median)
- Downloads per completion (guardrail)

---

## Experiment C — Campaign‑Focused Planner Mode from Mockups

**Hypothesis**  
A simplified **Campaign Mode** in planner, entered from Product Mockups with pre‑filled posts, will increase campaign scheduling vs dropping users into the full calendar.

**Change**
- When entering planner from the mockups ads wizard:
  - Open a scoped Campaign Mode view (per `product-mockups-mockup-to-campaign-flow-v1` and friction audit v1) with:
    - A limited date range (e.g., 7–14 days).
    - Pre‑filled draft posts using the selected mockups.
    - One primary CTA: **“Schedule this campaign”** that bulk‑schedules all drafts with editable times.
- Keep an escape hatch to the full calendar for advanced users.

**Variant(s)**
- Control: jump directly from mockups to full planner calendar.
- Variant C1: scoped Campaign Mode view.

**Primary metric**
- `campaign_scheduled_from_mockups_campaign_mode` per 100 `campaign_wizard_started_from_mockups_completion`.

**Secondary metrics**
- Time to first scheduled post.
- Number of posts per campaign.
- % of users that exit to full calendar (guardrail/insight).

---

## Experiment D — Multilingual Campaign as an Optional Boost

**Hypothesis**  
Positioning 100+ languages as an **optional reach boost** (1–2 extra languages) with grouped variants will improve multilingual adoption without overwhelming users.

**Change**
- In the ads wizard and Campaign Mode:
  - Default to 1 base language.
  - Add a simple control: **“+ Add language (optional)”** with 1–2 pre‑suggested languages based on location/brand settings.
  - In planner, show language variants grouped under each base post (not separate tiles).
- Landing page & in‑product copy frame languages as "1–2 extra languages for key campaigns" instead of "100+" everywhere.

**Variant(s)**
- Control: current multilingual behavior (if any) or no explicit multilingual integration in this flow.
- Variant D1: optional, grouped multilingual behavior.

**Primary metric**
- `campaign_scheduled_multilingual_from_mockups` per 100 mockup‑origin campaigns.

**Secondary metrics**
- Time to schedule (must not regress significantly vs mono‑language).
- % of users adding ≥1 language.

---

## Experiment E — Follow‑Up Campaign Suggestions

**Hypothesis**  
Right after scheduling the first campaign from Product Mockups, suggesting a small follow‑up set (e.g., "Follow‑up offer", "Retargeting", "Review request") will increase ongoing planner use.

**Change**
- After a user schedules a mockup‑origin campaign, show a confirmation screen with:
  - Summary: posts, dates, channels.
  - A suggestion strip: **“Plan your follow‑up”** with 2–3 recommended campaign templates.
  - CTA: **“Add follow‑up posts”** → opens Campaign Mode pre‑filtered to 7–14 days after the main campaign.

**Primary metric**
- `followup_campaign_created_from_mockups` per 100 mockup‑origin campaigns.

**Secondary metrics**
- Weekly active planner users with ≥2 campaigns in 30 days originating from mockups.

---

## Rollout & Prioritization

Suggested order (once analytics wiring is ready):

1. **Experiment B** — closest to the core "don’t stop at download" problem; high leverage, relatively low complexity.
2. **Experiment C** — required to make B truly effective (Campaign Mode must feel easier than full calendar).
3. **Experiment A** — align landing framing once the in‑product flow is working.
4. **Experiment D** — layer multilingual as an optional boost.
5. **Experiment E** — extend into retention and ongoing planner use.

This document should be linked from `mayagen/tasks/ACTIVE.md` under **Product Mockups Flow** and used as the source of truth for growth experiments tied to this funnel.