# Product Mockups → Campaign Mode Planner & Multilingual UX v2

Goal: Make the "mockup → ads → Campaign Mode" path feel like a guided, 5–10 minute flow from idea to scheduled campaign, while keeping multilingual simple and non-chaotic in the planner/scheduler.

## 1. Entry into Campaign Mode Planner

### 1.1 Primary entry CTAs
- On Product Mockups landing page and in-tool completion screen, promote:
  - **Primary:** "Use in ads & campaign" (opens Ads step with selected mockups preloaded)
  - **Secondary:** "Download images" (file export only)
- Add a short expectation line under the primary CTA:
  - "Turn these mockups into a 1‑week campaign in about 5 minutes."

### 1.2 Deep-link behavior
- `Use in ads & campaign` should deep-link into planner with:
  - `mode = "campaign"`
  - `source = "product_mockups"`
  - `campaign_seed = { mockup_ids, brand_id, suggested_channels }`
- If the user arrives from elsewhere (e.g., planner home), Campaign Mode behaves identically but without pre-seeded mockups.

## 2. Campaign Mode Planner Surface

### 2.1 Scoped calendar
- Campaign Mode should present a **scoped, minimal calendar**:
  - Time range: default to 7–10 days (configurable, default 7 for v1) starting from next available slot.
  - Channels: show only the 1–3 channels chosen in the Ads step.
  - View: strip down to a **list/strip view** of posts rather than full month grid.
- Top-level label: "Product Mockups Campaign" with a subline:
  - "Review and schedule your campaign in 3 quick steps."

### 2.2 Stepper + checklists
- Persistent stepper (top of planner pane):
  1. Mockups
  2. Ads
  3. Schedule
- Highlight current step (Schedule) with copy:
  - "Final step: confirm times & languages, then schedule."
- Right-hand or inline checklist:
  - [ ] Review post timings
  - [ ] Add languages (optional)
  - [ ] Confirm schedule

## 3. Base Post + Language Variants Model

### 3.1 Data model
- Treat each **post concept** as a **base post** with 0–N language variants.
- In Campaign Mode list view:
  - Show each base post once, with a small language pill row beneath (e.g., `EN`, `+2` if more).
  - Collapse individual language variants behind a chevron/disclosure.

### 3.2 UI behavior
- Default: one language (EN or brand default). No variants visible until user opts in.
- Expanding a base post row reveals:
  - A sublist of language variants with channel icons and scheduled time.
  - Edit / remove controls per variant.

## 4. Multilingual UX — Simple, Optional Upgrade

### 4.1 Add language control
- On the campaign overview (above post list), show:
  - Text: "Want more reach?"
  - Button: **+ Add language**.
- Clicking opens a dialog:
  - Title: "Add languages to this campaign"
  - Body guidance: "Start with 1–3 extra languages so your calendar stays tidy. You can always add more later."
  - Language selection:
    - Show recommended languages based on brand/locale.
    - Soft limit: 3 selected by default; show soft warning above 3:
      - "More languages = more rows in your calendar. We recommend 1–3 to keep things simple."

### 4.2 Language generation & preview
- After confirming languages:
  - Generate variants for all posts in the campaign.
  - Immediately show a **language review modal**:
    - Left: list of posts with base language.
    - Right: tabs or dropdown for each added language.
    - Per-language checks:
      - [ ] Looks good
      - [ ] Needs edit (inline editor)
  - CTA: **Apply to campaign** (schedules variants into Campaign Mode view).

## 5. Scheduling Controls — 5–10 Minute Path

### 5.1 Smart defaults
- When entering Schedule step:
  - Pre-fill times for each base post according to an opinionated pattern:
    - e.g., 3–5 posts over 7 days, spaced at recommended local times.
  - For multilingual variants:
    - Default to same day as base post, offset by 0–2 hours.
- Show an info line:
  - "We've picked publish times for you. You can drag or click to adjust before scheduling."

### 5.2 Single primary CTA
- Prominent button at bottom/right:
  - **Schedule this campaign**
- Secondary link:
  - "Adjust times individually" (focuses user on granular editing if needed).

### 5.3 Inline editing
- Clicking on a time opens a lightweight inline time picker.
- Drag-and-drop supported where feasible, but avoid requiring it for first-time completion.

## 6. Confirmation & Return Paths

### 6.1 Post-schedule confirmation
- After clicking **Schedule this campaign** and success:
  - Full-screen or modal confirmation:
    - Title: "Your campaign is scheduled"
    - Summary bullets:
      - X posts scheduled over Y days
      - Channels: list
      - Languages: `EN + N more`
    - Primary CTA: **View campaign in calendar**
    - Secondary CTA: **Duplicate for another product**

### 6.2 Calendar view after confirmation
- Deep-link into planner with:
  - Campaign filter on (`campaign_id`), showing only the scheduled campaign posts.
  - A small helper strip at top:
    - "You can edit times or languages here. Your changes will update the campaign automatically."

## 7. Analytics Hooks (UX-facing)

To support UX decisions and iteration, ensure the following events (names indicative) are fired and available in dashboards:

- `campaign_mode_opened_from_product_mockups` (with properties: `mockups_count`, `channels_selected`)
- `campaign_language_dialog_opened` (properties: `current_languages_count`)
- `campaign_languages_added` (properties: `languages_added_count`, `total_languages_count`)
- `campaign_schedule_default_accepted` vs `campaign_schedule_customized`
- `campaign_scheduled_from_mockups` (properties: `posts_count`, `languages_count`, `time_to_first_scheduled_campaign_seconds`)

These events should be wired consistently with Analytics v2 and used to track:
- Drop-offs between Ads and Schedule.
- Adoption of multilingual (1–3 languages vs 4+).
- Median time from first mockup completion → first scheduled campaign.

## 8. Guardrails & Edge Cases

- If the user deselects all languages except the base one, treat it as a normal single-language campaign; avoid error states.
- For high-language-count brands (enterprise):
  - Show a non-blocking banner when they exceed 5–6 languages:
    - "This will create many entries in your calendar. Consider starting with fewer languages or using language groups."
- Ensure all destructive actions (removing posts, removing languages) require light confirmation, not full modals.

---

This spec should be translated into Figma mocks for:
- Campaign Mode planner list/strip view.
- Base post with grouped language pill row.
- + Add language dialog and language review modal.
- Schedule step with stepper and checklist.
- Post-schedule confirmation and filtered calendar view.
