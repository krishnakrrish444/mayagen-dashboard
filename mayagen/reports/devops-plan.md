# DevOps & Migration Plan: mayagen.ai (CRA to Next.js)

## 1. Vercel Hosting Analysis & Migration Plan

### Current State: React CRA on Vercel
- **Architecture:** Client-side rendering (CSR).
- **Routing:** `react-router-dom` handling client-side routes; Vercel rewrites all requests to `index.html`.
- **Performance:** Initial load can be heavy due to large JS bundles; SEO is limited to what crawlers can execute.
- **Vercel Config:** Likely minimal `vercel.json` or zero-config relying on framework detection.

### Target State: Next.js on Vercel
- **Architecture:** Hybrid (SSG, SSR, ISR, and CSR).
- **Routing:** File-system based routing (App Router recommended for future-proofing, or Pages Router for easier migration).
- **Performance:** Faster FCP/LCP via server rendering and automatic code splitting.
- **Edge Capabilities:** Middleware for auth/redirects at the edge.

### Migration Phases

#### Phase 1: Environment Setup & Hybrid Boot
1.  **Initialize Next.js:** Install `next`, `react`, `react-dom` in the existing repo or a new monorepo structure.
2.  **Dual Mode:** Run Next.js alongside CRA temporarily if the app is massive, or go for a "strangler fig" pattern where new pages are Next.js and old ones are proxied. *Recommendation: Full cutover for standard-sized apps.*
3.  **Configuration:** Update `vercel.json` to prioritize the Next.js build output.

#### Phase 2: Code Migration
1.  **Routing:** Replace `react-router-dom` with `next/link` and `next/navigation` (or `next/router`).
    *   *Action:* Audit all `useHistory` / `useNavigate` hooks.
2.  **Asset Handling:** Move static assets from `public/` (CRA style) to Next.js `public/` (compatible, but ensure references use root paths).
3.  **Data Fetching:** Refactor `useEffect` data fetching to Server Components (App Router) or `getServerSideProps`/`getStaticProps` (Pages Router) where SEO/performance is critical.
4.  **Styling:** Ensure global CSS and component-level CSS (Modules/Tailwind) are compatible. Next.js has built-in support for both.
5.  **SEO:** Port `react-helmet` meta tags to Next.js Metadata API (App Router) or `next/head`.

#### Phase 3: Vercel Switchover
1.  **Build Command:** Change from `react-scripts build` to `next build`.
2.  **Output Directory:** Change from `build/` to `.next/`.
3.  **Environment Variables:** Prefix public variables with `NEXT_PUBLIC_` instead of `REACT_APP_`.
    *   *Script:* Automated find-and-replace script for the codebase.

---

## 2. CI/CD Pipeline Strategy (GitHub Actions)

### Workflow Design

We will implement three core workflows: `ci-check.yml`, `preview-deploy.yml`, and `production-deploy.yml`.

#### A. Continuous Integration (`ci-check.yml`)
*Trigger:* Pull Requests targeting `main` or `develop`.

1.  **Linting:** `npm run lint` (ESLint + Prettier).
2.  **Type Checking:** `tsc --noEmit`.
3.  **Unit Tests:** `npm run test` (Jest/Vitest).
4.  **Build Check:** `npm run build` (Ensures the app actually builds without errors).

#### B. Preview Deployments (`preview-deploy.yml`)
*Trigger:* Push to feature branches (or handled natively by Vercel Integration).

*Recommendation:* Use **Vercel's Native GitHub Integration** for previews rather than manual GH Actions for deploying. It is faster, zero-config, and provides comment hooks.
*   **Action:** Enable Vercel for GitHub.
*   **Settings:** "Automatically deploy all branches" = ON.

#### C. Production Release (`production-deploy.yml`)
*Trigger:* Push/Merge to `main`.

1.  **End-to-End Testing:** Run Playwright/Cypress tests against the *preview* URL before promoting, or against a staging environment.
2.  **Semantic Release (Optional):** Automate versioning and changelog generation based on commit messages.
3.  **Production Promotion:** Vercel automatically deploys `main` to production.
4.  **Post-Deploy Verification:** Run a lightweight "smoke test" suite against the live production URL.

### Automated Testing Strategy
-   **Unit:** Jest/Vitest for logic/utils.
-   **Component:** React Testing Library for UI components.
-   **E2E:** Playwright. Critical user paths (Login -> Generate -> Download).

---

## 3. Monitoring Stack Recommendation

### Recommendation: The "Vercel Native + Sentry" Stack

This combination offers the lowest friction and highest fidelity for Next.js apps.

| Tool | Role | Why? |
| :--- | :--- | :--- |
| **Vercel Analytics** | Real User Monitoring (RUM) | Zero-config Web Vitals (LCP, FID, CLS). Shows exactly how real users experience speed per route. |
| **Sentry** | Error Tracking & APM | Best-in-class stack traces for Next.js (server & client). Connects frontend errors to backend traces. |
| **Vercel Logs** | Log Aggregation | Built-in run-time logs. For advanced querying, integrate with **Axiom** or **Datadog**. |

### Configuration Steps
1.  **Sentry:**
    *   Install `@sentry/nextjs`.
    *   Use `npx @sentry/wizard -i nextjs` for auto-setup.
    *   Upload source maps during build (handled by the wizard's Webpack plugin).
2.  **Vercel Analytics:**
    *   Enable in Vercel Dashboard.
    *   Add `<Analytics />` component to root layout.

*Alternative:* **LogRocket** if "session replay" is critical for debugging UI UX issues (seeing exactly what the user clicked).

---

## 4. 301 Redirect Strategy

Migration URL structures often change. We must preserve SEO equity.

### Strategy: `next.config.js` Redirects

Next.js handles redirects efficiently at the edge.

### Redirect Map (Example)

| Old Path (CRA) | New Path (Next.js) | Type | Reason |
| :--- | :--- | :--- | :--- |
| `/home` | `/` | 301 | Canonicalize root |
| `/user/:id` | `/profile/:id` | 301 | Semantic renaming |
| `/about-us` | `/company/about` | 301 | Structural change |

### Implementation Details

1.  **Bulk Redirects:** Use `next.config.js`:
    ```javascript
    module.exports = {
      async redirects() {
        return [
          {
            source: '/old-blog/:slug',
            destination: '/blog/:slug',
            permanent: true, // 301
          },
        ]
      },
    }
    ```
2.  **Vercel Middleware:** For complex, dynamic, or massive lists (1000+ redirects), use Vercel Middleware (`middleware.ts`). It runs before the cache and is faster.
3.  **Fallback:** Ensure a custom `not-found.js` (404 page) is polished to catch any missed URLs.

### Verification
-   **Pre-Launch:** Write a script to curl old URLs and assert 301 status + correct location header.
-   **Post-Launch:** Monitor 404s in Vercel Analytics/Sentry immediately after go-live to patch gaps.
