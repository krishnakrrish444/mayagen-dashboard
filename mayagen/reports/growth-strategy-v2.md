# Growth & Acquisition Strategy v2 – Mayagen.ai

**Date:** 2026-02-12  
**Role:** Growth Lead  
**Core Product:** Unified AI social content studio – create graphics, plan content, and schedule posts in 100+ languages, powered by 45+ free tools.

---

## 1. Redesigned Acquisition Funnels (Full-Suite View)

### 1.1 Principles

- **TTV < 60s:** First “wow” (a generated graphic or scheduled post) within a minute.  
- **Free → Suite:** Every free tool experience gently exposes planner + scheduler.  
- **State never lost:** Whatever they create pre-signup is preserved post-signup.  
- **Recurring use by design:** Default paths nudge users into weekly scheduling habits, not one-off downloads.

We’ll design funnels around three primary acquisition surfaces:
- **SEO / free tools** (45+ tools, localized)
- **Templates & gallery** (browsing, inspiration)
- **Social scheduler / planner** (calendar-first users)

---

### 1.2 Free Tool → Suite Funnel (SEO-led)

**Example persona:** “Aisha”, a small business owner in Cairo, searching in Arabic for a Facebook post maker.

**Entry point:** SEO page like `/ar/facebook-post-generator` or `/es/ai-logo-maker`.

#### Flow

1. **Landing (Problem → Instant Action)**
   - Above the fold: single focused input/CTA depending on tool:
     - Text prompt, brand name, or basic form (e.g., “Describe your post in one sentence”).
   - Localized headline & microcopy.  
   - No signup wall to start.

2. **Create (First Value)**
   - User creates **at least 1–3 assets** (e.g., image variants, captions).  
   - In-results panel shows:
     - Primary action: **“Use in a social post”** (instead of only “Download”).  
     - Secondary actions: “Download (with watermark)”, “Regenerate”.

3. **Suite Exposure (Soft Cross-Sell)**
   - When user clicks **“Use in a social post”**:
     - Slide-in mini composer: choose network, add caption, pick date/time.  
     - Subtle copy: “Plan a week of posts in 2 minutes.”
   - System pre-fills:
     - Selected asset  
     - Smart caption from tool  
     - Recommended posting time (based on generic best practices for now).

4. **Signup Gate at Commitment Moment**
   - Triggered when user:
     - Clicks “Schedule post”, **or**  
     - Tries to **remove watermark**, **or**  
     - Tries to **save >1 scheduled post**.
   - Modal:  
     - Title: **“Save this post & auto-publish it”**  
     - Sub: “Create, plan & auto-post content every week. Free in 1 minute.”  
     - Options: Google / social login + email.
   - Post-signup redirect: directly into **calendar view** focused on that scheduled post.

5. **Activation & Onboarding to Habit**
   - On first calendar view:
     - Progress checklist:
       1. ✅ You scheduled your first post
       2. ☐ Add 2 more posts this week
       3. ☐ Connect your social account(s)
     - Inline prompt: “Want us to auto-create 3 more posts like this?” → 1-click generates draft posts using same brand & language.
   - Email/notification follow-ups:
     - T+1 day: “Here’s what’s scheduled this week” + quick link to add more.  
     - T+7 days: “Your weekly content report” (if they posted) or “You’re 1 click from publishing your first post” (if not).

**Key metrics:**
- Tool visitor → generated first asset  
- Generated asset → clicked "Use in social post"  
- Clicked "Use in social post" → signups  
- New signups → at least 1 scheduled post  
- % users with ≥3 posts scheduled in first 7 days

---

### 1.3 Gallery / Templates → Suite Funnel (Inspiration-led)

**Entry point:** User lands on a template/gallery page from search, social, or referral, e.g., `/gallery/instagram-sale-posts`.

#### Flow

1. **Browse & Filter**
   - Localized gallery with filters: network, goal (engagement/sales/awareness), language.  
   - Hover interactions: quick preview, likes, “Used X times this week”.

2. **Template Detail Page**
   - Shows:
     - Preview(s)  
     - Example captions in user’s locale  
     - Tags + vertical info (e.g., “Best for restaurants / promos”).
   - Primary CTA: **“Customize & schedule”**.  
   - Secondary CTA: “Edit & download”.

3. **Customize (Inline Editor)**
   - Simple editor opens on top:
     - User can tweak text, colors, images.  
     - Live preview of multiple aspect ratios for different networks.

4. **Schedule Prompt (Suite Hook)**
   - After editing, show side panel:
     - “Turn this into a full campaign?”  
     - Offer: auto-generate 3–5 variants for the week.  
   - Click → opens mini planner with suggested dates.

5. **Signup Gate**
   - When user tries to **save campaign** or schedule >1 post:
     - Same modal as 1.2 (focus on "Save & auto-publish").

6. **Onboarding**
   - Post-signup, drop them into **campaign view** inside calendar (e.g., "Spring Sale" campaign with 4 posts).  
   - Offer to auto-translate variants into other languages relevant to their region.

**Key metrics:**
- Gallery visitor → views template detail  
- Template detail → clicks "Customize & schedule"  
- Editor open → creates at least 1 variant  
- Editor users → signups  
- New signups → campaign with ≥3 scheduled posts

---

### 1.4 Scheduler / Planner → Suite Funnel (Planner-first)

**Entry point:** Marketing managers / power-users attracted by “social media scheduler” positioning or direct product tours.

#### Flow

1. **Landing**
   - Calendar- or queue-first hero: live demo calendar with sample posts.  
   - CTA: **“Start with a blank calendar”** and **“Fill my calendar with AI”**.

2. **Interactive Demo (No Signup)**
   - User can:
     - Click into any day → add a “mock” post using prompts or choose from “Suggested ideas for your niche”.  
     - Use a limited set of templates (from gallery) as starting points.
   - All drafts are stored in session.

3. **AI Autofill CTA**
   - After user creates 1 draft:
     - Prompt: “Want us to plan your whole week? We’ll generate 4 more posts in your language.”  
   - User clicks → we show a “ghost preview” of a week filled with posts.

4. **Signup to Activate Calendar**
   - To **save** or **connect social accounts**, user must sign up.  
   - Modal copy: “Activate your smart calendar – never start from scratch again.”

5. **Onboarding**
   - After signup, we:
     - Persist all drafts they created.  
     - Prompt connection of at least one social profile.  
     - Run a one-click “weekly plan” wizard: ask about topics, frequency, and languages; auto-generate recurring content pillars.

**Key metrics:**
- Landing visitor → interacts with calendar  
- Interactors → signups  
- Signups → connected at least 1 social account  
- Users with ≥1 week with ≥3 scheduled posts

---

## 2. Growth Loops Leveraging Free Tools, Gallery, and Scheduler

We’ll focus on **product-led loops** that stay close to existing strengths: free tools, visual gallery, and social scheduler.

### 2.1 Loop #1 – Watermarked Sharing → Gallery Discovery → New Users

**Summary:** Use small, tasteful watermarks and links to turn every shared asset into an acquisition channel.

**Mechanics:**
1. Free users export images with a **discreet watermark** (e.g., “made with mayagen.ai”) and a short URL.
2. When that image is posted or shared:
   - Viewers click through to a **landing page for that exact template/variant**.  
   - Page shows: “Like this post? Customize it in 10 seconds.”
3. New visitors can:
   - Start editing immediately (no signup).  
   - Optionally see a strip of **“similar posts from this creator’s gallery”** if the original user opts to share their public gallery.
4. Once they create their own version, we push them into the **Free Tool → Suite funnel** above.

**Why it works:** Every asset functions as both content and ad for Mayagen. Social networks become our distribution.

**Loop metric:**  
Watermarked exports per active user → click-through rate to gallery → new signups from template-detail pages.

---

### 2.2 Loop #2 – "Shared Schedule" Previews → Collaborative Signups

**Summary:** Encourage users to share **read-only previews** of their upcoming content calendar with clients/teammates, who in turn become new users.

**Mechanics:**
1. In scheduler, users can create a **shareable link** for a specific campaign or date range.
2. Shared view (no login required) shows:
   - Calendar or list of upcoming posts.  
   - Thumbnails from gallery/templates used.  
   - CTA: “Plan content for your own brand with this template set.”
3. Collaborators (clients, colleagues) can:
   - Comment/approve posts (with name/email).  
   - Convert their role into an account with 1-click: “Duplicate this calendar for my brand.”
4. When they convert, we pre-populate their planner with the same structure but empty content or adapted templates.

**Why it works:** Agencies, freelancers, and internal teams frequently share content calendars. Each shared schedule becomes a demo plus invitation.

**Loop metric:**  
Shared schedule links created → unique viewers → viewers who sign up → new accounts using scheduler in first 7 days.

---

### 2.3 Loop #3 – Public Galleries & Embeddable Widgets

**Summary:** Turn user galleries and curated template collections into **embeddable widgets** for blogs, portfolios, and resource pages.

**Mechanics:**
1. Users can mark a folder/campaign as **public** and generate a “Gallery Page” (hosted by Mayagen).  
2. They can also generate **embed code** (iframe/script) to show this gallery on their own site.
3. Embedded gallery:
   - Displays a grid or carousel of posts.  
   - Each tile links back to a **Mayagen gallery detail page**.  
   - Optionally has a subtle “Create similar post” CTA.
4. Visitors click through:
   - Land on template detail page.  
   - Enter the **Gallery → Suite funnel**.

**Why it works:** Designers, agencies, and creators love showcasing work. Embeds turn their sites into passive acquisition channels for Mayagen.

**Loop metric:**  
Public galleries created → external embeds → visits from embeds → new users created via gallery funnel.

---

### 2.4 Loop #4 – "Content Pack" Giveaways via Free Tools

**Summary:** Free tools generate not just a single asset, but **downloadable content packs** that naturally promote return visits and referrals.

**Mechanics:**
1. On select free tools (e.g., “Instagram caption generator”, “Weekly content planner”):
   - After generating content, we offer: “Get a full 7-day content pack for this topic.”
2. The content pack includes:
   - 7 posts (image + caption)  
   - Suggested schedule  
   - Multilingual variants (if selected).
3. To **download the pack as a ZIP or PDF**, user must:
   - Sign up, and  
   - Optionally share Mayagen on social or invite a teammate to co-plan content.
4. Inside the app, these content packs are saved as **reusable campaigns**.
5. Packs include a small footer: “Generated with Mayagen – click here to refresh this pack next week.”

**Why it works:** People love “done-for-you” assets. Packs encourage recurring weekly use and sharing with collaborators.

**Loop metric:**  
Content packs generated → signups from packs → returning users who generate ≥2 packs in 30 days.

---

## 3. First 3–5 Experiments (Funnels / CRO / Virality)

We’ll start with fast, learnable experiments that de-risk where to invest deeper.

### Experiment 1 – Tool Page Gate Timing (Front-gated vs. Back-gated)

**Goal:** Maximize signups from free tool SEO traffic without hurting search rankings or engagement.

**Hypothesis:** Allowing users to generate and preview content before signup will increase signup conversion rate and reduce bounce vs gating upfront.

**Setup:**
- A/B test on 3–5 high-traffic tools.
- **Variant A (Control):** Signup wall before using the tool.  
- **Variant B (Test):** Tool is fully usable for first X actions (e.g., 1–2 generations), but download/schedule/save triggers signup.

**Primary metric:**
- Visitor → signup rate from these pages.

**Secondary metrics:**
- Visitor → generated first asset  
- Time on page  
- Bounce rate

**Success criteria:**
- Variant B improves visitor → signup by **≥20%** with no worse than **+10%** increase in infra cost per free user (due to more free generations).

---

### Experiment 2 – "Use in Social Post" CTA vs. "Download" as Primary

**Goal:** Move users from one-off asset downloads into the scheduler-based habit loop.

**Hypothesis:** Making "Use in social post" the primary CTA after generation will significantly increase the % of users who interact with the scheduler and thus finalize signup.

**Setup:**
- On 5 key free tools, run an A/B test on the post-generation UI.
- **Variant A (Control):** Primary button = “Download”; secondary = “Use in social post”.  
- **Variant B (Test):** Primary = “Use in social post”; secondary = “Download (with watermark)”.

**Primary metric:**
- Generated asset sessions → scheduler interactions.

**Secondary metrics:**
- Scheduler interactors → signups  
- New signups → at least 1 scheduled post

**Success criteria:**
- ≥30% uplift in users who touch the scheduler at least once.  
- ≥15% uplift in new signups who create ≥1 scheduled post in first session.

---

### Experiment 3 – Watermark Referral Landing Page Optimization

**Goal:** Turn watermarked exports into a strong referral channel.

**Hypothesis:** Deep-linking watermark clicks to the **exact template variant** with social proof will convert better than routing to a generic homepage.

**Setup:**
- For all watermarked exports, randomly send click traffic to:
  - **Variant A (Control):** Homepage or main tools page.  
  - **Variant B (Test):** Template/asset-specific landing page with:  
    - The original asset  
    - Button: “Customize this for your brand”  
    - Strip: “Similar posts created with Mayagen”  
    - Lightweight social proof.

**Primary metric:**
- Visitor from watermark → first asset created.

**Secondary metrics:**
- Visitor from watermark → signup  
- Signup → first scheduled post

**Success criteria:**
- ≥40% increase in visitors who create an asset on their first session.  
- ≥20% increase in visitor → signup rate.

---

### Experiment 4 – Shared Calendar → Collaborator Conversion

**Goal:** Validate whether shareable schedules can reliably bring in collaborators as new users.

**Hypothesis:** Client/teammate viewers of shared calendars are high-intent and will convert at high rates when offered duplication of that structure for their own brand.

**Setup:**
- Enable basic “Share read-only calendar” for a subset of users.
- Viewer page versions:
  - **Variant A (Control):** Simple read-only view with minimal branding.  
  - **Variant B (Test):** Shows "Duplicate this calendar for your brand" CTA + email capture.

**Primary metric:**
- Unique viewers of shared calendars → email leads/accounts.

**Secondary metrics:**
- New collaborator accounts → created at least 1 scheduled post within 7 days.  
- Number of shared calendars per active creator.

**Success criteria:**
- ≥15% of unique viewers become leads/accounts.  
- ≥40% of those new accounts create at least 1 scheduled post in first week.

---

### Experiment 5 – Weekly Content Pack Onboarding

**Goal:** Increase week-2 and week-4 retention by building a repeating “weekly planning ritual”.

**Hypothesis:** Offering a ready-made weekly content pack at the right moment in onboarding will give users a simple recurring reason to return.

**Setup:**
- Target: new signups who create at least 1 scheduled post in week 1.
- **Variant A (Control):** Regular email recap / generic product tips.  
- **Variant B (Test):** At end of week 1, send:
  - Email + in-app message: “Your free 7-day content pack for next week is ready.”  
  - Clicking opens a pre-built campaign with 5–7 posts (images + captions) tailored by niche/language.

**Primary metric:**
- Week-2 active rate for users who had at least 1 post in week 1.

**Secondary metrics:**
- Number of posts scheduled in week 2.  
- % of users generating ≥2 content packs in 30 days.

**Success criteria:**
- ≥20% uplift in week-2 retention among the eligible cohort.  
- ≥25% uplift in users with ≥5 total posts scheduled by day 30.

---

## 4. Execution Priorities (Sequencing)

1. **Foundational plumbing (Weeks 1–2):**
   - Ensure cross-tool state persistence (assets created pre-signup survive signup).  
   - Implement unified tracking: tool → scheduler → signup → retention.

2. **High-impact funnel changes (Weeks 2–4):**
   - Roll out **back-gated free tool flows** and “Use in social post” primary CTAs.  
   - Launch basic weekly calendar onboarding.

3. **Loops MVPs (Weeks 4–8):**
   - Watermarked exports with deep-linked template pages.  
   - Simple shared calendar read-only view with sign-up CTA.

4. **Refine & scale (Beyond 8 weeks):**
   - Improve embeddable galleries.  
   - Launch full content pack mechanism and multi-language automation.  
   - Iterate on copy, localization, and CRO based on experiment learnings.

This v2 strategy reframes Mayagen as a **full-suite social publishing system** where the 45+ free tools, gallery, and scheduler are tightly connected to drive:  
(1) higher initial activation, (2) more users adopting the scheduler habit, and (3) sustainable, product-led growth loops.
