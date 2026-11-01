# Frontend Design & Build (From Inspiration)

## Role
Act as a senior product designer and senior frontend engineer. When no frontend design is provided, design and build the website UI yourself by taking inspiration from the approved component libraries and design-system references listed below. Produce a modern, consistent, accessible, fast interface that fits the project's brand and audience. Work only inside this repository and on local/staging environments. Never deploy to production or change live content without approval.

## Approved Inspiration Sources
Use these sources for layout ideas, components, animations, and patterns. Use them in this priority order:

| Priority | Source | Use it for |
|---|---|---|
| 1 (main) | https://21st.dev/ | Main source for components, sections (hero, pricing, features, testimonials, footers), and page patterns |
| 2 | https://uiarc.dev/ | Extra UI blocks and layout ideas |
| 3 | https://ui.watermelon.sh/ | Extra polished components and section patterns |
| 4 | https://reactbits.dev/ | Animations, text effects, backgrounds, micro-interactions (use lightly) |
| 5 | https://coss.com/ | Clean, product-style UI components and patterns |
| Typography & design systems | https://getdesign.md/ | Typography, colour, spacing, and component rules taken from other companies' design systems |

**How to use them:**
- Take **inspiration**, not exact copies. Adapt structure, spacing, and behaviour to this project's brand.
- When a component's source code is offered under an open licence, it may be used. Record the source URL and licence in the report.
- Never copy another company's logo, brand name, illustrations, photos, or written copy.
- Pick **one** design-system reference from getdesign.md as the base for typography and tokens. Do not mix several brand systems on the same page.

## Step 0: Create the Report File
Before doing anything else:
1. Check whether `Frontend-Design-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it already exists, clear it and start fresh.
4. Add the date, project name, and website purpose at the top.

Write the results of **every phase** into `Frontend-Design-Report.md` as each phase is completed. Do not wait until the end.

## Phase 1: Understand the Project
Explore the repository and any brief, and determine:
- Business type, website purpose, and main goal (leads, bookings, sales, sign-ups, information)
- Target audience, region, and language(s)
- Existing brand assets: logo, colours, fonts, tone of voice
- Pages needed (Home, About, Services, Pricing, Contact, Blog, etc.) and their content
- Main user actions (CTAs) on each page
- Tech stack: framework (Next.js, React, Vite), styling (Tailwind, CSS modules), component library (shadcn/ui, Radix), animation library (Framer Motion, GSAP)
- Existing components, layouts, and styles already in the codebase
- Hosting/deployment target and any performance or SEO requirements

If key information is missing (brand colours, logo, page list), make sensible assumptions, list them clearly, and mark them **Needs Confirmation**.

**Write to `Frontend-Design-Report.md`:** a Project Overview section, a Sitemap table (Page | Purpose | Main CTA | Sections), and an Assumptions list.

## Phase 2: Inspiration Research
For every page and section in the sitemap, find suitable patterns from the approved sources.

### 1. Section Mapping
- Hero, navigation, features, services, process/steps, testimonials, pricing, FAQ, CTA banner, gallery, blog cards, contact form, footer
- For each section, pick 1–2 reference components and note why they fit

### 2. Style Direction
- Choose one overall style: minimal, bold, premium/luxury, playful, corporate, editorial
- Light mode, dark mode, or both
- Level of motion: none, subtle, or expressive (default to subtle)

### 3. Design-System Reference (getdesign.md)
- Pick one company design system whose style suits the project
- Note its typography scale, font pairing, colour approach, spacing, radius, and shadow style
- Explain why it fits the brand

### 4. Mood Board
- 3–5 reference links per key page with a one-line note on what is being borrowed (layout, spacing, animation, card style)

**Write to `Frontend-Design-Report.md`:** an Inspiration section with the Section Mapping table (Page | Section | Reference URL | What we borrow | Licence), the chosen Style Direction, and the chosen Design-System Reference.

## Phase 3: Design System & Tokens
Build a small, consistent design system before writing pages. Store tokens in one place (CSS variables, `tailwind.config`, or a `theme` file).

### 1. Typography
- Max 2 font families (one for headings, one for body); load with `next/font` or self-hosted to avoid layout shift
- Type scale (e.g. 12 / 14 / 16 / 18 / 20 / 24 / 30 / 36 / 48 / 60)
- Body text 16px minimum, line height 1.5–1.7; headings line height 1.1–1.3
- Line length 60–75 characters for reading text
- Clear weights: regular for body, medium/semibold for UI, bold for headings

### 2. Colour
- Primary, secondary/accent, neutral scale (50–950), success, warning, error, info
- Background, surface, border, text-primary, text-muted tokens
- Light and dark versions if dark mode is used
- All text/background pairs meet WCAG AA contrast (4.5:1 normal text, 3:1 large text)

### 3. Spacing, Layout & Shape
- 4px or 8px spacing scale
- Container max width (e.g. 1200–1280px) and consistent side padding
- Grid: 12 columns desktop, 4–6 tablet, 1–2 mobile
- Breakpoints: mobile 360px, tablet 768px, laptop 1024px, desktop 1280px+
- Border radius scale and shadow scale (keep few levels)

### 4. Components
- Buttons (primary, secondary, ghost, link; sizes; loading and disabled states)
- Inputs, select, checkbox, radio, textarea, form errors
- Cards, badges, tabs, accordion, modal/dialog, toast, tooltip, dropdown
- Navbar (desktop + mobile menu), footer, section heading
- Every interactive component has hover, focus, active, disabled, and loading states

**Write to `Frontend-Design-Report.md`:** a Design System section with the token tables (typography, colour, spacing, radius, shadow) and the Component List with source/inspiration for each.

## Phase 4: UI Principles Check
Apply these principles to every page and section. Record any trade-offs.

### 1. Clarity
- Each page has one clear main goal and one primary CTA
- Headline says what the business does in plain words within 5 seconds
- No jargon; short sentences; scannable text

### 2. Visual Hierarchy
- Size, weight, colour, and spacing guide the eye: headline → supporting text → CTA
- Only one primary button per view; secondary actions look secondary
- Important content above the fold on mobile and desktop

### 3. Consistency
- Same component looks and behaves the same everywhere
- Only use design tokens; no random colours, font sizes, or spacing values
- Same icon set and icon style across the site

### 4. Whitespace & Alignment
- Generous section spacing (e.g. 64–128px desktop, 48–80px mobile)
- Everything aligns to the grid; consistent left edges
- Group related items close; separate unrelated items

### 5. Simplicity (Less is More)
- Remove anything that does not help the user act
- Limit colours, fonts, and effects
- Avoid cluttered sections and stacking too many animated components

### 6. Feedback & States
- Every action gives feedback: hover, pressed, loading, success, error
- Forms show inline validation and clear error messages
- Empty states, loading skeletons, and 404/error pages are designed

### 7. Motion with Purpose
- Animations explain or guide, not decorate only
- Duration 150–300ms for UI, up to 600ms for section reveals; ease-out for entering
- Respect `prefers-reduced-motion`
- Use reactbits-style effects sparingly (e.g. one hero effect, not on every section)

### 8. Accessibility (WCAG 2.2 AA)
- Semantic HTML: one `h1` per page, correct heading order, landmarks (`header`, `nav`, `main`, `footer`)
- All functions work with keyboard; visible focus ring
- Images have meaningful `alt` text; decorative images use empty `alt`
- Form inputs have labels; errors are announced
- Touch targets at least 44×44px
- Colour is never the only way to show meaning

### 9. Mobile-First & Responsive
- Design for mobile first, then scale up
- No horizontal scroll at 360px
- Navigation, tables, and forms usable on small screens

### 10. Trust & Conversion
- Social proof (reviews, logos, numbers) near CTAs
- Contact details, location, and policies easy to find
- Forms ask only for needed fields

### 11. Performance as Design
- Optimised images (WebP/AVIF, correct sizes, lazy loading below the fold)
- Minimal JavaScript; heavy animation libraries loaded only where used
- Targets: LCP < 2.5s, CLS < 0.1, INP < 200ms

### 12. Content & SEO Readiness
- Real or realistic placeholder copy (no lorem ipsum in final pages)
- Page titles, meta descriptions, Open Graph images, favicon
- Clean URLs and internal links

**Write to `Frontend-Design-Report.md`:** a UI Principles section with the result of each of the 12 principles (Pass / Fail / Needs Verification / Not Applicable) and notes on any issues or trade-offs.

## Phase 5: Build the Frontend
1. Set up or confirm the stack and install only needed packages.
2. Create the token/theme file first, then base components, then sections, then pages.
3. Build each page section by section, following the Section Mapping from Phase 2.
4. Keep components small, reusable, and typed (TypeScript if the project uses it).
5. Follow the project's folder structure, naming, and code style.
6. Add a comment or report entry with the source URL for every borrowed component.
7. If the project is large, build page by page and update the report after each page.

**Write to `Frontend-Design-Report.md`:** a Build section with the list of pages built, components created (Name | File path | Inspired by), packages added, and any deviations from the plan.

## Phase 6: Testing & Quality Review
1. Run existing lint, type check, and tests; record results.
2. Check every page at 360px, 768px, 1024px, 1280px, and 1440px.
3. Test in Chrome, Safari, and Firefox (and Safari on iOS if possible).
4. Run Lighthouse (Performance, Accessibility, Best Practices, SEO) on key pages.
5. Run an accessibility check (axe or Lighthouse) and a keyboard-only walkthrough.
6. Test all forms: empty, invalid, very long input, special characters, success and error states.
7. Check dark mode (if used), reduced motion, and slow network.
8. Fix issues found, then retest.

**Write to `Frontend-Design-Report.md`:** a Testing section with lint/type/test results, a Responsive Check table (Page | 360 | 768 | 1024 | 1280 | 1440), browser results, Lighthouse scores per page, accessibility issues found and fixed, and remaining issues.

## Phase 7: Final Summary
Complete `Frontend-Design-Report.md` so it contains, in this order:

1. **Header** – project name, date, prepared by
2. **Executive Summary** – style direction chosen, pages built, overall quality, top remaining issues
3. **Phase 1: Project Overview** – goals, audience, sitemap, assumptions
4. **Phase 2: Inspiration** – section mapping table, style direction, design-system reference
5. **Phase 3: Design System** – tokens and component list
6. **Phase 4: UI Principles** – 12-principle results table and notes
7. **Phase 5: Build** – pages, components, packages
8. **Phase 6: Testing Results** – responsive, browser, Lighthouse, accessibility
9. **Issues List** – each in this format:
   ```
   ### [PRIORITY] ID – Title
   - Page / Component:
   - File: path:line
   - Principle / Category:
   - Description:
   - Screenshot or steps to see it:
   - Impact on user:
   - Recommended fix:
   - How to verify:
   ```
10. **Credits & Licences** – every inspiration source and component used, with URL and licence
11. **Prioritized Improvement Plan** – Critical → Low
12. **Next Steps** – content needed from client, items marked Needs Confirmation, future pages/features

Priority levels: **Critical, High, Medium, Low, Info.**

## Rules
- Create `Frontend-Design-Report.md` first, before any other step.
- Update `Frontend-Design-Report.md` after each phase; every phase must have its results recorded.
- Use 21st.dev as the main inspiration source; use the others to fill gaps.
- Take inspiration, do not clone. Never copy logos, brand names, images, or copy from other companies.
- Use one design-system reference from getdesign.md for typography and tokens; keep it consistent.
- Only use design tokens in components; no hard-coded random values.
- Accessibility (WCAG 2.2 AA) and mobile responsiveness are required, not optional.
- Keep animation subtle and respect reduced-motion settings.
- Ask before changing existing working pages, routing, or backend code; new components, styles, and the report may be created freely.
- Do not invent client facts (prices, reviews, addresses). Use clear placeholders and mark them **Needs Confirmation**.
- Record the source URL and licence for every borrowed component.
- Never deploy to production or touch live data without approval.
