# Logo Maker → Launch Week Planner: UX Gaps & Refinements (v1)

_Last updated: 2026-02-13 — Shuri (@product-ux)_

This note builds on:
- `/mayagen/reports/logo-maker-logo-to-launch-planner-multilingual-ux-v2.md`
- `/mayagen/reports/logo-maker-logo-to-launch-5-minute-path-v1.md`

Focus: **where a first-time user can still slip or get confused inside Launch Week planner**, even with v2 specs, and concrete refinements to keep the path close to:

> Idea → logo → launch assets → scheduled posts (in ~5–7 minutes), including 1–3 extra languages.

---
## 1. Entry Confusion: "What just happened?"

**Friction**
- From the user’s perspective, they were in a **wizard** (Logo → Brand Kit → Launch Assets), and suddenly they’re inside a **calendar**.
- Even with scoped Launch Week mode, it can feel like a context switch: "Did my logo work finish? Am I now in some other tool?"

**Refinements**
1. **Wizard shell persists into planner**
   - Keep the same 4-step header/stepper used earlier:
     - `1 · Logo` → `2 · Brand Kit` → `3 · Launch posts` → `4 · Schedule`
   - In planner/Launch Week mode, highlight step 4 with text: `Step 4 of 4 — Schedule launch (about 1 minute)`.

2. **Inline recap strip on entry**
   - At top of planner, show a compact recap:
     - Logo thumbnail + brand name.
     - Text: `Launch week for [Brand Name]`.
     - Subcopy: `We’ve created X posts over Y days. Review, (optionally) add languages, then schedule.`
   - This reduces the feeling of a hard context switch and reinforces that they’re still on-rails.

3. **Return affordances stay clear**
   - Small text link near the recap: `Back to launch posts` (goes back one step in the wizard, not out of the flow entirely).
   - Avoid any global nav links that look like primary exits; demote them visually while in guided mode.

---
## 2. "Schedule launch week" Anxiety

**Friction**
- The primary CTA is powerful and slightly scary: users may worry they’ll "publish now" or do something irreversible.
- Especially true if they haven’t edited times or languages; they may stall instead of clicking.

**Refinements**
1. **Clarify behavior directly on the button**
   - Label: `Schedule launch week`.
   - Sub-label (small text under CTA): `We’ll keep your posts as scheduled drafts until their time comes. You can edit or cancel anytime.`

2. **Pre-confirmation tooltip on hover** (desktop)
   - Short hint: `Nothing goes live immediately — you’re just locking in your launch plan.`

3. **First-run interstitial for cautious users**
   - On the **very first** Logo → Launch Week run, if the user opens the time picker or language dialog but then hovers the CTA for >2–3 seconds, show a one-time helper:
     - Title: `You can change this later`
     - Copy: `Scheduling now just saves your launch plan. You can tweak times and text before posts go out.`

---
## 3. Planner Overwhelm on Mobile

**Friction**
- Launch Week mode is scoped, but on small screens, a week calendar plus checklists plus language chips can still feel crowded.
- Risk: users drop because they can’t see the relationship between posts, times, and languages.

**Refinements**
1. **Mobile-first stacked layout**
   - Replace grid-style calendar with a **chronological list** for Launch Week on small screens:
     - `Day & date` heading (e.g., `Mon 14 Feb`).
     - Under each day, show Base Post cards with time + language chips.
   - Keep one floating CTA bar at bottom: `Schedule launch week`.

2. **Checklist collapses into top ribbon**
   - On mobile, show the 3 checklist items as a compact progress ribbon:
     - `1 Review` · `2 Languages` · `3 Schedule` with ticks as they complete.
   - Tapping an item scrolls to the relevant section or opens the language dialog.

3. **Language variants as chips, not rows**
   - Never render each language as a separate row on mobile; always group via chips on the Base Post.

---
## 4. Multilingual Review: Too Many Places to Click

**Friction**
- v2 introduces a Language Review modal, language chips on posts, and the `+ Add language` dialog. There’s a risk of users bouncing between them without a clear mental model.

**Refinements**
1. **Single canonical entry to deep review**
   - Treat the **Language Review modal** as the main place for cross-post language review.
   - From the planner, language chips should:
     - Open the modal at the corresponding post + language, instead of opening a separate inline editor.

2. **Explicit "Done for now" state**
   - At the end of the Language Review modal, show:
     - Summary: `You’ve reviewed X posts across Y languages.`
     - CTA: `Back to launch week`.
     - Subcopy: `You can always update language text from the calendar later.`

3. **Guard against over-translation**
   - In the `+ Add language` dialog, show an inline hint if users scroll through a long list:
     - `For this launch, we recommend starting with 1–3 extra languages so your calendar stays tidy.`

---
## 5. After Launch: "Where Did My Flow Go?"

**Friction**
- Once the user has scheduled launch week, it’s easy for the guided experience to disappear into the larger app.
- If they come back a day later, they should not have to re-learn how to find their launch.

**Refinements**
1. **Guided-mode state on dashboard**
   - For any active Logo-based launch, show a card:
     - `Your [Brand Name] launch is underway`.
     - Progress snippet: `X of Y posts sent • EN + N languages`.
     - CTA: `View launch week` (returns to scoped Launch Week planner with the same simplified header and checklist, now in a "progress" state).

2. **Launch filter preset in full planner**
   - Save a reusable filter preset: `Logo launch for [Brand Name]`.
   - When users click `View in full planner` from the guided mode, apply this preset and visually tag it as such, so they understand why the calendar looks the way it does.

3. **Re-entry from Logo Maker**
   - If the user re-opens Logo Maker for the same brand while a launch is scheduled, show a light touch banner:
     - `You already have a launch week scheduled for [Brand Name].`
     - CTAs: `View launch` (planner scoped) • `Create more assets`.

---
## 6. Summary for Implementation

The existing specs get us most of the way to a 5–7 minute guided path. The key remaining risks are **context switching**, **CTA anxiety**, and **mobile overwhelm**.

Concrete changes to prioritize:
1. Extend the wizard shell (stepper + time hints) into Launch Week planner.
2. Add an entry recap strip and a clear "Back to launch posts" affordance.
3. Make the behavior of `Schedule launch week` feel reversible and safe via sub-label + one-time helper.
4. Simplify the mobile layout to a chronological list with a single floating CTA and a compact checklist ribbon.
5. Use the Language Review modal as the canonical deep-review surface, with language chips acting as anchors into it.
6. Preserve a guided-mode re-entry path from both dashboard and Logo Maker, so the launch story stays coherent over days, not just minutes.

These refinements should reduce drop-off in the planner step, especially on mobile, and make multilingual adoption feel like a small, safe upgrade instead of a structural change to how the calendar works.