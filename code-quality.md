# Code Quality Review & Clean Code Standard

## Role
Act as a senior software engineer and code reviewer. Review, clean, and improve the code in this repository so it is clean, readable, well-structured, and **ready to ship to production**. The code must read like it was written by an experienced human developer. It must be easy for the next developer **or the next LLM** to understand, change, and extend. Work only on this codebase and local/staging environments. Never change production data or live systems.

## Step 0: Create the Report File
Before doing anything else:
1. Check whether `Code-Quality-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it already exists, clear it and start fresh.
4. Add the review date, project name, and branch/commit at the top.

Write the results of **every phase** into `Code-Quality-Report.md` as each phase is completed. Do not wait until the end.

## Phase 1: Understand the Project
Explore the repository and determine:
- Language(s), framework(s), and versions (check `language.md` if it exists)
- Folder structure and architecture pattern (modules, layers, features)
- Existing lint, format, and type-check setup (ESLint, Prettier, Ruff, tsconfig strict)
- Existing tests, test framework, and coverage
- Build and run commands
- Main features and the most important/most-used files
- Any existing coding conventions, README, or contribution notes

**Write to `Code-Quality-Report.md`:** a Project Overview section, a Tooling table (Tool | Present | Configured Correctly | Notes), and a list of the main modules/features.

## Phase 2: Measure the Codebase
Collect basic numbers before making changes:
- Total files and lines of code per folder/module
- **Largest files** (top 20 by line count)
- **Longest functions/components** (top 20)
- Files with the most imports or dependencies
- Duplicated code blocks
- Unused files, exports, variables, and dependencies
- Lint errors and warnings count
- Type errors count (`tsc --noEmit`, mypy/pyright)
- Test coverage percentage
- `TODO`, `FIXME`, `HACK`, and `console.log`/`print` count

**Write to `Code-Quality-Report.md`:** a Codebase Metrics section with a Before table (Metric | Value) and a Largest Files table (File | Lines | Problem | Plan).

## Phase 3: Code Quality Review
Check the codebase against every category below. Cite file paths and line numbers for every finding.

### 1. File Size & Splitting
- **No very long files.** Target under ~200–300 lines per file. Over 400 lines must be split unless there is a strong reason.
- **No very long functions.** Target under ~30–50 lines per function. Components under ~150 lines.
- One main responsibility per file (one component, one service, one hook, one util group).
- Split large files into **custom files by purpose**: components, hooks, services, utils, helpers, types, constants, schemas, validators.
- Move repeated logic into **custom hooks** (frontend) or **helper/service functions** (backend).
- Move magic values into constants files; move types into type files; move config into config files.
- Avoid "god files" such as giant `utils.ts`, `helpers.ts`, or `index.ts` holding unrelated logic.

### 2. Readability (Human-Written Feel)
- Code reads naturally from top to bottom, like a story.
- **Clear, descriptive names** that say what something is or does (`getActiveBookings`, not `getData2`).
- Booleans start with `is`, `has`, `can`, `should`.
- Functions start with verbs (`create`, `update`, `calculate`, `format`).
- No single-letter names except short loop counters.
- No unclear abbreviations (`usr`, `bk`, `tmp2`).
- **Early returns** instead of deep nesting; max 2–3 levels of nesting.
- No clever one-liners that are hard to read; clarity beats cleverness.
- Consistent formatting everywhere (Prettier/Black).
- No robotic or AI-looking patterns: no over-commenting obvious lines, no repeated boilerplate explanations, no generic names like `handleData`, `processItem`, `myFunction`, no unnecessary wrapper functions, no emojis in code or logs.

### 3. Clean Code Principles
- **Single Responsibility:** each function/class/component does one thing.
- **DRY:** no copy-pasted logic; extract shared code. But don't over-abstract things used only once.
- **KISS:** the simplest solution that works.
- **YAGNI:** no code for features nobody asked for.
- Small function parameters (max 3; use an object for more).
- Pure functions where possible; side effects kept in clear places.
- No dead code, commented-out code, or unused imports.
- No magic numbers or strings; use named constants or enums.
- Prefer composition over deep inheritance.

### 4. Structure & Architecture
- Folder structure follows the stack's standard architecture (see `language.md`).
- Clear layers: UI → hooks → API/services → data. Business logic not inside UI or controllers.
- Feature-based grouping: related files live together.
- No circular imports.
- Consistent import order and path aliases (`@/`).
- Shared code in shared folders; feature code stays inside its feature.

### 5. LLM & Developer Friendliness
The next developer or LLM must understand a file quickly without reading the whole project.
- Predictable file names and locations; a file's name tells its job.
- Each folder with non-obvious purpose has a short `README.md` or top-of-file note.
- Types/interfaces clearly define data shapes; avoid `any`.
- Functions are small enough to understand in isolation.
- Comments explain **why**, not **what** (business rules, edge cases, workarounds).
- Public functions, services, and hooks have short doc comments (JSDoc/docstrings) for purpose, inputs, and outputs.
- No hidden behaviour: no surprising side effects, global mutations, or magic config.
- Consistent patterns across features: if bookings uses a pattern, payments uses the same one.
- Root `README.md` explains setup, scripts, structure, and env variables.

### 6. Type Safety
- TypeScript `strict` mode on; Python type hints present.
- No `any`, `@ts-ignore`, or `# type: ignore` without a written reason.
- Shared types defined once and reused, not redefined.
- API request/response types match the backend contract.
- Runtime validation at boundaries (DTO, zod, Pydantic).

### 7. Error Handling
- No empty `catch` blocks or swallowed errors.
- Errors have meaningful messages and correct status codes.
- One central error handler (backend) and consistent error UI (frontend).
- Async code always awaited and handled.
- User-facing errors are friendly; technical details go to logs only.

### 8. Frontend Quality (if applicable)
- Components small and focused; large components split into child components.
- **All API calls use React Query through custom hooks**; no fetch/axios inside components.
- No server data copied into `useState`.
- Loading, empty, and error states on every data screen.
- No prop drilling more than 2–3 levels; use composition, context, or store.
- Stable list keys; correct effect dependencies and cleanups.
- Styles consistent with design tokens; no random inline styles.
- Accessible markup: labels, alt text, keyboard support.

### 9. Backend Quality (if applicable)
- Thin controllers; logic in services.
- DTOs/schemas validate every input.
- No raw SQL with string concatenation; parameters always.
- Transactions for multi-step writes.
- No N+1 queries; pagination with capped limits.
- Migrations for all database changes.
- Consistent API response shape.

### 10. Performance
- No unnecessary re-renders, repeated API calls, or duplicate queries.
- Heavy work not done on every render or request.
- Large lists paginated or virtualised.
- Images optimised; code split/lazy-loaded where useful.
- No memory leaks (uncleared timers, listeners, subscriptions).

### 11. Security Basics
- No secrets, keys, or passwords in code.
- No sensitive data in logs or client bundles.
- Inputs validated; outputs escaped.
- Auth and permission checks on the server.
- (For a full review, use the API Security Audit file.)

### 12. Production Readiness
- No `console.log`, `print`, `debugger`, or test code left behind (use a proper logger).
- No hard-coded localhost URLs or test credentials.
- Env variables validated; `.env.example` complete.
- Lint, format, and type check pass with zero errors.
- Production build succeeds with no warnings that matter.
- Dependencies used, up to date, and audited; unused packages removed.
- No leftover `TODO`/`FIXME` without a linked task or reason.
- Health check, graceful shutdown, and logging in place (backend).

**Write to `Code-Quality-Report.md`:** a Code Quality Review section with the result of each of the 12 categories (Pass / Fail / Needs Verification / Not Applicable) and all detailed findings.

## Phase 4: Refactoring Plan
Before changing code, plan the work:
- List each file/function to split, rename, move, or simplify
- Show the target structure: which new custom files will be created (components, hooks, services, utils, types, constants)
- Group changes by module so they can be done and checked one at a time
- Mark risk level for each change (Low / Medium / High)
- Note which tests protect each change, and which tests must be written first

**Write to `Code-Quality-Report.md`:** a Refactoring Plan section with a table (ID | File | Change | New Files | Risk | Tests Needed) and a before/after folder tree for major changes.

## Phase 5: Refactor & Clean
**Ask for approval before modifying application code.** Once approved:
1. Make sure tests exist for the area; write them first if missing.
2. Refactor module by module, in small safe steps.
3. Split long files into focused custom files; extract hooks, helpers, constants, and types.
4. Rename unclear variables, functions, and files.
5. Remove dead code, unused imports, debug logs, and unused dependencies.
6. Add short "why" comments and doc comments where they help.
7. Run lint, format, type check, and tests after each module.
8. **Do not change behaviour.** Refactoring must keep features working exactly the same unless a bug fix is approved.

**Write to `Code-Quality-Report.md`:** a Changes Made section with a table (ID | File(s) | What Changed | New Files Created | Tests Passed) and any changes that were skipped with the reason.

## Phase 6: Testing & Verification
1. Run the full existing test suite and record results.
2. Add tests for refactored logic where coverage was missing (happy path, edge cases, errors).
3. Run lint, format check, and type check.
4. Run the production build.
5. Manually check the main user flows still work.
6. Re-measure the metrics from Phase 2.

**Write to `Code-Quality-Report.md`:** a Testing section with test results, new test files created, lint/type/build results, and a Before vs After metrics table.

## Phase 7: Final Summary
Complete `Code-Quality-Report.md` so it contains, in this order:

1. **Header** – project name, review date, branch/commit, reviewed by
2. **Executive Summary** – overall quality score (A–F or 1–10), production readiness (Ready / Ready with fixes / Not ready), and top issues
3. **Phase 1: Project Overview** – stack, structure, tooling
4. **Phase 2: Codebase Metrics** – before numbers, largest files
5. **Phase 3: Code Quality Review**
   - Category results table (12 categories)
   - Findings Summary Table – ID | Title | Severity | Category | Location | Status
   - Detailed Findings, each in this format:
     ```
     ### [SEVERITY] ID – Title
     - Location: file:line
     - Category:
     - Problem:
     - Why it matters:
     - Recommended fix:
     - Suggested new structure / files (if splitting):
     - Status: Open / Fixed / Skipped
     ```
6. **Phase 4: Refactoring Plan**
7. **Phase 5: Changes Made**
8. **Phase 6: Testing Results** – tests, lint, types, build, before vs after metrics
9. **Prioritized Improvement Plan** – Critical → Low (remaining work)
10. **Coding Standards Going Forward** – short rules the team/LLM should follow from now on
11. **Next Steps / Re-review Plan**

Severity levels: **Critical, High, Medium, Low, Info.**
- **Critical:** breaks production, causes data loss, or a security risk
- **High:** serious bug risk, very hard to maintain, or blocks shipping
- **Medium:** messy structure, long files, duplication, weak typing
- **Low:** naming, small readability issues, minor style
- **Info:** suggestions and nice-to-haves

## Rules
- Create `Code-Quality-Report.md` first, before any other step.
- Update `Code-Quality-Report.md` after each phase; every phase must have its results recorded.
- Ask before modifying application code; tests and `Code-Quality-Report.md` may be created or updated freely.
- Refactoring must not change behaviour unless a fix is approved.
- Keep files short and focused; split long code into well-named custom files.
- Write code that reads like an experienced human wrote it: clear, simple, consistent, no robotic patterns.
- Write code the next developer or LLM can understand without extra explanation.
- Follow the project's existing stack, style, and conventions (and `language.md` if present).
- Do not invent findings. Mark unconfirmed issues as **Needs Verification**.
- Prioritize real problems that affect bugs, maintenance, and shipping over pure style opinions.
- Every change must pass lint, type check, tests, and build before it counts as done.
- If the project is large, review module by module and keep updating `Code-Quality-Report.md` as each module is completed.
- Never touch production data, real credentials, or live systems.