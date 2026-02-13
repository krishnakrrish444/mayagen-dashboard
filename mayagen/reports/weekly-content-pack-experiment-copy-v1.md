# Weekly Content Pack Experiment — Messaging & Copy v1

This document refines the core messaging for the Weekly Content Pack experiment, with variants by segment and surfaces. The through-line on every surface is:

> Mayagen helps you **create → plan → schedule** a week of posts (in up to 100+ languages) without starting from a blank page.

---

## 1. Core Value Proposition (Global)

**Headline (global theme):**
- "Skip the blank page. Get a weekly content pack you can schedule in one review."

**Subhead options:**
- "Mayagen creates a balanced mix of posts for your brand, plans them on your calendar, and lets you schedule everything in a few clicks — in your main language, plus 1–2 more if you like."
- "From idea to scheduled posts: Mayagen drafts this week’s memes, stories, and promos, suggests days and times, and lets you approve everything in one place."

**Supporting bullets:**
- "3–7 posts per week tailored to your channels and audience."
- "Suggested days and times, ready to review on your calendar."
- "Optional variants in 100+ languages, grouped so your planner stays clean."
- "One review to **create → plan → schedule** your week."

Tone guidelines:
- Keep language plain and concrete ("posts," "calendar," "week")
- Show the outcome (a week of scheduled posts) instead of the mechanism ("AI automation").
- Treat multilingual as a bonus layer of reach, not a requirement.

---

## 2. Segment Variants

### 2.1 New but activated users
*Segment:* Recently signed up, connected at least one channel, has created or scheduled 1–3 posts.

**Angle:** "You’ve proven you can publish; now let Mayagen keep you consistent."

**In-app banner copy:**
- Title: **"Turn this week into a full content plan"**
- Body: "You’ve already published with Mayagen. Let us draft a weekly content pack — memes, story posts, and simple promos — and drop them onto your calendar. Review once, schedule the week."
- CTA: **"Generate this week’s pack"**
- Secondary: "Not now"

**Modal copy (key section):**
- Section title: **"Create → plan → schedule in one pass"**
- Body: "We create 3–7 posts for your brand, plan them across your channels, and let you schedule them in a single review. Start in your main language, then add 1–2 more from 100+ supported languages if you want extra reach."


### 2.2 Returning but inconsistent users
*Segment:* Has posted before, but no scheduled posts in the current/coming week.

**Angle:** "You don’t need a big plan; you need this week sorted."

**Dashboard nudge:**
- Title: **"Nothing scheduled this week"**
- Body: "Let Mayagen propose a weekly content pack — a simple mix of memes, story posts, and promos — already placed on your calendar. Tweak what you like, then schedule everything in a few clicks."
- CTA: **"See this week’s pack"**

**Email subject & preview variants:**
- Subject options:
  - "We drafted this week’s posts for you"
  - "Your weekly content pack is ready to review"
  - "Want a full week of posts without the blank page?"
- Preview options:
  - "Create → plan → schedule this week’s posts in one pass."
  - "3–7 posts, suggested times, optional variants in 100+ languages."

**Email body (variant A — inconsistent users):**
> Hi {{first_name}},
>
> You’ve posted with Mayagen before — but it’s easy for the week to get away from you.
>
> This time, let Mayagen handle the hard part.
>
> **Your weekly content pack includes:**
> - 3–7 posts (memes, story posts, and simple promos)
> - Suggested days and times on your calendar
> - Optional variants in 100+ languages (grouped so your planner stays clean)
>
> You can review everything in one place, edit any post, and schedule your week in a few clicks.
>
> **Create → plan → schedule — without starting from a blank page.**
>
> 👉 **Open this week’s content pack**
>
> — The Mayagen team
>
> PS: As you publish more, your packs get smarter about what works for your audience.


### 2.3 Highly active / power users
*Segment:* Publishes regularly, has multiple channels and possibly multiple languages.

**Angle:** "You already publish; we’ll save you time on planning and variants."

**In-app copy (planner hint):**
- Title: **"Want a head start on next week?"**
- Body: "Let Mayagen draft a weekly content pack based on what’s working — ideas, times, and language variants — then you take it from there."
- CTA: **"Generate next week’s pack"**

**Email body (variant B — power users):**
> Hi {{first_name}},
>
> You’re already publishing regularly with Mayagen.
>
> To save you time on planning and variants, we can draft your next weekly content pack for you.
>
> **Here’s what you get in a few clicks:**
> - 3–7 post ideas inspired by what’s worked for you
> - A proposed weekly calendar across your main channels
> - Optional variants in your key languages (from our 100+ supported languages)
>
> You can review everything in the planner, keep what you like, adjust what you don’t, and schedule the rest.
>
> **Create → plan → schedule your next week in minutes.**
>
> 👉 **Review your suggested content pack**
>
> — The Mayagen team

---

## 3. 100+ Languages Positioning

The goal is to make multilingual feel like extra reach, not complexity or obligation.

**Key phrasing options:**
- "Start in your main language, then add 1–2 more from 100+ supported languages in one click."
- "We keep variants grouped in your planner, so your calendar doesn’t turn into a wall of duplicates."
- "Turn a single idea into posts across your key markets — without writing each one from scratch."

**Tooltip / helper text examples:**
- Tooltip on `+ Add language`:
  - "Add 1–2 more languages. Mayagen will generate translated versions and keep them grouped with the original."
- Helper text below language selector:
  - "We recommend starting with 1–3 languages total so your calendar stays focused. You can always add more later."

---

## 4. Planner & Confirmation Microcopy

**Planner header (when pack is generated):**
- Title: **"Weekly content pack — Week of {{date}}"**
- Subtitle: "Review your AI-drafted posts, then schedule the week in one click."

**Primary CTA above planner:**
- Label: **"Schedule this week’s pack"**
- Helper text: "We’ll schedule all remaining drafts on your calendar. You can still edit or delete any post later."

**Empty state (no pack yet):**
- Title: **"Want help filling this week?"**
- Body: "Generate a weekly content pack — Mayagen will draft a simple mix of posts, plan them across your channels, and let you schedule everything in a single review."
- CTA: **"Generate a weekly pack"**

**Confirmation toast:**
- "{{count}} posts scheduled across {{channels}} in {{languages}} language(s). You can tweak anything from your planner."

**Failure state (generation error):**
- Title: **"We couldn’t create this week’s pack"**
- Body: "Something went wrong on our side. Try again in a moment, or start from a blank planner — your calendar is still safe."

**Disconnected channels:**
- Title: **"Reconnect a channel to schedule this pack"**
- Body: "You’ll need at least one connected social account so Mayagen can schedule your weekly content pack."
- CTA: **"Reconnect channels"**

---

## 5. Messaging Checklist (for all surfaces)

When you add or review copy for this experiment, check:

- [ ] Does it clearly communicate **create → plan → schedule** as one flow?
- [ ] Does it avoid heavy jargon ("AI-powered orchestration", etc.)?
- [ ] Does 100+ languages feel like optional reach, not a setup chore?
- [ ] Is the outcome obvious ("a week of posts scheduled")?
- [ ] Is the cognitive load low ("review once", "one click", "this week")?

If a line doesn’t help someone imagine a week of posts scheduled with less effort, it probably doesn’t belong.