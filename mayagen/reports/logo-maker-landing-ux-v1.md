# Logo Maker Landing – UX Review v1

_Last updated: 2026-02-13_

## 1. Role of Logo Maker in the Suite

From Product Strategy v2 and Content & Messaging v2, Logo Maker is not a standalone logo tool; it's the **entry point to a brand system and launch flow**:

- New logo → **Brand Kit** → **Templates across tools** → **Launch campaign scheduled in calendar**.
- It should feel like you’re **setting up a command center for your brand**, not just exporting a logo file.

Implication for landing: every major section and CTA should reinforce that **Logo Maker = start of a broader launch workflow**.

---

## 2. Friction & Gaps in the Intended Flow

Target flow (per strategy docs):

> New logo → brand kit → social templates → scheduled launch posts

Friction points and risks if we treat Logo Maker too narrowly:

1. **“File export” mental model instead of “launch flow”**
   - If the page or in-product flow emphasizes downloading logo assets (PNG/SVG) over creating a brand kit, users will stop at the file and never discover templates, planner, or scheduler.

2. **Weak connection to planner + scheduler**
   - Product Strategy v2 highlights **idea → graphic → scheduled post** as a core flow, but Logo Maker’s story could easily end at “you now have a logo.”
   - Without explicit CTAs like **“Launch your new brand”** that lead into planner/scheduler, users won’t intuit that the next step is populating their calendar.

3. **Brand Kit not clearly surfaced as the “next step”**
   - Strategy v2 doubles down on Brand Kit v1/v2 as the glue across tools.
   - If the landing doesn’t explain that Logo Maker **auto-builds a brand kit** and pushes that kit into other tools, users will experience each tool as separate.

4. **Multilingual launch story is implicit, not explicit**
   - Content v2 positions Mayagen as multilingual by design, but for Logo Maker the multilingual angle may be underplayed.
   - Opportunity: pitch **multilingual brand lockups and launch assets** (e.g., name/tagline in multiple languages, launch posts per market) directly from the Logo Maker page.

5. **No clear “time to value” narrative**
   - Our north star is flows like “idea → graphic → scheduled post in 5 minutes.”
   - For Logo Maker, an equivalent narrative would be: **“New logo to fully scheduled launch week in under 30 minutes.”** The landing structure needs to make that feel concrete and believable.

---

## 3. Proposed Landing Page Structure (UX-Focused)

This builds on Content v2’s structure but makes the **flow into brand kit + templates + scheduler** more explicit and visual.

### 3.1 Above the Fold

- **Title:** `Logo Designer – Design your brand, then roll it out everywhere.`
- **Sub-heading (slightly adjusted):**
  > Craft a logo, turn it into a living brand kit, and auto-generate the launch assets and posts you need—from social avatars to a full launch week—in one AI-native workspace.

- **Primary CTA:** `Design your logo & launch kit`
  - Tooltip or microcopy: “You’ll set up your logo, brand kit, and first launch posts in a guided flow.”

- **Secondary CTA:** `See launch flow`
  - Scrolls to a visual strip showing: **Logo → Brand Kit → Templates → Calendar**.

### 3.2 Flow Strip: “From logo to launch in one guided flow”

A horizontal, step-by-step visualization (desktop) or vertical cards (mobile):

1. **Step 1 – Design your logo**
   - Microcopy: “Explore AI-powered logo concepts based on your name, industry, and values.”
2. **Step 2 – Auto-build your brand kit**
   - Microcopy: “Colors, fonts, and usage rules are generated for you—and applied across Mayagen.”
3. **Step 3 – Generate launch-ready templates**
   - Microcopy: “Profile images, cover photos, announcement posts, and promo templates created in one click.”
4. **Step 4 – Schedule your launch across channels**
   - Microcopy: “Drop your launch posts straight onto the calendar—localized for each language you care about.”

Add **inline badges** like “Multilingual ready” and “Planner + scheduler included” to reinforce suite positioning.

### 3.3 Value Section: “Your logo is the start of a brand system”

Refine the existing "From logo concept to complete brand kit" section into three clear columns:

- **Column 1 – Explore & decide**
  - Bullet examples:
    - "Get guided directions, not random options—narrow down quickly with structured feedback."
    - "Preview how each concept looks on profiles, covers, and posts before committing."

- **Column 2 – Auto-brand everything**
  - Bullet examples:
    - "Save your chosen logo as a brand kit with one click."
    - "Apply brand styling automatically in memes, mockups, and social templates."

- **Column 3 – Launch in days, not months**
  - Bullet examples:
    - "Generate a launch campaign kit: announcement, countdown, and ‘now live’ posts."
    - "Schedule your first week of posts across platforms in a single view."

Include a small illustrated diagram or mini calendar preview to reinforce the scheduling angle.

### 3.4 Multilingual Branding & Launch Section

Dedicated section to make multilingual a first-class story:

- **Heading:** `Launch your brand in every market at once`
- Supporting bullets:
  - "Explore name and tagline directions across multiple languages."
  - "Generate logo lockups and taglines for each region while keeping design consistent."
  - "Create localized launch posts (captions + visuals) for each language and schedule them together."

Add a mini UI mock: tabs for languages (e.g., EN, ES, FR) with previews of brand lockups and launch posts.

### 3.5 How Logo Maker Fits Into Mayagen

A section that explicitly connects to other tools and flows:

- Short narrative:
  - "Start with Logo Designer to define your brand."
  - "Your Brand Kit becomes the default across Meme Generator, Product Mockups, and social post templates."
  - "Planner and Scheduler help you roll out a coordinated launch across channels and languages."
- Visual: simple node diagram with Logo Designer at the left, Brand Kit in the center, and arrows to Templates, Planner, and Scheduler.

### 3.6 Social Proof & “Time to Launch” Story

- Small testimonial-style block:
  - "We went from ‘no logo’ to a full social launch kit in one afternoon." – Solo café owner / creator quote (placeholder for now).
- Metric-oriented microcopy:
  - "Typical new brands ship their first week of posts in under 30 minutes after choosing a logo."

---

## 4. In-Product UX Recommendations (Post-Logo Flow)

The landing should promise a **guided flow**, and product UX must deliver it. Key suggestions:

1. **Guided “Next Step” after choosing a logo**
   - After the user selects a logo, don’t drop them on a generic download page.
   - Show a 3-step wizard:
     1. "Confirm your brand kit" (colors, fonts, usage).
     2. "Generate your launch assets" (avatars, covers, basic social templates).
     3. "Plan your launch" (open the calendar with suggested posts pre-filled).

2. **Persistent “Brand Kit status” indicator**
   - In the header or sidebar, show whether a Brand Kit is **Draft**, **Ready**, or **Live across tools**.
   - Clicking it opens the Brand Kit manager with options to adjust and preview affected templates.

3. **Deep links from Logo Maker to Planner/Scheduler**
   - In the "Launch assets" step, include a primary action: `Open in Planner`.
   - This takes users directly to a pre-filtered calendar view showing only the new-brand launch posts, with platform and language filters active.

4. **Multilingual lockup assistant**
   - Within the Logo Maker editor or post-selection flow, offer:
     - "Add languages" → pick target languages.
     - Mayagen generates name/tagline variants and previews of how they appear in the logo/brand lockups.
   - Option to “Create launch posts in these languages” which feeds into the planner.

5. **“Finish launch setup” nudges**
   - If a user creates a logo but leaves before scheduling anything, show non-intrusive nudges on dashboard and calendar:
     - "Finish launch setup for [Brand X]: generate launch posts and schedule them in a few clicks."

---

## 5. Success Metrics & Instrumentation

To know if Logo Maker is actually feeding the suite as intended, track:

- % of Logo Maker users who create a **Brand Kit** within the same session.
- % who **generate at least one launch template** (avatar, cover, announcement post).
- % who **schedule at least one post** within 24–48 hours of choosing a logo.
- Median time from **logo created → first scheduled post**.
- % of launch posts that use **>1 language**.

We should set rough targets (once usage exists), e.g.:

- 60%+ of logo creators create a brand kit in the same session.
- 40%+ create at least one launch post.
- 25%+ schedule at least one launch post in >1 language.

---

## 6. Next Steps

- Align with content on final copy for headings and bullets based on this structure.
- Coordinate with product/design on:
  - The flow strip and diagram visuals.
  - Post-logo wizard screens and deep links to planner/scheduler.
- Once initial designs are ready, run a **5-user remote test** with the task:
  - "You’re launching a new brand. Using Mayagen, go from no logo to having your first week of launch posts scheduled." Document where they stall, backtrack, or miss the brand kit/calendar steps.
