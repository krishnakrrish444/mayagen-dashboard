# Analytics & Tracking Plan for Mayagen.ai

## 1. Executive Summary & Stack Recommendation

**Objective:** To gain deep visibility into user behavior, optimize the activation funnel, and drive retention for the new Next.js platform.

### Recommended Stack: **PostHog**
**Why PostHog?**
*   **All-in-One Platform:** Combines product analytics, session replay, feature flags, and A/B testing in one suite. This reduces tool fatigue and integration complexity for the engineering team.
*   **Next.js Native:** Excellent first-party support for Next.js (App Router) and React.
*   **Cost-Effective:** Generous free tier (1M events/mo) is perfect for early-stage growth compared to Amplitude's steep entry pricing.
*   **Open Source Roots:** greater data control and privacy options if self-hosting becomes necessary later (though Cloud is recommended for now).
*   **Session Replay:** crucial for seeing *why* users drop off in the design editor, not just *where*.

**Runner Up:** Mixpanel (Great for pure analysis, but lacks session replay/feature flags natively).
**Avoid:** Amplitude (Overkill and too expensive for current stage).

---

## 2. Key Metrics Dashboard (The "Morning Coffee" View)

This dashboard is designed for SK to review daily. It answers: "Is the product growing, and are people finding value?"

### North Star Metric
*   **Weekly Active Creators (WAC):** Users who created or edited at least one design in the last 7 days.

### Section A: Growth & Acquisition
1.  **Signups (Daily/Weekly):** Total new accounts created.
2.  **Activation Rate:** % of new signups who reach the "Aha!" moment (Exported a Design) within 24 hours.
3.  **Traffic Source Breakdown:** Where are high-value users coming from? (Direct, SEO, Social).

### Section B: Engagement & Retention
4.  **DAU / MAU Ratio:** Stickiness indicator (Target > 20%).
5.  **Retention Curves:** Cohort analysis showing % of users returning to *create* (not just login) in Week 1, Week 4, and Week 12.
6.  **Designs per User:** Average number of designs created per active user (measure of depth).

### Section C: Monetization (Future-proofing)
7.  **Upgrade Intent:** Total unique users clicking "Upgrade" or hitting paywalls.
8.  **Free-to-Paid Conversion:** % of users converting to a paid plan (if applicable).

---

## 3. User Properties Schema

These properties allow us to segment users into meaningful groups (e.g., "Power Users" vs. "Casuals").

| Property Name | Data Type | Description | Example Values |
| :--- | :--- | :--- | :--- |
| `plan_tier` | String | Current subscription level | `free`, `pro`, `enterprise` |
| `total_designs_created` | Number | Lifetime count of designs | `15`, `0`, `142` |
| `last_design_date` | ISO Timestamp | Date of last creation activity | `2023-10-27T10:00:00Z` |
| `signup_source` | String | Where they came from | `google`, `referral`, `twitter` |
| `is_power_user` | Boolean | True if > 5 designs/week (Computed) | `true`, `false` |
| `account_age_days` | Number | Days since signup | `45` |
| `primary_use_case` | String | Self-selected during onboarding | `social_media`, `print`, `ads` |

---

## 4. Tracking Plan (Event Schema)

### Naming Convention
*   **Format:** `Object Action` (Noun-Verb) to keep events sorted by feature.
*   **Casing:** Title Case (e.g., `Design Created`).

### Core Events

#### A. Authentication & Onboarding
| Event Name | Trigger | Key Properties | Business Question |
| :--- | :--- | :--- | :--- |
| `User Signed Up` | Successful account creation | `method` (email/google), `referral_code` | How is our acquisition funnel performing? |
| `Onboarding Completed` | User finishes the welcome flow | `duration_seconds`, `selected_role` | Is onboarding too long? |

#### B. Creation Workflow (The Core Loop)
| Event Name | Trigger | Key Properties | Business Question |
| :--- | :--- | :--- | :--- |
| `Template Selected` | User clicks a template to start | `template_id`, `category`, `search_term` | Which templates drive usage? |
| `Design Created` | Editor loads successfully | `source` (blank/template), `design_id` | Top of the creation funnel. |
| `Element Added` | User adds text, image, or shape | `type` (text/image/shape), `library_source` | How do users build designs? |
| `AI Generation Started` | User prompts the AI | `prompt_length`, `mode` (image/text) | Is AI feature being discovered? |
| `AI Generation Completed`| AI returns a result | `latency_ms`, `success` (true/false) | Is the AI performant? |

#### C. Value Realization (The "Aha!" Moment)
| Event Name | Trigger | Key Properties | Business Question |
| :--- | :--- | :--- | :--- |
| `Design Exported` | User downloads/shares final output | `format` (png/jpg), `quality` | **Primary Conversion Event** |
| `Design Shared` | User generates a public link | `platform` (link/email) | Is virality working? |

#### D. Monetization & Friction
| Event Name | Trigger | Key Properties | Business Question |
| :--- | :--- | :--- | :--- |
| `Paywall Hit` | User tries a paid feature | `feature_name`, `trigger_location` | What drives upgrade intent? |
| `Upgrade Clicked` | User clicks "Upgrade" button | `page_location` | High intent to purchase. |
| `Subscription Started` | Successful payment | `plan_id`, `mrr_value`, `interval` | Revenue realization. |

---

## 5. Implementation Guide (Next.js)

1.  **Install SDK:** `npm install posthog-js`
2.  **Initialize:** Create a `providers.tsx` client component to wrap the app.
3.  **Capture:** Use `posthog.capture('Event Name', { property: 'value' })` in your event handlers.
4.  **Identify:** Call `posthog.identify(userId, { userProperties })` immediately after login.
