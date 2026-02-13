# Weekly Content Pack Experiment — Messaging & Copy v2 (Suite-First)

This v2 tightens v1 into implementation-ready copy blocks and a simple surface matrix. Through-line for every surface:

> **"Create → plan → schedule a week of posts (optionally in 100+ languages) without starting from a blank page."**

Multilingual is always:
- Optional (1–2 extra languages recommended)
- Presented as extra reach, not extra work
- Grouped in the planner so the calendar doesn’t explode

---

## 1. Surface Matrix (where this shows up)

**Surfaces & primary line:**
1. **Dashboard banner / in-app nudge**  → "Turn this week into a full content plan."
2. **Planner empty state**              → "Want help filling this week?"
3. **Email (re-engagement)**            → "We drafted this week’s posts for you."
4. **Power-user planner hint**          → "Want a head start on next week?"
5. **Pack-generated planner state**     → "Weekly content pack — Week of {{date}}"

Each surface uses the same spine:
- Outcome: a week of posts scheduled
- Flow: create → plan → schedule
- Multilingual: main language first, +1–2 languages as reach

---

## 2. Core Blocks (shared across segments)

### 2.1 Global headline & subhead

**Global headline (shared idea):**
- "Skip the blank page. Get a weekly content pack you can schedule in one review."

**Global subhead options:**
- "Mayagen drafts this week’s posts, drops them onto your calendar, and lets you schedule everything in a few clicks — in your main language, plus 1–2 more if you like."
- "From idea to scheduled posts: Mayagen creates a simple weekly plan on your calendar so you can review once and hit schedule."

**Benefit bullets (modular):**
- "3–7 posts per week tailored to your brand and channels."
- "Suggested days and times, already placed on your calendar."
- "Optional variants in 100+ languages, grouped so your planner stays clean."
- "One review to **create → plan → schedule** your week."

Tone rules (for any new copy):
- Use concrete nouns: *posts, calendar, week, schedule*.
- Show the outcome ("a week of posts scheduled"), not the mechanism ("AI automation").
- Treat 100+ languages as a lever for reach, not a setup chore.

---

## 3. Segment-Specific Copy

### 3.1 New but activated users
*Segment:* Recently signed up, created/scheduled 1–3 posts.

**In-app banner**
- **Title:** "Turn this week into a full content plan"
- **Body:** "You’ve already published with Mayagen. Let us draft a weekly content pack — memes, stories, and simple promos — and drop them onto your calendar. Review once, schedule the week."
- **Primary CTA:** "Generate this week’s pack"
- **Secondary:** "Not now"

**Intro modal section**
- **Section title:** "Create → plan → schedule in one pass"
- **Body:** "We create 3–7 posts for your brand, plan them across your channels, and let you schedule them in a single review. Start in your main language, then add 1–2 more from 100+ supported languages if you want extra reach."

---

### 3.2 Returning but inconsistent users
*Segment:* Has posted before; no scheduled posts this week.

**Dashboard nudge**
- **Title:** "Nothing scheduled this week"
- **Body:** "Let Mayagen propose a weekly content pack — a simple mix of memes, stories, and promos — already placed on your calendar. Tweak what you like, then schedule everything in a few clicks."
- **CTA:** "See this week’s pack"

**Email — inconsistent users (ready to ship)**
- **Subject options:**
  - "We drafted this week’s posts for you"
  - "Your weekly content pack is ready to review"
  - "Want a full week of posts without the blank page?"
- **Preview options:**
  - "Create → plan → schedule this week’s posts in one pass."
  - "3–7 posts, suggested times, optional variants in 100+ languages."

**Body:**
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

---

### 3.3 Highly active / power users
*Segment:* Publishes regularly; multiple channels, maybe multiple languages.

**Planner hint**
- **Title:** "Want a head start on next week?"
- **Body:** "Let Mayagen draft a weekly content pack based on what’s working — ideas, suggested times, and language variants — then you take it from there."
- **CTA:** "Generate next week’s pack"

**Email — power users (ready to ship)**
- **Subject options:**
  - "A head start on next week’s posts"
  - "We can draft next week’s content pack for you"
- **Preview options:**
  - "Save time on planning and language variants."
  - "3–7 post ideas, a proposed calendar, optional variants in your key languages."

**Body:**
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

## 4. 100+ Languages — Implementation-Ready Snippets

**Short value lines:**
- "Start in your main language, then add 1–2 more from 100+ supported languages in one click."
- "Keep multilingual variants grouped under each post so your calendar stays clean."
- "Turn one idea into posts across your key markets — without writing each one from scratch."

**Tooltip for `+ Add language`:**
- "Add 1–2 more languages. Mayagen will generate translated versions and keep them grouped with the original post."

**Helper text below language selector:**
- "We recommend starting with 1–3 languages total so your calendar stays focused. You can always add more later."

These lines can be reused across Logo Maker, Meme Generator, Product Mockups, and planner surfaces for consistency.

---

## 5. Planner & State Copy (Ready to Drop In)

**Planner header (pack generated):**
- Title: "Weekly content pack — Week of {{date}}"
- Subtitle: "Review your AI-drafted posts, then schedule the week in one click."

**Primary CTA above planner:**
- Label: "Schedule this week’s pack"
- Helper: "We’ll schedule all remaining drafts on your calendar. You can still edit or delete any post later."

**Empty state (no pack yet):**
- Title: "Want help filling this week?"
- Body: "Generate a weekly content pack — Mayagen will draft a simple mix of posts, plan them across your channels, and let you schedule everything in a single review."
- CTA: "Generate a weekly pack"

**Confirmation toast:**
- "{{count}} posts scheduled across {{channels}} in {{languages}} language(s). You can tweak anything from your planner."

**Failure state (generation error):**
- Title: "We couldn’t create this week’s pack"
- Body: "Something went wrong on our side. Try again in a moment, or start from a blank planner — your calendar is still safe."

**Disconnected channels:**
- Title: "Reconnect a channel to schedule this pack"
- Body: "You’ll need at least one connected social account so Mayagen can schedule your weekly content pack."
- CTA: "Reconnect channels"

---

## 6. Quick Review Checklist (for SK, design, and growth)

Use this checklist when wiring any new surface to the Weekly Content Pack experiment:

- [ ] The copy explicitly mentions **create → plan → schedule** as one flow.
- [ ] The outcome is concrete: "a week of posts scheduled" or equivalent.
- [ ] 100+ languages are framed as optional reach (typically +1–2 languages), never a setup chore.
- [ ] Multilingual UX keeps variants grouped; copy doesn’t imply cluttered calendars.
- [ ] Time/effort is framed as low: "this week", "one review", "in a few clicks".
- [ ] The CTA verb matches the step: *Generate*, *See*, *Review*, or *Schedule* — not vague "Learn more".

This v2 is ready for direct use in product, emails, and experimentation briefs, and can be treated as the canonical messaging source for the Weekly Content Pack across the Mayagen suite.