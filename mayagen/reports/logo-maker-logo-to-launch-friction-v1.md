# Logo Maker → Logo-to-Launch Flow – Friction & UX Change List v1

_Last updated: 2026-02-13 — Shuri (@product-ux)_

This document focuses on friction inside the **"logo → brand kit → launch assets → calendar"** flow and proposes **concrete UI/UX changes** to make the path closer to:

> Idea → graphic → scheduled post in **5–10 minutes**, even for first-time users and multilingual launches.

It builds on:
- `/mayagen/reports/logo-maker-landing-ux-v1.md`
- `/mayagen/reports/logo-maker-logo-to-launch-flow-v1.md`
- `/mayagen/reports/logo-maker-landing-copy-v2.md`

---

## 1. Friction: Entry into the Guided Flow is Too Optional

**Observed risk**
- Landing currently offers CTAs like **"Design your logo & launch kit"** and **"See logo-to-launch flow"`, but it’s still possible for users to:
  - Enter the editor in a generic mode (no sense of a 4-step wizard).
  - Treat the experience as a normal logo editor and never see planner/scheduler.

**Why this matters**
- Our core story is **create → plan → schedule**. If the guided flow is optional or easy to miss, many users will stay in a pure-design mental model and never touch planner/scheduler.

**Concrete UX changes**
1. **Default to guided mode for new workspaces**
   - First-time users should always enter Logo Maker via a **"Launch a new brand"** preset that starts the 4-step wizard (`Logo → Brand Kit → Launch Assets → Calendar`).
   - Advanced users can switch to "Logo-only" mode from a small link.

2. **Persistent flow breadcrumb in the editor**
   - Always show `Logo → Brand Kit → Launch Assets → Calendar` at the top.
   - Current step should be visually strong; others clickable but marked as upcoming/completed.

3. **Inline time expectation**
   - In hero and/or stepper, add copy like: `Typical time to first scheduled launch post: 5–10 minutes.`
   - This frames the experience as a short, guided flow rather than an open-ended editor.

---

## 2. Friction: Post-Logo Step Still Feels Like "Download" First

**Observed risk**
- Even with the proposed wizard, users may still:
  - Look for the download button as the primary completion cue.
  - Treat Brand Kit as “extra setup” instead of the default next step.

**Concrete UX changes**
1. **Make Brand Kit the clear primary path**
   - After logo selection, show a full-screen **Step 2: Brand Kit** pane.
   - Primary action: `Save Brand Kit & continue`.
   - Download should live behind a small `More actions` menu, not as a primary button.

2. **Inline benefit reminder**
   - Short bullet list under the primary CTA:
     - "Auto-brand memes, mockups, and templates."
     - "Use your logo across the planner and scheduler in one click."

3. **Gentle guardrail on skipping**
   - If user clicks `Skip for now`, show a confirmation copy: 
     > "Without a Brand Kit, your logo won’t connect to templates, planner, or scheduler. Continue anyway?"
   - Default focus on `Go back and create Brand Kit`.

---

## 3. Friction: Calendar Step Overwhelms First-Time Users

**Observed risk**
- Dropping users into a full-featured planner/scheduler can be overwhelming:
  - Too many controls (filters, views, campaigns, etc.).
  - Unclear which posts are part of the current logo launch vs everything else.

**Concrete UX changes**
1. **Scoped "Launch Week" mode**
   - Open the calendar in a simplified **Launch Week** mode when coming from Logo Maker:
     - Fixed **week view**.
     - Only show posts tied to `brand_id` from the current flow.
     - Hide or collapse non-essential filters/sidebars.

2. **Launch checklist panel**
   - Right-hand side checklist:
     - [ ] Review your launch posts
     - [ ] Add languages
     - [ ] Confirm schedule
   - Each checklist item scrolls/focuses the relevant UI.

3. **Single primary CTA: `Schedule launch week`**
   - Button at top of the view that:
     - Schedules all current launch posts at opinionated default times.
     - Shows a short confirmation summary.
   - Advanced tweaks (individual times, channels) are still possible but not required to succeed.

4. **Clear grouping of "this flow" posts**
   - Visual tag or pill on each draft: `Logo launch`.
   - Small label above the calendar: `You’re viewing posts for: [Brand Name] – Logo launch`.

---

## 4. Friction: Multilingual UX is Powerful but Easy to Avoid or Misuse

**Observed risk**
- Multilingual is a strong differentiator, but:
  - If hidden behind generic settings, users may never discover it.
  - If exposed too early or with too many options, first-time users may bail.

**Concrete UX changes**
1. **Deferring language choice until calendar step**
   - Avoid asking about languages during logo creation/Brand Kit; keep that phase visually focused.
   - Introduce language choice after users see draft posts on the calendar.

2. **Inline `+ Add language` with copy that reduces fear**
   - Button near calendar heading: `+ Add language`.
   - Helper text: `We’ll keep visuals synced and adapt the copy for each language.`

3. **Hard limit in guided mode**
   - In this flow, allow up to **3 additional languages** (plus the primary one).
   - Microcopy: `You can add more later from your calendar settings.`

4. **Variant grouping by base post**
   - Each base post row shows language chips: `EN`, `ES`, `HI`, etc.
   - Clicking a chip reveals that language’s caption + preview side-by-side, not as separate ungrouped cards.

5. **Quick-review mode**
   - Add a compact "Review language variants" modal that:
     - Steps through each post with all languages stacked.
     - Offers a simple approve/edit toggle.

---

## 5. Friction: No Strong Feedback Loop After Scheduling

**Observed risk**
- After clicking `Schedule`, users might not feel the impact:
  - Unsure what was actually created.
  - Unsure how to change things later.

**Concrete UX changes**
1. **Explicit launch summary panel**
   - Immediately after scheduling, show a non-modal panel (or modal with clear follow-ups):
     - "You’re launching [Brand Name]."
     - X posts over Y days.
     - Channels and languages covered.

2. **Direct link to "Manage this launch"**
   - CTA: `Manage this launch in planner` which:
     - Filters planner to this brand + campaign.
     - Shows only the logo-launch posts.

3. **Dashboard nudge**
   - On workspace/home, show a card for upcoming launches:
     - "[Brand Name] launch is scheduled for [date]."
     - CTA: `Review posts` (deep-links into filtered planner view).

---

## 6. Friction: Time-to-First-Scheduled-Post Not Explicitly Prioritized

**Observed risk**
- The flow supports fast completion, but we haven’t explicitly optimized or framed it around **time-to-first-scheduled-post**.

**Concrete UX changes**
1. **Instrument and surface TTFSP (Time To First Scheduled Post)**
   - Track the time from `logo_created` to `post_scheduled_from_logo_flow`.
   - Show average TTFSP in internal dashboards; use it as a primary UX success metric for this flow.

2. **Microcopy anchoring user expectation**
   - At flow start: `Most creators get their first launch post scheduled in under 10 minutes.`
   - At each step, small copy like `~2 minutes` under step labels.

3. **Shortcut path for impatient users**
   - Offer a **"Skip details, just ship my first post"** option at Step 3 (Launch Assets):
     - Generates a single high-confidence launch post.
     - Jumps straight into calendar with that one draft selected and a big `Schedule this post` button.

---

## 7. Summary – Net Effect on Key Flows

If we implement the above changes, the intended user experience becomes:

1. Almost all first-time Logo Maker sessions start in a clearly labeled **logo-to-launch wizard**.
2. Users understand that the natural completion of Logo Maker is a **scheduled launch post**, not just a download.
3. The calendar step feels **scoped and friendly**, focused on a single launch week and brand.
4. Multilingual is surfaced as a **safe, guided enhancement**, not an overwhelming configuration screen.
5. Users receive clear feedback after scheduling, with obvious paths to review and extend the launch.

This should:
- Increase the % of logo creators who schedule at least one post (and at least one multi-language post).
- Reduce abandonment after logo download.
- Improve **time-to-first-scheduled-post**, bringing us closer to the "idea → graphic → scheduled post in 5–10 minutes" north star for this flow.