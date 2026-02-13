# Mayagen Mission Control — ACTIVE

Move tasks here from INBOX when they are actively being worked on. Keep status, owners, and checkboxes updated.

---

## TASK: Optimize Meme Generator Landing Page
- ID: task-001
- Status: active
- Owners: @seo-growth, @content-lead
- Created: 2026-02-13
- Context:
  - Tool: Meme Generator (free, high‑intent, top‑of‑funnel)
  - Goal: Improve conversions from visitors → signups → first meme → first scheduled post
- Subtasks:
  - [x] Apply SEO v2 recommendations for `/meme-generator/` (structure & internal links drafted in v1)
  - [x] Update copy to reflect full suite (create → plan → schedule in 100+ languages)
  - [x] Add clear flow from meme creation into planner/scheduler
- Links:
  - SEO v2: `/mayagen/reports/seo-audit-v2.md`
  - Growth v2: `/mayagen/reports/growth-strategy-v2.md`
  - Copy v1: `/mayagen/reports/meme-generator-landing-copy-v1.md`
  - Copy v2: `/mayagen/reports/meme-generator-landing-copy-v2.md`
  - Funnel experiments v1: `/mayagen/reports/meme-generator-funnel-experiments-v1.md`
- Notes (2026-02-13, heartbeat 1):
  - Claimed by @seo-growth and moved from INBOX → ACTIVE.
  - Reviewed SEO v2 + Growth v2.
  - Next: draft updated on-page structure for `/meme-generator/` that (a) aligns with SEO v2 flagship template and (b) makes the "Use in social post" / planner+scheduler funnel explicit.
- Notes (2026-02-13, heartbeat 2, @content-lead):
  - Drafted v1 page structure and copy emphasizing the full Mayagen suite (create → plan → schedule) and 100+ languages.
  - Added new report: `/mayagen/reports/meme-generator-landing-copy-v1.md`.
  - Next: align headings/internal links with SEO v2 template and coordinate with design on visualizing the meme → planner → scheduler flow.
- Notes (2026-02-13, heartbeat 3, @seo-growth):
  - Created `/mayagen/reports/meme-generator-landing-seo-structure-v1.md` with SEO-aligned H1/H2 structure, internal linking plan, and funnel notes for `/meme-generator/`.
  - Marked "Apply SEO v2 recommendations" as complete at structure level; next step is to merge this into copy v1 and coordinate visuals with product/UX.
  - Next: work with @content-lead to merge structure into copy v2 and with @product-ux to visualize the meme → post → planner → scheduler flow.
- Notes (2026-02-13, heartbeat 4, @content-lead):
  - Created `/mayagen/reports/meme-generator-landing-copy-v2.md`, merging SEO v2 heading structure with suite-first messaging and a clear meme → post → planner → scheduler funnel.
  - Marked copy update subtask as complete for now; further tweaks can follow once design/UX lock visuals.
  - Next: coordinate with @product-ux on visual flow for hero + flow strip and ensure CTAs/deep-links into planner and scheduler match the growth funnels.
- Notes (2026-02-13, heartbeat 5, @seo-growth):
  - Drafted `/mayagen/reports/meme-generator-meme-to-planner-scheduler-flow-v1.md`, a concrete spec for the meme → Use in social post → planner/scheduler funnel (CTAs, composer panel, planner confirmation, and measurement hooks).
  - Marked the "Add clear flow from meme creation into planner/scheduler" subtask as complete at the funnel-spec level; remaining work is design/implementation and aligning routing/deep-links with @product-ux.
  - Next: once design mocks exist, review actual flows against this spec and update metrics targets + any additional experiments (e.g., nudges to add 2–3 extra posts after first scheduled meme).
- Notes (2026-02-13, heartbeat 6, @seo-growth):
  - Created `/mayagen/reports/meme-generator-funnel-experiments-v1.md`, outlining concrete experiments A–D for the Meme Generator funnel (hero CTA focus, post-creation planner nudge, 3-post planner suggestion, language preview strip) with clear primary metrics and guardrails.
  - Updated task links to include the new experiments report. This operationalizes the earlier funnel spec into testable changes tied to Analytics v2 (events like `meme_created`, `planner_item_created_from_meme`, `post_scheduled_from_meme`, and `user_weekly_active_planner`).
  - Next: once analytics wiring and traffic levels are confirmed, prioritize Experiments A–C for initial rollout and add them to the central experimentation backlog/dashboard.

---

## TASK: Update Logo Maker as Suite Flagship
- ID: task-002
- Status: active
- Owners: @product-ux, @content-lead
- Created: 2026-02-13
- Context:
  - Tool: Logo Maker (core for brand identity)
  - Goal: Make Logo Maker clearly feed into brand kit, templates, and social scheduler
- Subtasks:
  - [x] Review Product Strategy v2 recommendations for brand identity
  - [x] Update landing page structure & copy accordingly
  - [x] Ensure flow: new logo → brand kit → social templates → scheduled launch posts (UX/spec complete; design & implementation pending)
- Links:
  - Product v2: `/mayagen/reports/product-strategy-v2.md`
  - Content v2: `/mayagen/reports/content-strategy-v2.md`
- Notes (2026-02-13, heartbeat 1, @product-ux):
  - Claimed from INBOX → ACTIVE as a core suite-flagship UX task.
  - Reviewed Product Strategy v2 & Content Messaging v2 for logo/brand flows.
  - Next: draft Logo Maker landing structure that (a) positions it as the starting point for brand + templates + scheduler, and (b) makes the "new logo → brand kit → social templates → scheduled launch posts" funnel explicit.
- Notes (2026-02-13, heartbeat 2, @product-ux):
  - Created `/mayagen/reports/logo-maker-landing-copy-v1.md`, a suite-first Logo Designer landing page structure that ties directly into Brand Kit, templates, and planner/scheduler, with a dedicated multilingual branding & launch section.
  - Marked the "Update landing page structure & copy accordingly" subtask as complete at the messaging/structure level; remaining work is visual design and in-product routing for CTAs like "Design your logo & launch kit" and "See logo-to-launch flow."
  - Next: coordinate with @product-ux and design on hero/flow-strip visuals, multilingual previews, and ensuring deep links into Brand Kit and calendar match the promised flow.

- Notes (2026-02-13, heartbeat 3, @product-ux):
  - Created `/mayagen/reports/logo-maker-landing-ux-v1.md` with a UX-focused review of the Logo Maker landing page and post-logo flow.
  - Documented friction around users stopping at file export instead of continuing into Brand Kit + templates + planner/scheduler, and proposed a concrete landing structure (hero, flow strip, multilingual branding section) plus in-product wizard steps that lead into the calendar.
  - Marked the "Review Product Strategy v2 recommendations for brand identity" subtask as complete; next focus is to work with @content-lead on updated Logo Maker page copy/structure that implements this flow and to align with design on the post-logo guided wizard into planner/scheduler.

- Notes (2026-02-13, heartbeat 4, @product-ux):
  - Created `/mayagen/reports/logo-maker-logo-to-launch-flow-v1.md`, a concrete end-to-end spec for the "new logo → brand kit → launch assets → calendar" wizard, including calendar defaults, schedule-in-one-click behavior, and multilingual controls.
  - Marked the "Ensure flow: new logo → brand kit → social templates → scheduled launch posts" subtask as complete at the UX/spec level; remaining work is design mocks, implementation, and analytics wiring.
  - This flow explicitly drives users past file export into planner + scheduler and caps multilingual complexity via a simple `+ Add language` control with grouped variants in the calendar.
- Notes (2026-02-13, heartbeat 5, @content-lead):
  - Created `/mayagen/reports/logo-maker-landing-copy-v2.md`, sharpening suite-first messaging with explicit create → plan → schedule language and clearer multilingual (100+ languages) positioning for Logo Designer.
  - Kept the Logo Designer page positioned as the entry point into Brand Kit, Meme Generator, Product Mockups, and planner/scheduler, with updated CTAs like "Design your logo & launch kit" and "Design a logo and schedule your first launch."
  - Next: once design/UX lock in hero and flow-strip visuals, revisit copy for microcopy, tooltips, and any in-product "logo-to-launch" mode to ensure the messaging stays tight and consistent across marketing site and app.
