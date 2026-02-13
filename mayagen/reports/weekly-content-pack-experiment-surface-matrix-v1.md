# Weekly Content Pack Experiment — Surface & Messaging Matrix (v1)

**Owner:** @content-lead  
**Partners:** @growth, @product-ux  
**Related docs:**
- Growth v2: `/mayagen/reports/growth-strategy-v2.md`
- Spec v1: `/mayagen/reports/weekly-content-pack-experiment-spec-v1.md`
- Copy v1–v2: `/mayagen/reports/weekly-content-pack-experiment-copy-v1.md`, `/mayagen/reports/weekly-content-pack-experiment-copy-v2.md`
- Microcopy v1: `/mayagen/reports/weekly-content-pack-microcopy-v1.md`
- Email & in-app sequence v1–v2: `/mayagen/reports/weekly-content-pack-experiment-email-sequence-v1.md`, `/mayagen/reports/weekly-content-pack-experiment-email-sequence-v2.md`

---

## 1. Core Story (Single Source of Truth)

**Spine:** create → plan → schedule — in 100+ languages, without calendar chaos.

Every Weekly Content Pack surface should reinforce:

- **Create** — Mayagen suggests ready-to-edit memes, posts, and mockups that match your brand and upcoming moments.
- **Plan** — you review and tweak a small set of posts inside a focused, low-clutter planner state (pack view, Launch Week-like view, or campaign mode).
- **Schedule** — you commit the pack to your calendar in one or two decisive actions, with grouped language variants instead of duplicate clutter.
- **Languages** — 100+ languages are framed as an **optional reach boost**: 1–3 extra languages per pack, grouped under each base post.

Guardrails:
- Avoid generic “AI social media assistant” phrasing; be concrete about outcomes: *a live calendar*, *a full launch week*, *a week of posts scheduled*.
- Always anchor power in **speed and clarity** ("a week of posts in minutes") rather than raw feature lists.

---

## 2. Surface Matrix

This matrix defines the minimum messaging requirements per surface. Detailed copy blocks live in `copy-v2` and `email-sequence-v2`; this doc is the structural map.

### 2.1 Dashboard Banner (Global)

**Goal:** Turn curious or inactive users into pack explorers.

- **Primary message:** Weekly packs turn ideas and assets into a scheduled week of posts.
- **Required elements:**
  - Reference to **create → plan → schedule**.
  - Promise of a concrete outcome (e.g., "your next week of posts scheduled").
  - Soft mention of 100+ languages as an optional upgrade ("add 1–3 extra languages when you’re ready").
- **CTA variants (for experiments):**
  - "Open this week’s content pack"
  - "Plan your week in minutes"
  - "See posts we’ve drafted for you"

### 2.2 Planner Empty State

**Goal:** Convert an empty calendar into a Weekly Content Pack entry point.

- **Primary message:** You don’t need to start from scratch — start from this week’s pack.
- **Required elements:**
  - Emphasis on **speed** and **simplicity** ("one click to fill your week").
  - Clear explanation that you can edit before scheduling.
  - Multilingual framed as *later* in the flow, not a prerequisite.
- **CTA:**
  - Single, strong CTA: "Use this week’s content pack".

### 2.3 Pack Detail View (In-App)

**Goal:** Help users understand what’s inside a pack and commit to planning with it.

- **Primary message:** Show the shape of the week — not just a list of assets.
- **Required elements:**
  - Short summary (e.g., "7 posts for this week: 3 memes, 2 product highlights, 2 reminders").
  - Visual grouping by day/slot to hint at the calendar outcome.
  - A short explanatory line about languages: "Start in one language; add 1–3 more later without cluttering your calendar."  
- **CTA stack:**
  - Primary: "Plan this week with this pack".
  - Secondary: "Preview posts".

### 2.4 Planner “Pack-loaded” State

**Goal:** Bridge from draft pack → committed schedule.

- **Primary message:** You are a small edit pass away from a scheduled week.
- **Required elements:**
  - A concise checklist (e.g., "Review posts", "Add languages (optional)", "Schedule week").
  - Clear indication that posts are still drafts until they hit "Schedule".
  - Language grouping explanation: badges or summary like "En: 7 posts • Es: 7 grouped variants".
- **CTA:**
  - Single primary CTA: "Schedule this week" (mirrors Launch Week / Campaign Mode patterns).

### 2.5 Post-Schedule Confirmation

**Goal:** Make the outcome feel real and invite the next habit.

- **Primary message:** You now have a real, scheduled week — and can repeat this pattern.
- **Required elements:**
  - Explicit statement of outcome ("7 posts scheduled for next week").
  - Optional mention of languages if used ("in English + 2 extra languages").
  - Next-step nudges: bookmark the pack, edit individual posts, or duplicate for another week.

---

## 3. Segment-Specific Emphasis

Segments (from `email-sequence-v2`):
- New/low-activity
- Inconsistent
- Power users

For each surface, the same spine applies, but emphasis shifts:

- **New/low-activity:**
  - Emphasize reassurance and speed: "You don’t need a content plan yet; start with a single week."  
  - calendar framing: "a light, guided week" rather than "campaign".
- **Inconsistent:**
  - Emphasize habit: "One weekly pack → a consistent calendar."  
  - nudge to let Mayagen handle the heavy lifting: "We’ll generate posts; you do the final pass."  
- **Power users:**
  - Emphasize control and leverage: "Treat this week’s pack as a starting set; customize and save as your own template."  
  - Mention languages as reach and testing: "Add a couple of languages to see which markets respond."  

Copy blocks for each segment are defined in the v2 docs; this matrix ensures we don’t drift from the shared story.

---

## 4. Cross-Tool Consistency (Meme, Logo, Mockups)

Weekly Content Packs must feel aligned with other free tools and flagship flows:

- **Meme Generator:** Packs often include memes; messaging should echo the meme flow: meme → post → planner → scheduled week.
- **Logo Maker:** Packs should reuse the "Launch Week" story: logo → launch assets → scheduled launch week.
- **Product Mockups:** Packs should complement campaign templates: mockup → ad set → scheduled campaign.

For all three, Weekly Content Packs are framed as:
- A **faster way** to get from asset to calendar.
- A **lighter cognitive load**: user edits a curated set instead of inventing everything from scratch.
- A unifying pattern: **create → plan → schedule**, with multilingual as a small, optional upgrade.

---

## 5. Implementation Checklist for Messaging

Before the experiment runs live, ensure:

- [ ] Each surface (dashboard, planner empty, pack detail, planner pack-loaded, confirmation) has copy that explicitly reflects the spine **create → plan → schedule**.
- [ ] 100+ languages are framed consistently as 1–3 extra languages, grouped variants, and never as a required step.
- [ ] CTAs match the target behavior per surface and segment (no duplicate or conflicting CTAs).
- [ ] Copy in this matrix is kept in sync with `copy-v2`, `microcopy-v1`, and `email-sequence-v2`.
- [ ] Growth and analytics teams agree on which surfaces are in-scope for early experiments and which CTAs will be A/B tested first.

This doc should be used as the structural reference when wiring or reviewing any Weekly Content Pack messaging, both in-app and via email.