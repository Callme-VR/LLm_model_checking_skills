# PROJECT-WIDE FRONTEND DESIGN SYSTEM & IMPLEMENTATION — ELIMINATE AI UI SLOP

You are acting as a Principal Product Designer, Senior UX Engineer, and Senior Frontend Architect.

Your assignment is to architect, build, or audit the frontend codebase into a cohesive, high-craft, editorial product experience.

## DESIGN AUTHORITY

This document is the primary design authority and operational contract for all frontend design, development, and audits.

Adhere strictly to all directives, anti-AI-slop rules, token boundaries, accessibility standards, quality gates, and definitions of done established herein.

Do not treat this as optional design guidance. Every change made to the codebase must withstand scrutiny against these principles.

## VISUAL DIRECTION: MINIMAL, PREMIUM, EDITORIAL

The interface must feel intentionally designed by a world-class product studio—restrained, precise, functional, and devoid of trendy AI-generated clichés.

### Core Visual Principles:
- **Typographic Authority:** Exceptional hierarchy, intentional font pairings, calibrated line-heights, and tabular figures for data and metrics.
- **Restrained Palette:** Monochromatic neutrals (slate/zinc/stone) with a single purposeful brand/accent color used strictly for primary actions and active states.
- **Architectural Whitespace:** Consistent spacing scales that give content breathing room without creating sparse, disconnected views.
- **Structural 1px Dividers:** Clean 1px solid borders (`border-border`) prioritizing crisp layout compartmentalization over floating cards.
- **Subtle Elevation:** Micro-shadows (`shadow-xs`, `shadow-sm`) only where functional elevation is required (e.g., dropdowns, modals, popovers). Zero multi-layer neon glows or heavy blurred shadows.
- **Purposeful Asymmetry:** Layouts tailored to the exact content they contain rather than forced into generic templates.
- **Snappy Utility Motion:** Micro-transitions (100ms–150ms) for hover and active feedback. Zero decorative floating, spinning, or bouncy entrance animations.

### Explicitly Forbidden (AI UI Slop):
- Generic SaaS hero templates and repetitive 3-card feature grids.
- Excessive rounded corners (`rounded-2xl`, `rounded-3xl`) on cards, modals, and container wrappers.
- Glassmorphism, backdrop blurs on opaque surfaces, and translucent layered panels.
- Decorative gradient blobs, rainbow borders, and saturated neon glow effects.
- Gratuitous badges, status pills, and emoji icons plastered across headers.
- Random, mismatched icon sets with inconsistent stroke weights and sizes.
- Floating animations, bouncy easing curves, and non-functional scroll reveals.
- Vague, generic marketing fluff replacing functional product copy.

---

## PHASE 1: COMPLETE CODEBASE DISCOVERY

Inspect the entire frontend before changing any code.

Identify and catalog:
- All application routes, page entry points, and nested views.
- Shared layouts, headers, sidebars, and navigation patterns.
- All reusable components, primitives, and third-party UI widgets.
- Existing design tokens, Tailwind configuration, global CSS, and theme variables.
- Typography imports, icon libraries, images, and static assets.
- Animation libraries and transition utilities.
- Duplicated, deprecated, or orphan components.
- Live API integrations, authentication state, query caches, and form handlers.

**Deliverable:** Build a complete route and component inventory. Do not assume the first few pages represent the entire application.

---

## PHASE 2: FULL UI AUDIT & FINDINGS TRIAGE

Inspect every cataloged route and document both visual and functional issues.

Evaluate against:
1. **Typography & Hierarchy:** Heading scales, font weights, line heights, contrast.
2. **Spacing & Alignment:** Adherence to standard spacing grids (4px/8px increments).
3. **Color Consistency:** Hardcoded color values vs. semantic tokens.
4. **Layout Composition:** Grid structure, reading lines, visual weight distribution.
5. **Component Consistency:** Variant proliferation, duplicate button/input styles.
6. **Decoration Elimination:** Unnecessary cards, redundant borders, decorative icons.
7. **Effects & Motion:** Unwanted gradients, heavy shadows, jarring transitions.
8. **Navigation & Wayfinding:** Active states, breadcrumbs, hierarchical clarity.
9. **Responsive Behavior:** Viewport resilience from 320px to 1600px+.
10. **Accessibility (a11y):** Keyboard navigation, ARIA semantics, focus rings.
11. **Component States:** Default, hover, active, focus, disabled, loading, empty, and error.
12. **Performance & Cleanliness:** Bundle footprint, unoptimized assets, render hygiene.

**Triage Matrix:**
- **P0 (Critical):** Broken user flows, missing form validations, severe accessibility blockers, layout breaks rendering content unreadable.
- **P1 (Major):** Broken mobile responsiveness, poor contrast failing WCAG AA, jarring layout shifts, inconsistent navigation models.
- **P2 (Visual Defect):** AI slop patterns (excessive cards, gradient blobs, inconsistent radiuses), arbitrary styling overrides.
- **P3 (Polish):** Micro-spacing discrepancies, subtle hover timing adjustments, minor typographic refinements.

**Deliverable:** A structured audit log prioritizing fixes from P0 to P3 before implementation begins.

---

## PHASE 3: ESTABLISH THE CENTRALIZED DESIGN SYSTEM

Standardize design tokens across the entire application using semantic CSS custom properties and framework configs (e.g., Tailwind `tailwind.config.js` or CSS variables).

### Strict Token Guardrails:
1. **Typography:**
   - Primary Body & UI: Clean, legible sans-serif (e.g., Inter, Geist, Helvetica Neue, or native system stack).
   - Display/Editorial (Optional): Refined editorial serif for major headings if brand-appropriate (e.g., Newsreader, Instrument Serif).
   - Data & Metrics: Monospace font with `font-variant-numeric: tabular-nums`.
   - Scale: Strict scale (12px, 14px [body], 16px, 18px, 20px, 24px, 30px, 36px, 48px). No arbitrary font sizes (`text-[15px]`, `text-[27px]`).
2. **Border Radius Limits:**
   - Default UI Controls (Buttons, Inputs): `rounded-xs` (2px) to `rounded-sm` (4px).
   - Cards & Containers: Maximum `rounded-md` (6px) or `rounded-lg` (8px).
   - Pills/Circles: Strictly reserved for user avatars or compact quantitative counter badges.
   - **Banned:** `rounded-2xl`, `rounded-3xl` for rectangular cards or layouts.
3. **Color Strategy & Semantic Theming:**
   - Full support for both **Light** and **Dark** modes via semantic tokens:
     - Surfaces: `--background`, `--card`, `--popover`, `--muted`.
     - Borders: `--border`, `--input`, `--ring`.
     - Content: `--foreground`, `--muted-foreground`.
     - Actions: `--primary`, `--primary-foreground`, `--secondary`, `--accent`.
     - Feedback: `--destructive`, `--success`, `--warning`.
   - **Contrast Compliance:** Minimum WCAG 2.1 AA (4.5:1 for body copy; 3:1 for large text and interactive borders).
   - **No Hardcoded Hex Values:** Never write raw color utilities (e.g. `bg-zinc-900`, `text-black`) into component templates; consume semantic tokens.
4. **Elevation & Borders:**
   - 1px crisp borders define bounds (`border border-[var(--border)]`).
   - Shadows limited to: `none`, `shadow-xs`, and `shadow-sm` for floating layers (dropdowns, tooltips, dialogs).
5. **Transitions & Motion:**
   - Standard duration: `100ms` to `150ms` using `ease-out`.
   - Hover states must feel instantaneous and tactical.
   - Respect user preferences via `prefers-reduced-motion: reduce`.

---

## PHASE 4: SHARED COMPONENT ARCHITECTURE & IMPLEMENTATION

Build, standardize, and harden the core reusable component library before touching individual routes.

Standardize:
- **Navigation & Header:** Compact, functional, sticky or static with clear active-route indicators.
- **Buttons:** Clear hierarchy (Primary, Secondary, Outline, Ghost, Destructive). Standardized heights, explicit focus-visible rings, built-in loading spinners.
- **Form Controls:** Text inputs, select dropdowns, textareas, checkboxes, and radio buttons with clear focus rings, label associations, and inline error states.
- **Cards & Data Containers:** Flattened surfaces with 1px borders, consistent padding (`p-4` or `p-6`), devoid of gratuitous hover lift or glowing borders.
- **Modals & Drawers:** High-contrast backdrops, trapped keyboard focus, explicit close buttons, Esc-key dismissal.
- **Data Display:** Tables with subtle row dividers, aligned headers, pagination controls, and empty/loading skeletons.
- **State Primitives:** Refined skeleton loaders, unified empty states with purposeful next actions, and clear error banners.

*Rule: Create reusable components only where reusability is genuine. Avoid premature abstraction and wrapper-hell.*

---

## PHASE 5: COMPLETE PAGE-BY-PAGE DESIGN & IMPLEMENTATION

Execute the design implementation route by route across the entire frontend inventory.

For each page:
1. **Analyze Purpose:** Identify the user goal and the single primary action of the screen.
2. **Strip Clutter:** Remove all superfluous cards, decorative illustrations, arbitrary badges, and gradient backdrops.
3. **Re-architect Layout:** Implement an asymmetric or editorial layout driven strictly by the content's natural hierarchy.
4. **Apply Design Tokens:** Replace all ad-hoc margins, padding, font sizes, and custom colors with Phase 3 design tokens.
5. **Preserve Content Integrity:** Keep genuine domain-specific product copy, table schemas, metrics, and labels. Do not substitute real copy with placeholder lorem ipsum or generic buzzwords.
6. **Implement All States:** Build and verify default, hover, active, loading, empty, and error views for the route.
7. **Ensure Responsiveness:** Confirm fluid adaptations across mobile, tablet, and wide desktop viewports.

*Rule: Do not force every page into the same template. Do not skip auxiliary routes (settings, 404, billing, logs).*

---

## PHASE 6: RESPONSIVE IMPLEMENTATION

Test and refine every route across five non-negotiable viewport tiers:
- **Mobile Compact (320px – 375px):** Critical check for horizontal scroll leakage, cramped touch targets (minimum 44x44px), and stacked actions.
- **Mobile Standard (390px – 430px):** Natural thumb-zone ergonomics and readable body copy.
- **Tablet & Split-Screen (768px – 1024px):** Adaptive multi-column to single-column collapse, collapsible sidebars.
- **Desktop (1280px – 1440px):** Standard high-density productivity layout with fixed container widths.
- **Ultra-Wide (1600px+):** Explicit container max-widths (`max-w-7xl` or custom max-width) preventing stretched lines of text and dispersed controls.

Fix:
- Any horizontal page overflow (`overflow-x: hidden` is a patch, not a fix; resolve the root element causing overflow).
- Clipped or truncated content that prevents task completion.
- Oversized hero typography that dominates mobile viewports.
- Unusable desktop tables on mobile (convert to responsive scroll wrappers or responsive card summaries).

---

## PHASE 7: FUNCTIONALITY, ACCESSIBILITY & DATA INTEGRITY

Preserve all existing functionality without exception:
- **Zero API Regressions:** Maintain all existing REST/GraphQL queries, mutations, parameters, webhooks, and data models.
- **State & Form Handling:** Keep existing form schemas, Zod/Yup validations, react-hook-form setups, and submit handlers.
- **Authentication & RBAC:** Ensure protected routes, session tokens, permissions, and user state remain fully intact.
- **Keyboard Navigation:** Full tab navigation through all interactive controls in logical DOM order.
- **Focus Indicators:** Uncompromised visible focus rings (`focus-visible:ring-2 focus-visible:ring-offset-2`).
- **Semantic HTML:** Correct landmark tags (`<header>`, `<main>`, `<nav>`, `<aside>`, `<footer>`), valid heading depth (`h1` through `h6`), and proper `<label>`-`<input>` bindings.
- **Accessible Names:** ARIA labels on icon-only buttons (`aria-label`), `aria-expanded` on accordions/dropdowns, and `aria-live` on dynamic updates.

*Rule: Never replace functional features with visual mockups or static stubs.*

---

## PHASE 8: QUALITY ASSURANCE & VERIFICATION GATES

Run all available automated and manual quality checks before declaring completion:

1. **Linting & Formatting:** Pass ESLint / Prettier without introduced warnings or errors.
2. **Type Safety:** Pass TypeScript compiler (`tsc --noEmit`) with zero type errors.
3. **Automated Testing:** Run and pass all existing unit, integration, and E2E test suites (Jest, Vitest, Cypress, Playwright).
4. **Production Build:** Execute `npm run build` (or equivalent package manager command) to confirm zero bundling errors or SSR/hydration failures.
5. **Runtime Cleanliness:** Inspect browser developer console to verify zero uncaught exceptions, 404 asset errors, or deprecation warnings.
6. **Cross-Browser & Visual Check:** Visually verify key pages across Chrome, Safari, and Firefox in both Light and Dark modes.

---

## SCOPE AND SAFETY RULES

- **Frontend Scope Only:** Do not modify unrelated backend services, database schemas, or cloud configurations.
- **No Orphaned Dependencies:** Do not delete packages from `package.json` without verifying they are completely unused across the project.
- **No Destructive Deletion:** Do not delete components without searching the entire codebase for dynamic or indirect imports.
- **No Hallucinated Copy:** Do not invent customer logos, fictional testimonials, vanity metrics, or fake product capabilities.
- **No Unjustified Rewrites:** Build upon and elevate existing components rather than rewriting from scratch, unless an existing component is fundamentally unmaintainable.
- **Truth in Verification:** Never claim testing or browser verification that was not physically executed.

---

## FINAL DELIVERABLES

1. **Frontend UI Audit Report:** Route-by-route audit with cataloged issues categorized by P0–P3 severity.
2. **Route & Component Inventory:** Comprehensive map of all pages, layouts, and reusable components.
3. **Design System Specification:** Documented token scales (typography, colors, spacing, borders, radius, shadows).
4. **Hardened Shared Component Library:** Accessible, production-ready, anti-slop primitives.
5. **Production Application Routes:** Fully implemented, high-craft views adhering to editorial standards.
6. **Responsive Verification Report:** Viewport validation across mobile, tablet, desktop, and ultra-wide.
7. **Accessibility Verification:** WCAG 2.1 AA audit with keyboard and focus validation.
8. **Build & Test Verification:** Proof of clean TypeScript compilation, lint passing, and successful production build.
9. **Changelog of Files:** Structured list of modified, created, and deleted files.
10. **Known Limitations & Follow-ups:** Any unverified edge cases or deferred tasks documented transparently.

---

## DEFINITION OF SUCCESS

The entire frontend feels like a cohesive, high-performance, editorial product built by senior software and design craftspeople.

- Every page has an intentional reason for its layout.
- Every component shares a unified visual and interactive vocabulary.
- Every viewport is ergonomic, functional, and visually balanced.
- Every interaction provides instant, predictable feedback.
- Every design decision serves usability, clarity, and product identity.

Do not merely modernize or patch the UI. Build a timeless, high-craft product experience.
