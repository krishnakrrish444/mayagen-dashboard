# Weekly Content Pack Experiment — Spec v1

## Overview

**Goal:** Use weekly, auto-generated content packs to turn "I signed up and tried a tool" into "I publish consistently across channels in my language(s)" — and make Mayagen's full suite (create → plan → schedule in 100+ languages) feel like the default way to run social.

**Audience:**
- Busy solo founders, marketers, and small teams
- Already have at least one connected channel or published post
- Struggle with "what do I post this week?" and doing it consistently

**Core Idea:**
Once a week, Mayagen proposes a ready-to-use content pack tailored to the user:
- 3–7 suggested posts (memes, value posts, promos, product mockups)
- Pre-selected channels and times
- Multilingual variants where relevant (grouped per idea, not exploded into chaos)
- One-click: **"Accept & schedule"** or **"Review & tweak"** in the planner.

Mayagen does the heavy lifting of **creating** posts, **planning** a balanced mix, and **scheduling** them — the user just reviews and approves.

---

## Scope for v1

### Content Pack Definition (MVP)

Each weekly content pack includes:

1. **Content mix**
   - 1 × brand/mission or story post
   - 1–2 × meme or light/relatable posts (using Meme Generator)
   - 1–2 × product/feature or launch posts (optionally using Product Mockups)
   - 1 × engagement or question post

2. **Channel plan**
   - Default to the user's most-used 1–2 channels (e.g., Instagram + LinkedIn)
   - Use planner rules if they exist; otherwise, sensible defaults (3–5 posts/week)

3. **Schedule proposal**
   - Suggested days and times (e.g., Mon/Wed/Fri at local-evening slots)
   - Clearly shown as a **draft weekly plan** the user can accept or edit

4. **Multilingual behavior**
   - Default language = signup or most-used language
   - Optional `+ Add language` control to add 1–2 extra languages
   - For each post, variants are grouped together in the planner:
     - One idea → multiple language versions → scheduled to adjacent time slots

5. **Export into planner & scheduler**
   - Once user accepts, pack becomes a set of scheduled posts in the planner
   - All edits happen via the usual planner/scheduler — no special mode needed after acceptance

---

## UX Entry Points

### 1) Post-signup / early activation (in-app)

**Trigger:** User has connected at least one channel and created or scheduled their first post.

**Surface:**
- In-app banner on dashboard: **"Want help posting every week? Get your first weekly content pack."**
- CTA opens a modal explaining the pack and showing a preview.

**Key copy (in-app banner & modal)**
- Banner title: **"Stay consistent without starting from a blank page"**
- Banner body: "Mayagen can propose a weekly content pack — memes, posts, and promo ideas — already planned on your calendar. Review in minutes, schedule in one click."
- Primary CTA: **"Generate this week’s content pack"**
- Secondary: "Maybe later"

Modal sections:
1. "What you’ll get": 3–7 posts, channels, suggested times, optional extra languages.
2. "How it works":
   - Mayagen **creates** post ideas for your brand
   - Packs them into a **weekly plan** in your calendar
   - Lets you **schedule** everything in one review
3. "Languages": "Start in your main language, then add 1–2 more from 100+ supported languages. We group variants so your calendar stays clean."

Primary CTA: **"Create this week’s pack"** (opens planner with the proposal loaded as a draft week).

### 2) Ongoing engagement (email)

**Trigger:** User has:
- At least one channel connected, and
- Posted at least once in the last 30 days, or
- Has gone inactive for 7–21 days (different variants).

**Surface:** Weekly email with personalized subject and a clear CTA back into planner.

**Email copy v1**

**Subject line options:**
1. "We drafted this week’s posts for you"
2. "Your weekly content pack is ready (just review & schedule)"
3. "No ideas this week? Try these posts we made for you"

**Preview text options:**
- "Memes, story posts, and promos — already planned on your calendar."
- "Create → plan → schedule in minutes, in your language."

**Body:**

> Hi {{first_name}},
>
> Showing up every week is hard when you start from a blank page.
>
> This week, Mayagen can do the heavy lifting for you.
>
> **Your weekly content pack includes:**
> - 3–7 posts (memes, story posts, simple promos)
> - Suggested days and times on your calendar
> - Optional variants in 100+ languages
>
> You can review everything in one place, make quick edits, and schedule it all in a few clicks.
>
> **Create → plan → schedule — without the weekly scramble.**
>
> 👉  **Open this week’s content pack**
>
> If you’d rather keep full control, you can still start from scratch in the planner any time.
>
> — The Mayagen team

Secondary text (footer):
> PS: As you publish more, your packs will get smarter about what works for your audience.

### 3) Dashboard nudge (for returning users)

**Trigger:** User returns to dashboard on a Monday (or their local-start-of-week) with no posts scheduled for the week.

**Surface:** Slim inline card at top of dashboard.

**Copy:**
- Title: **"You don’t have anything scheduled this week"**
- Body: "Let Mayagen create a weekly content pack — memes, posts, and simple promos — and drop them straight into your planner. You can edit or remove anything before it’s scheduled."
- CTA: **"Generate a weekly pack"**

---

## Planner & Scheduler Behavior

When a user accepts or generates a pack:

1. **Draft mode in planner**
   - All pack posts appear in the weekly planner as drafts.
   - Clearly labeled: "Weekly content pack — Week of {{date}}".
   - User can:
     - Edit text, images, channels
     - Toggle languages on/off per post
     - Drag posts to different days/times

2. **Single action to schedule**
   - Primary CTA above the planner: **"Schedule this week’s pack"**
   - On click:
     - All remaining drafts are scheduled
     - Confirmation toast and summary: "7 posts scheduled across 2 channels in 2 languages."

3. **Language handling**
   - Pack is generated in base language
   - `+ Add language` lets user choose additional languages from a curated list
   - For each post, Mayagen generates translated versions and groups them:
     - Example: "Launch teaser" → EN, ES, FR grouped on the same day with staggered times.

4. **Failure/edge cases (copy only)**
   - If generation fails: "We couldn’t generate this week’s pack. Try again, or start from a blank planner — your calendar is still safe."
   - If channels disconnected: "Reconnect at least one channel to let Mayagen schedule this week’s pack."

---

## Messaging Guidelines (for all surfaces)

- Always reinforce the suite: **create → plan → schedule**.
- Make 100+ languages feel like **reach**, not complexity:
  - "Start in your main language, then add 1–2 more in one click."
  - "We group language variants so your calendar doesn’t turn into a wall of duplicates."
- Emphasize relief from the blank page:
  - "Skip the blank page. Start from a weekly pack."
  - "One review, a full week of posts scheduled."
- Avoid heavy jargon like "AI-powered multi-channel orchestration".
- Show outcomes: scheduled posts, consistent weeks, multilingual reach.

---

## Open Questions / Next Steps

- Should packs be opt-in (strong recommendation) or auto-generated silently and surfaced when useful?
- How many posts per pack feels like "enough" without overwhelming users? (3–5 vs 5–7)
- Which languages should we suggest by default beyond the primary? (Based on geo? UI language? Past behavior?)

**Next for @content-lead:**
- Refine email and in-app copy once UX flows and visuals are defined.
- Draft variants for different segments (new vs returning, active vs at-risk).

**Next for @product-ux / @growth (for SK to delegate):**
- Turn this spec into concrete Figma flows and planner states.
- Wire events so we can measure pack acceptance, edits, and resulting scheduled posts.