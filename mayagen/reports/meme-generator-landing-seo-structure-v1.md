# Meme Generator Landing Page — SEO & Funnel Structure v1

**URL:** `/meme-generator/`
**Owner:** @seo-growth  
**Related docs:**
- SEO v2 architecture: `/mayagen/reports/seo-audit-v2.md`
- Growth & acquisition v2: `/mayagen/reports/growth-strategy-v2.md`
- Copy & narrative v1 (content): `/mayagen/reports/meme-generator-landing-copy-v1.md`

## 1. Page Purpose & Primary Job

- Rank for high‑intent meme queries ("meme generator", "meme maker", "ai meme generator").
- Convert visitors into:
  1) first meme created,
  2) first interaction with **"Use in social post"**,
  3) first scheduled post inside planner/scheduler.
- Make it clear that Meme Generator is a **free entry point into the Mayagen suite** (create → plan → schedule → multilingual distribution).

## 2. Keyword & Intent Mapping

**Primary keywords**
- meme generator
- meme maker
- meme creator

**Secondary/supporting**
- ai meme generator
- text meme maker
- gif meme maker
- meme generator for social media

**Search intent:**
- Users expect an **instant, free meme tool** with minimal friction.
- Our twist: keep that expectation, but clearly connect to **planner + scheduler** without over‑gating.

## 3. Recommended On‑Page Heading Structure

H1 and H2s are tuned to SEO v2 section 2.5 while reflecting the suite funnel.

### H1
- **H1:** Meme Generator – Make Viral Memes That Actually Ship
  - Meta title variant: `Meme Generator – Make Viral Memes & Schedule Posts | Mayagen`

### H2 Sections (Top‑Level)

1. **H2: Create Memes in Seconds With AI**
   - Covers core tool expectations from SEO v2:
     - Classic templates (Distracted Boyfriend, Drake, etc.).
     - Upload your own image.
     - AI caption suggestions from a short prompt or topic.

2. **H2: Turn Your Meme Into a Social Post (In One Click)**
   - Explicitly surfaces the **"Use in social post"** CTA as the primary action after generation.
   - Shows mini composer: select platform → caption → schedule time.
   - Internal links:
     - `/social-media-posts/` (for more robust post creation)
     - `/social-media-scheduler/` (for full calendar view)

3. **H2: Plan Meme Campaigns, Not One‑Off Posts**
   - Aligns with Growth v2 funnels (free tool → planner → scheduler):
     - Explain adding memes into campaigns/boards.
     - Show weekly/monthly planner with memes mixed into other post types.
   - Internal links:
     - `/social-content-planner/`
     - `/content-calendar/`

4. **H2: Memes in 100+ Languages With Nano Banana Pro**
   - Brings Nano Banana Pro and multilingual angle forward:
     - Turn one meme idea into localized variants.
     - Emphasize "translate the joke, not just the words".
   - Internal links:
     - `/multilingual-social-posts/`

5. **H2: Why Teams Start With Memes (and Stay for the Suite)**
   - Reframes Meme Generator as gateway into the full AI creative suite:
     - On‑brand memes using brand kit assets.
     - Reuse memes in ads, posts, and templates.
   - Internal links:
     - `/suite/`
     - `/logo-maker/` and `/brand-kit/` (for aligning memes with brand identity)

6. **H2: Examples of Meme‑Led Campaigns**
   - Cards for sample use cases (B2B launch, ecommerce drop, community engagement) that:
     - Start from a meme.
     - Flow into scheduled campaigns.
   - Optional internal links:
     - Relevant blog posts once they exist (e.g., "From Meme to Marketing Campaign" article).

7. **H2: Meme Generator FAQs**
   - Answer both tool‑level and suite‑level questions:
     - Is Meme Generator free?
     - Do I need an account to start?
     - Can I schedule memes as posts?
     - Which platforms and languages are supported?
   - Marked up as FAQ schema (`FAQPage`).

## 4. Content & UI Notes by Section

### 4.1 Hero + Above the Fold

- Keep the copy and layout direction from `meme-generator-landing-copy-v1.md` but ensure:
  - The H1 matches the SEO title (or very close variant).
  - A visible **inline tool preview** is rendered server‑side (meme canvas + planner peek) for SEO.
- Primary CTA: **"Start free with Meme Generator"** (no signup wall to create first meme).
- Secondary CTA: **"See how it works"** → anchor to the "Turn Your Meme Into a Social Post" section.

### 4.2 "Create Memes in Seconds With AI" (H2 #1)

- Include 2–3 **popular template names** in body copy for relevance.
- Mention **upload your own image** and **text‑only memes** for completeness.
- Implement a short **How‑to block** (3–4 steps) so we can attach `HowTo` schema.

### 4.3 "Turn Your Meme Into a Social Post" (H2 #2)

- This is the key funnel hinge.
- Make **"Use in social post"** the visually primary CTA after meme generation; "Download (with watermark)" is secondary.
- Show a mini composer that previews:
  - Selected channel (Instagram, X, LinkedIn, etc.).
  - Auto‑generated caption + hashtags.
  - A simple date/time picker.
- Copy should echo Growth v2 language: "Use in social post" → planner → scheduler → weekly habit.

### 4.4 "Plan Meme Campaigns" (H2 #3)

- Show planner/scheduler UI with multiple memes slotted across a week.
- Emphasize that memes can:
  - Sit alongside regular posts, carousels, and ads.
  - Be duplicated and localized.
- CTA: **"Open in planner"** → takes current meme into `/social-content-planner/` (or in‑app planner route).

### 4.5 "Memes in 100+ Languages" (H2 #4)

- Explain Nano Banana Pro briefly in copy.
- Show side‑by‑side examples of the same meme localized for 2–3 languages.
- Clarify that users can:
  - Choose languages per channel.
  - Review and tweak localized text before scheduling.

### 4.6 "Why Teams Start With Memes" (H2 #5)

- Bring in brand kit and suite language from SEO v2 & Growth v2:
  - Mention logo maker, brand kit, templates, scheduler in one short paragraph.
- Explicit internal links (HTML):
  - `href="/suite/"`
  - `href="/logo-maker/"`
  - `href="/brand-kit/"`

### 4.7 Examples & FAQ (H2 #6–7)

- Example cards should double as **soft CTAs** into the planner/scheduler:
  - "View this as a calendar" → deep link into demo calendar/campaign.
- FAQ answers must clarify:
  - Free vs paid boundaries (free memes, paid scheduling at scale).
  - That no signup is required for first meme, but is required to **save schedule**.

## 5. Internal Linking Checklist

From `/meme-generator/`, we should:

- Link to **suite narrative**:
  - `/suite/`
- Link to **planning & scheduling**:
  - `/social-content-planner/`
  - `/social-media-scheduler/`
  - `/content-calendar/`
- Link to **brand identity tools**:
  - `/logo-maker/`
  - `/brand-kit/`
- Link to **multilingual value prop**:
  - `/multilingual-social-posts/`
- (Future) Link to **supporting content**:
  - Blog posts about meme‑led campaigns and social content systems.

## 6. Technical SEO Notes

- Ensure `/meme-generator/` is treated as a **Tier 1 flagship tool page** per SEO v2.
- Use `WebApplication` schema with:
  - `name`: `Mayagen Meme Generator`
  - `applicationCategory`: `EntertainmentApplication` / `DesignApplication`
  - `isPartOf`: `https://mayagen.ai/suite/`
- Add `HowTo` + `FAQPage` structured data for the relevant sections.
- Ensure the hero and H2 blocks are all **SSR/SSG** so copy is present in HTML.

## 7. Next Steps

- [x] Draft SEO‑aligned heading structure and internal link plan (this doc).
- [ ] Review with @content-lead to merge structure into `meme-generator-landing-copy-v1.md`.
- [ ] Coordinate with design/UX on visuals for:
  - Meme editor + planner/scheduler combo hero.
  - Meme → post → calendar flow strip.
  - Multilingual meme examples (side‑by‑side).
