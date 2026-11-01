---
type: standard
read_when: Writing code in any stack. Read Shared Standards, that stack's section and the Final Checklist.
then: verification.md
---

# Languages & Frameworks Guide

## Role
Act as a senior full-stack engineer. Use this file as the coding standard for this repository. First find out which stack the project uses, then follow that stack's architecture, folder structure, and conventions. Check its "Do Not Forget" list and the Final Checklist before finishing any task. Work only on this codebase and local/staging environments. Never change production data or live systems.

**Two ways to use this file:**
- **Normal coding (the default):** use it as a standard. Read Shared Standards, your stack's section, and the Final Checklist. Skip Step 0 and Phases 1 to 6, and do not create `Language-Report.md`. `workflow.md` runs the task.
- **Stack review:** only when the owner asks for one, run the phases and write `Language-Report.md`.

**Existing projects win.** What a project already does outranks everything in this file. These standards apply to new projects, and to new code where the project has no pattern of its own. Never move a project to TypeScript, a new library or a new structure because this file says so. Checklist items for tools the project does not have are Not Applicable.

## Stacks I Work With Most
These are the stacks I use most often. **This is not a priority order.** A project can be in any language or framework, including ones not listed here.

| Stack | Usually Used For |
|---|---|
| **NestJS + TypeORM** | Backend APIs, admin systems, business logic, databases |
| **Next.js** | Websites, SEO pages, dashboards, full-stack frontend |
| **React.js** | SPAs, admin panels,  dashboards, widgets, full-stack frontend, frontend-only prototypes |
| **Node.js** | Scripts, small services, CLI tools, workers, webhooks |
| **Python** | Fast learning, quick experiments, data/AI scripts, automation |

**Which stack to use:**
1. **Existing project:** use the stack it already has, even if it is not listed here. Never move a project to one of these stacks just because I use them more.
2. **New project with a stack named in the brief:** use that stack.
3. **New project with no stack named:** choose what best fits the project, and confirm the choice with me before building. These usual fits are a starting point, not a rule:
   - Backend with database, auth, and roles → NestJS + TypeORM
   - Public website, or SEO matters → Next.js
   - Internal app with no SEO, frontend only → React.js (Vite)
   - Small script, cron job, webhook, or one-off tool → Node.js
   - Data, AI/ML, scraping, idea testing, or learning → Python

**If the project uses a stack not listed here:** apply the Shared Standards, then use that language's own conventions and standard tools for naming, structure, linting, formatting, and testing. Record what you used in the report.

## Step 0: Create the Report File (Stack Review Only)
Before doing anything else:
1. Check whether `Language-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it already exists, clear it and start fresh.
4. Add the date, project name, branch/commit, and a one-line summary of the task at the top.

Write the results of **every phase** into `Language-Report.md` as each phase is completed. Do not wait until the end.

## Phase 1: Identify the Stack
Explore the repository and determine:
- Language(s), framework(s), and versions
- Package manager and lockfile
- Database, ORM, and migration tool
- Lint, format, type-check, and test setup
- Build and run commands
- Folder structure and architecture pattern
- Existing conventions, README, or contribution notes

**Write to `Language-Report.md`:** a Project Overview section, a Stack table (Area | Found | Version | Evidence File), and which section of this guide applies. If none applies, say so and list the conventions and tools that will be used instead.

## Phase 2: Check the Standards
Compare the part of the project you are working on against the Shared Standards and the stack's section below (architecture, folder structure, conventions, and "Do Not Forget" list). If the project consistently does something differently, follow the project and record the difference. Do not change it unless asked.

**Write to `Language-Report.md`:** a Standards Check section with a table (Standard | Result | Notes), where Result is Pass / Fail / Needs Verification / Not Applicable, and a Differences From This Guide list.

## Phase 3: Plan the Work
Before changing code, list:
- Files to create or change
- New packages needed, and why the current stack cannot do the job
- Database, env variable, and API contract changes
- Tests to add or update
- Anything that needs my approval (framework, database, or major package changes)

**Write to `Language-Report.md`:** a Plan section with a table (ID | File | Change | Risk | Tests Needed).

## Phase 4: Do the Work
1. Follow the plan, the project's style, and the stack's section below.
2. Work in small steps, and run lint and type check after each one.
3. If the plan changes, update the Plan section instead of adding a duplicate.

**Write to `Language-Report.md`:** a Changes Made section with a table (ID | File(s) | What Changed | New Files Created | Tests Passed), packages added, and any changes skipped with the reason.

## Phase 5: Testing & Verification
1. Run lint, format check, type check, and tests.
2. Run the production build.
3. Check that the main flows you touched actually work.
4. Go through the Final Checklist at the end of this file.

**Write to `Language-Report.md`:** a Testing section with the result of each command, and the Final Checklist results (Item | Pass / Fail / Not Applicable).

## Phase 6: Final Summary
Complete `Language-Report.md` so it contains, in this order:

1. **Header** – project name, date, branch/commit, prepared by
2. **Executive Summary** – stack, what was done, status (Done / Done with issues / Blocked), top remaining issues
3. **Phase 1: Stack** – project overview, stack table, guide section applied
4. **Phase 2: Standards Check** – results table, differences from this guide
5. **Phase 3: Plan** – plan table
6. **Phase 4: Changes Made** – changes table, packages added, skipped changes
7. **Phase 5: Testing Results** – lint, types, tests, build, Final Checklist results
8. **Issues List** – each in this format:
   ```
   ### [PRIORITY] ID – Title
   - Location: file:line
   - Standard:
   - Problem:
   - Why it matters:
   - Recommended fix:
   - Status: Open / Fixed / Skipped
   ```
9. **Next Steps** – remaining work, Critical → Low, and items marked Needs Verification

Priority levels: **Critical, High, Medium, Low, Info.**

---

## Shared Standards (All Stacks)

### Code Quality
- TypeScript in all JS stacks with **strict mode on**. Avoid `any`.
- ESLint + Prettier for JS/TS. Ruff + Black for Python.
- Small functions, clear names, one job per file. No dead or commented-out code.
- Prefer simple, readable code over clever code.

### Naming
| Item | Style | Example |
|---|---|---|
| Files & folders (JS/TS) | kebab-case | `booking-status.enum.ts` |
| Classes, components, types | PascalCase | `BookingService`, `BookingCard` |
| Variables & functions | camelCase | `getBookings`, `isLoading` |
| Constants & env variables | UPPER_SNAKE_CASE | `MAX_PAGE_SIZE`, `DATABASE_URL` |
| Database tables & columns | snake_case | `booking_items`, `created_at` |
| Python files & functions | snake_case | `load_data.py`, `get_bookings` |
| React hooks | camelCase starting with `use` | `useBookings` |

### Environment & Secrets
- All config lives in `.env`. Commit only `.env.example` with keys and no values.
- Validate env variables when the app starts. Fail early if any are missing.
- Never hard-code keys, passwords, tokens, or production URLs.
- Use separate env files/values for development, staging, and production.

### Package Manager & Versions
- One package manager per project (`pnpm` preferred, or follow the existing lockfile). Never commit two lockfiles.
- Pin the Node version (`.nvmrc` + `engines` in `package.json`) and the Python version.

### Git
Agents work on the `njr` branch and follow `agent.md`. The branches below are how the repository itself is organised.
- Small commits with prefixes: `feat:`, `fix:`, `refactor:`, `chore:`, `docs:`, `test:`.
- Branches: `main` (production), `dev` (staging), `feature/...`, `fix/...`.
- `.gitignore` covers `node_modules`, `.env`, `dist`, `build`, `.next`, `.venv`, `__pycache__`, `.DS_Store`.

### Errors, Logging & Data
- Never swallow errors. Log useful context.
- Never log passwords, tokens, OTPs, or full card/ID numbers.
- Store dates in **UTC**. Convert only for display (`Asia/Kathmandu`, `Europe/London`).
- Store money as `decimal` or integer minor units (paisa/pence), never floating point.

### Standard API Contract (Backend ↔ Frontend)
- REST, versioned: `/api/v1/...`
- Plural resource names: `/bookings`, `/bookings/:id`
- Methods: `GET` read, `POST` create, `PATCH` partial update, `PUT` full replace, `DELETE` remove
- List responses return **data + meta** (page, limit, total)
- Single responses return **data**
- Error responses return **statusCode, message, and field errors**
- Status codes: 200, 201, 204, 400, 401, 403, 404, 409, 422, 429, 500

---

## NestJS + TypeORM

### What I Use
| Area | Tool |
|---|---|
| Framework | NestJS + Nest CLI |
| ORM | TypeORM (`@nestjs/typeorm`) |
| Database | PostgreSQL (default), MySQL if required |
| Config | `@nestjs/config` with schema validation (Joi) |
| Validation | `class-validator`, `class-transformer` |
| Auth | Passport + JWT, argon2 or bcrypt for hashing |
| API docs | Swagger (`@nestjs/swagger`) |
| Security | Helmet, Throttler (rate limit), CORS allowlist |
| Testing | Jest (unit), Supertest (e2e) |
| DB client | DBeaver on macOS |

### Architecture
**Modular, layered architecture.** Each feature is its own module.

| Layer | Job |
|---|---|
| **Controller** | Receives HTTP requests, applies guards, validates DTOs, calls the service. No business logic. |
| **Service** | All business logic, rules, ownership checks, and transactions. |
| **Repository / Entity** | Database access through TypeORM. Entities describe tables. |
| **DTO** | Shapes and validates input (create, update, query) and output (response DTOs). |
| **Common** | Shared guards, decorators, filters, interceptors, pipes, enums. |

**Request flow:** Request → Middleware → Guard (auth/roles) → Pipe (validation) → Controller → Service → Repository → Database → Interceptor (response shape) → Response. Errors go through the global exception filter.

### Folder Structure
```
project-root/
├── src/
│   ├── main.ts                  # app bootstrap, global pipes, helmet, CORS, prefix
│   ├── app.module.ts            # root module, imports all feature modules
│   ├── config/                  # env validation, database config, app config
│   ├── common/
│   │   ├── decorators/          # @Roles, @CurrentUser, @Public
│   │   ├── guards/              # JwtAuthGuard, RolesGuard
│   │   ├── filters/             # global exception filter
│   │   ├── interceptors/        # response transform, logging
│   │   ├── pipes/
│   │   ├── dto/                 # pagination DTO, shared DTOs
│   │   ├── enums/
│   │   └── utils/
│   ├── database/
│   │   ├── data-source.ts       # used by the TypeORM CLI for migrations
│   │   ├── migrations/
│   │   └── seeds/
│   └── modules/
│       ├── auth/
│       ├── users/
│       └── bookings/
│           ├── dto/             # create, update, query, response DTOs
│           ├── entities/        # booking.entity.ts
│           ├── bookings.controller.ts
│           ├── bookings.service.ts
│           ├── bookings.module.ts
│           └── bookings.service.spec.ts
├── test/                        # e2e tests
├── .env.example
├── nest-cli.json
├── tsconfig.json
└── package.json
```

### Conventions
- One module per feature. Modules export only what other modules need.
- Global prefix `api/v1`.
- Global ValidationPipe with whitelist, reject unknown fields, and transform enabled.
- Every input has a DTO. Update DTOs extend the create DTO as partial.
- Responses never return raw entities with sensitive fields. Hide them with exclude rules or response DTOs.
- Entities use UUID primary keys, `created_at` / `updated_at` columns, and soft delete where records must be kept.
- Status and role columns use enums.
- Migration scripts in `package.json`: generate, run, revert.

### Do Not Forget
- **`synchronize: false`** outside local development. Always use **migrations**, and review each generated migration before running it.
- Keep `data-source.ts` separate from the Nest module config.
- **Ownership checks** in services, so users can only reach their own records (prevents IDOR).
- **Guards** on every protected route. Mark public routes clearly.
- **Indexes** on foreign keys and filter/search columns. **Unique constraints** where duplicates are not allowed.
- **Transactions** for any multi-step write.
- **Avoid N+1 queries.** Load relations deliberately; don't make everything eager.
- **Always use query parameters** in QueryBuilder. Never build SQL with string concatenation.
- Set `onDelete` behaviour on relations.
- TypeORM returns `decimal` as a string. Convert carefully.
- **Pagination with a capped limit** (max 100).
- **Global exception filter** with clean errors and no stack traces in production.
- Hash passwords. Never select the password column by default.
- Rate-limit login, OTP, and password reset.
- Health check endpoint and graceful shutdown hooks.
- Swagger only in dev/staging, or protected in production.

---

## Next.js

### What I Use
| Area | Tool |
|---|---|
| Framework | Next.js (App Router) + TypeScript |
| Styling | Tailwind CSS |
| Components | shadcn/ui (Radix), inspiration from 21st.dev |
| Icons | lucide-react |
| Forms | react-hook-form + zod |
| Server data | Server Components with fetch caching |
| Client data | TanStack Query (React Query) with custom hooks |
| Client state | Zustand (only when needed) |
| Animation | Framer Motion (light use) |
| Images & fonts | `next/image`, `next/font` |
| SEO | Metadata API, sitemap, robots, JSON-LD |

### Architecture
**Server-first, feature-based architecture.**

| Layer | Job |
|---|---|
| **app/ (routes)** | Pages, layouts, loading/error states, route groups. Thin; mostly composes sections. |
| **Server Components** | Default. Fetch data on the server, render HTML, good for SEO and speed. |
| **Client Components** | Only for interactivity (state, effects, events, browser APIs). |
| **features/** | Feature logic: components, hooks, API functions, types, schemas. |
| **components/** | Shared UI (buttons, cards), layout (navbar, footer), page sections. |
| **lib/** | API client, query client, query keys, utilities, constants. |
| **Server Actions / Route Handlers** | Form submits and small backend tasks. Validate input and check auth inside them. |

**Data rule:** Server Components fetch directly on the server. Client components use **React Query custom hooks**. They never call fetch/axios directly.

### Folder Structure
```
project-root/
├── public/                      # static files, favicon, og images
├── src/
│   ├── app/
│   │   ├── (marketing)/         # public pages: home, about, services, contact
│   │   ├── (auth)/              # login, register
│   │   ├── (dashboard)/         # protected pages
│   │   ├── api/                 # route handlers
│   │   ├── layout.tsx           # root layout, fonts, providers
│   │   ├── page.tsx
│   │   ├── loading.tsx
│   │   ├── error.tsx
│   │   ├── not-found.tsx
│   │   ├── sitemap.ts
│   │   └── robots.ts
│   ├── components/
│   │   ├── ui/                  # shadcn base components
│   │   ├── layout/              # navbar, footer, sidebar
│   │   ├── sections/            # hero, features, pricing, faq, cta
│   │   └── common/              # shared small components
│   ├── features/
│   │   └── bookings/
│   │       ├── api/             # API functions
│   │       ├── hooks/           # React Query hooks
│   │       ├── components/
│   │       ├── schemas/         # zod schemas
│   │       └── types.ts
│   ├── hooks/                   # shared non-API hooks
│   ├── lib/                     # api client, query client, query keys, utils
│   ├── providers/               # QueryClientProvider, theme provider
│   ├── store/
│   ├── styles/
│   ├── types/
│   └── middleware.ts            # auth redirects
├── .env.example
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

### Conventions
- Route groups in brackets organise pages without changing URLs.
- `"use client"` only at the smallest component that needs it, never on whole pages without reason.
- Each important route has `loading`, `error`, and `not-found` handling.
- Page sections live in `components/sections`, so pages stay short and readable.
- Design tokens (colours, fonts, spacing) live in one place (Tailwind config / CSS variables).

### Do Not Forget
- **Server Components by default.**
- **No secrets in client code.** Only `NEXT_PUBLIC_` variables reach the browser.
- **Metadata on every page:** title, description, canonical URL, and Open Graph image.
- **sitemap.ts, robots.ts, and JSON-LD structured data** for SEO sites.
- **`next/image`** with proper sizes. Priority only on the hero image. Allow remote image domains in config.
- **`next/font`** to avoid layout shift.
- **Decide caching per route:** static, revalidate on a timer, or no-store.
- **Validate Server Action and Route Handler input** with zod, and check auth inside them.
- Middleware handles redirects, but **real permission checks happen on the server/backend**.
- **Avoid hydration errors:** no random values, current time, or `window` during server render.
- **React Query + custom hooks** for all client-side API calls, with central query keys and invalidation after mutations.
- **Performance targets:** LCP < 2.5s, CLS < 0.1, INP < 200ms.
- Run a production build before deploying.
- For VPS deploys: standalone output, PM2 or Docker, Nginx reverse proxy, correct `PORT`.

---

## React.js

### What I Use
| Area | Tool |
|---|---|
| Build tool | Vite + TypeScript |
| Routing | React Router |
| Styling | Tailwind CSS + shadcn/ui |
| **API / server state** | **TanStack Query (React Query) – required for all API calls** |
| HTTP client | Axios instance with interceptors |
| Client state | Zustand (Context for small apps) |
| Forms | react-hook-form + zod |
| Tables | TanStack Table |
| Charts | Recharts |
| Testing | Vitest + React Testing Library |
| Mocking | MSW or mock data inside API functions |

### Architecture
**Feature-based architecture with a strict API layer.**

| Layer | Job |
|---|---|
| **Pages** | One per route. Compose feature components. No API logic. |
| **Feature components** | UI for a feature. Use custom hooks only. |
| **Custom hooks (React Query)** | Wrap every API call: `useQuery` for reading, `useMutation` for create/update/delete. Handle cache invalidation. |
| **API functions** | Plain functions that call the backend through the axios instance. One file per feature. |
| **Axios instance** | Base URL, credentials, timeout, interceptors (auth, 401 handling, errors). |
| **Query keys** | All keys defined in one central file. |
| **Store** | Only true client state (UI, theme, filters). Never server data. |

**API flow:** Component → custom hook → React Query → API function → axios instance → backend.
Components **never** call axios/fetch directly and **never** fetch inside `useEffect`.

### Folder Structure
```
project-root/
├── public/
├── src/
│   ├── main.tsx                 # app entry, providers
│   ├── App.tsx
│   ├── routes/                  # route config, protected routes
│   ├── pages/                   # one page per route
│   ├── layouts/                 # main layout, dashboard layout, auth layout
│   ├── components/
│   │   ├── ui/                  # shadcn base components
│   │   └── common/              # shared components (loader, empty state, error state)
│   ├── features/
│   │   └── bookings/
│   │       ├── api/             # bookings API functions
│   │       ├── hooks/           # useBookings, useBooking, useCreateBooking ...
│   │       ├── components/
│   │       ├── schemas/         # zod schemas for forms
│   │       └── types.ts
│   ├── hooks/                   # shared hooks: useDebounce, useAuth, usePagination
│   ├── lib/
│   │   ├── axios.ts             # axios instance + interceptors
│   │   ├── query-client.ts      # QueryClient defaults
│   │   ├── query-keys.ts        # all query keys
│   │   └── utils.ts
│   ├── providers/               # QueryClientProvider, theme, auth
│   ├── store/                   # Zustand stores
│   ├── mocks/                   # mock data / MSW handlers for prototypes
│   ├── types/
│   └── styles/
├── .env.example
├── vite.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

### Conventions
- One custom hook per API action, named clearly (`useBookings`, `useBooking`, `useCreateBooking`, `useUpdateBooking`, `useDeleteBooking`).
- QueryClient defaults: sensible stale time, one retry, no refetch on window focus unless needed.
- React Query Devtools enabled in development.
- Path alias `@/` for imports from `src`.
- Shared loading, empty, and error components reused on every data screen.

### Do Not Forget
- **Every API call goes through React Query and a custom hook.** No exceptions.
- **Never copy server data into `useState`.** React Query is the source of truth.
- **Invalidate related queries after every mutation**, so lists refresh automatically.
- **Use `enabled`** for queries that depend on an ID or a filter value.
- Pagination uses keep-previous-data. Infinite scroll uses infinite queries.
- Optimistic updates only where they clearly improve UX, with rollback on error.
- **Disable submit buttons while a mutation is pending**, to prevent double submits.
- **Loading, empty, and error states** on every data screen.
- Follow the hook rules: call hooks only at the top level, and names start with `use`.
- **List keys** use stable IDs, not array index.
- Clean up effects (timers, listeners) and keep dependency arrays correct.
- Protected routes are for UX only. **Real permission checks happen in the backend.**
- Avoid storing tokens in localStorage. Prefer HttpOnly cookies.
- `VITE_` variables are public. **No secrets in the frontend.**
- Lazy-load routes in large apps.
- Memoize only when there is a real performance problem.
- Accessibility: labels, keyboard navigation, focus states, alt text.
- For prototypes, mock data lives inside API functions or MSW, so hooks and components don't change when the real API arrives.
- SPA on a server: Nginx must fall back to `index.html`.

---

## Node.js

### What I Use
| Area | Tool |
|---|---|
| Runtime | Node.js LTS |
| Language | TypeScript (`tsx` to run in dev, `tsc` to build) |
| Small APIs | Express or Fastify |
| Validation | zod |
| Env | dotenv or Node's built-in env file support, validated with zod |
| HTTP client | Native fetch with timeouts |
| Jobs & queues | node-cron, BullMQ + Redis |
| Logging | pino |
| Process manager | PM2 |
| Testing | Vitest or Jest |

### Architecture
**Layered service architecture** (for small APIs, workers, and webhooks).

| Layer | Job |
|---|---|
| **Routes** | Map URLs to controllers. |
| **Controllers** | Read the request, validate with zod, call the service, send the response. |
| **Services** | Business logic. No request/response objects here. |
| **Repositories / clients** | Database queries and external API calls. |
| **Middlewares** | Auth, error handler, request logging, rate limiting. |
| **Jobs / workers** | Background and scheduled tasks. |
| **Config** | Validated env and constants. |

For **scripts and CLI tools**, keep a simple structure: entry file, `lib` helpers, config, and output folder.

### Folder Structure
```
project-root/
├── src/
│   ├── index.ts                 # entry: start server or worker
│   ├── app.ts                   # app setup, middlewares, routes
│   ├── config/                  # env validation, constants
│   ├── routes/
│   ├── controllers/
│   ├── services/
│   ├── repositories/            # db queries
│   ├── clients/                 # external API clients
│   ├── middlewares/             # auth, error handler, logger, rate limit
│   ├── jobs/                    # cron jobs, queue workers
│   ├── schemas/                 # zod schemas
│   ├── utils/
│   └── types/
├── scripts/                     # one-off scripts
├── tests/
├── .env.example
├── .nvmrc
├── ecosystem.config.js          # PM2 config
├── tsconfig.json
└── package.json
```

### Conventions
- Choose ES Modules or CommonJS once per project and stay consistent.
- Use `async/await`, not callback chains.
- One central error handler middleware.
- Structured JSON logs (pino) with a request ID.

### Do Not Forget
- **Use LTS Node** and pin the version.
- **Always await promises** and handle errors.
- Catch errors per request, so one bad request cannot end the process. For **unhandled rejections and uncaught exceptions** outside a request, log them and exit cleanly.
- **Graceful shutdown** on SIGTERM/SIGINT: close the server, DB, and queues.
- **Timeouts on all external HTTP calls.**
- **Don't block the event loop.** No heavy sync work or sync file reads in request handlers.
- **Stream large files** instead of loading them fully into memory.
- Build file paths safely, and never trust user input in paths.
- **Webhooks:** verify signatures, respond fast, process in the background, and make processing idempotent.
- Validate every request body, query, and param with zod.
- Run dependency audits regularly.
- **PM2:** ecosystem file, save the process list, and enable startup on VPS reboot.

---

## Python

### What I Use
| Area | Tool |
|---|---|
| Version | Python 3.11+ |
| Environment | `venv` or `uv` |
| Dependencies | `requirements.txt` or `pyproject.toml` |
| APIs | FastAPI + Uvicorn |
| Validation & models | Pydantic |
| Data | pandas, numpy |
| HTTP | httpx or requests |
| AI / LLM | Official SDKs (Anthropic, OpenAI); frameworks only if needed |
| Scraping | BeautifulSoup, Playwright |
| Notebooks | Jupyter (inside VS Code) |
| Lint & format | Ruff, Black |
| Testing | pytest |

### Architecture
Two modes, depending on the goal:

**A. Learning / experiments:** a simple, flat structure. One concept per file or notebook, with short notes on what was learned.

**B. Small app or API (FastAPI):** a layered structure.

| Layer | Job |
|---|---|
| **Routers** | API endpoints, grouped by feature. |
| **Schemas** | Pydantic models for request/response validation. |
| **Services** | Business logic. |
| **Models / DB** | Database models and session handling. |
| **Core** | Config, settings, security, logging. |

### Folder Structure

**Learning / experiments**
```
python-learning/
├── .venv/
├── basics/                      # variables, loops, functions, classes
├── data/                        # pandas, csv, json practice
├── api/                         # requests/httpx practice
├── ai/                          # LLM SDK experiments
├── notebooks/
├── notes.md                     # what I learned, simple explanations
├── requirements.txt
└── .gitignore
```

**Small app / FastAPI**
```
project-root/
├── app/
│   ├── main.py                  # FastAPI app, routers included
│   ├── core/                    # config, settings, security, logging
│   ├── routers/                 # bookings.py, users.py
│   ├── schemas/                 # Pydantic models
│   ├── services/
│   ├── models/                  # DB models
│   ├── db/                      # session, base, migrations (Alembic)
│   └── utils/
├── scripts/
├── tests/
├── .env.example
├── requirements.txt / pyproject.toml
└── README.md
```

### Conventions
- Follow PEP 8 with snake_case functions and PascalCase classes.
- Type hints on all functions.
- Settings loaded from env through Pydantic settings.
- Runnable scripts use a main entry guard.
- Use `pathlib` for file paths.

### macOS Setup Reminder
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Do Not Forget
- **Always use a virtual environment.** Never install packages into the macOS system Python.
- Activate the environment before running anything. Keep dependencies saved and updated.
- Add `.venv`, `.env`, and `__pycache__` to `.gitignore`.
- **Read and write files with UTF-8 encoding** (important for Nepali/Devanagari text).
- **Never build SQL with f-strings.** Use parameters.
- **Timeouts on network requests.**
- Keep experiments separate from real project code.
- When learning, explain each new concept simply with a small working example and a note in `notes.md`.
- Use Alembic for database migrations in real apps.

---

## Final Checklist (Before Finishing Any Task)
- [ ] The project's stack followed (or a new project's stack confirmed)
- [ ] Folder structure and naming follow the project, then this guide
- [ ] Strict typing used where the language supports it (TypeScript strict, Python type hints)
- [ ] All inputs validated (DTO / zod / Pydantic, or the stack's equivalent)
- [ ] Auth and permission checks done on the server
- [ ] No secrets in code or frontend bundles; `.env.example` updated
- [ ] Errors handled cleanly; no stack traces leaked
- [ ] Frontend API calls use React Query custom hooks (React and Next.js projects)
- [ ] Loading, empty, and error states in the UI
- [ ] Database changes done through migrations
- [ ] Lint, format, type check, and tests pass
- [ ] Production build works
- [ ] README / setup notes updated if anything changed
- [ ] `Language-Report.md` complete, with every phase recorded (stack review only)

## Rules
- In a stack review, create `Language-Report.md` first, before any other step.
- In a stack review, update `Language-Report.md` after each phase; every phase must have its results recorded.
- The listed stacks are the ones I use most, not a priority order. A project can be in any language.
- Match the existing project's structure, naming, and style before applying this guide.
- Ask before changing the framework, database, or major packages.
- Don't add a new package if the current stack already solves the problem.
- Keep code simple, readable, and consistent.
- Explain things in simple language, with steps for macOS and DBeaver where relevant.
- Do not invent results. Mark anything unconfirmed as **Needs Verification**.
- Never touch production data, real credentials, or live systems without approval.
