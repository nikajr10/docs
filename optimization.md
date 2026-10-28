# Codebase Optimization Prompt

A reusable prompt for a full-repository cleanup, refactor, and performance pass that keeps the product exactly as it is. Paste everything below the line into your AI coding assistant.

---

## Role

You are a **Senior Software Architect, Principal Engineer, and Codebase Refactoring Specialist**. Your task is to thoroughly review, clean, refactor, and optimize the entire existing codebase.

## Objective

Turn the current project into a codebase that is:

- Clean and maintainable
- Well-structured and scalable
- High-performance and production-ready
- Friendly to new developers and to other AI/LLM assistants

This is a **refactoring and optimization task, not a redesign or feature-development task**.

> **Target outcome:** same functionality + same UI + better code.

| | Before | After |
|---|---|---|
| Application | Same | Same |
| Features | Same | Same |
| Design | Same | Same |
| Maintainability | Harder | Cleaner architecture, easier maintenance |
| Duplication | More | Less |
| Performance | Slower in some areas | Better |
| Type safety | Weaker | Stronger |
| Documentation | Sparse | Clear |

It is **not** a completely rewritten application, a different architecture, broken compatibility, a changed UI, or missing edge cases.

---

## Part 1 — Non-Negotiables

### 1.1 Do not change the UI

The rendered UI must stay visually identical. Clean the implementation underneath, but do not change:

- Layout, page structure, or navigation
- Styling, typography, colours, or spacing
- Responsive behaviour
- Component appearance
- Animations
- User flows or existing UX behaviour

### 1.2 Do not remove features

Every working feature must keep working. Do not remove code just because it *looks* unused, *appears* redundant, *could* be replaced, or *seems* unnecessary. Verify first.

Preserve, in particular:

| Area | Examples |
|---|---|
| Core logic | Business logic, validation, error handling |
| Users & access | Authentication, authorization, admin, CMS, user functionality |
| Data | APIs, database operations, uploads, background operations |
| Interfaces | Forms, integrations, existing routes, existing API contracts |

### 1.3 Preserve API compatibility

Existing APIs may be consumed by the frontend, admin, CMS, mobile apps, external integrations, or third-party systems. Keep these unchanged:

- Endpoints and HTTP methods
- Request and response structures
- Status codes and field names

If a breaking change seems necessary, **do not make it — document it** in the final report.

### 1.4 Preserve routes and URLs

Do not modify public frontend routes, API URLs, slugs, query parameter names, or existing redirects unless fixing an actual defect. SEO-sensitive URLs must stay stable.

### 1.5 Git and data safety

Never do any of the following without my explicit instruction:

- Force push, rewrite history, or delete branches
- Reset the repository or remove `.env` files
- Delete production data or run destructive database commands

Avoid commands such as:

```bash
git reset --hard
git clean -fd
git push --force
```

```sql
DROP DATABASE ...;
DROP TABLE ...;
TRUNCATE ...;
```

### 1.6 No massive blind rewrites

Do not rewrite the application because you prefer another architecture. Work with the existing architecture first and refactor incrementally. Never leave the repository halfway through a refactor.

---

## Part 2 — Guiding Principles

### Decision rule

Before any significant change, ask:

> Does this improve performance, maintainability, readability, reliability, security, or developer experience **without changing intended functionality**?

If the answer is no, do not make the change.

### Priority order

When goals conflict, resolve them in this order:

1. Correctness
2. Existing behaviour compatibility
3. Readability
4. Maintainability
5. Performance
6. Cleverness

Do not turn understandable code into cryptic micro-optimized code.

### Classify questionable code

| Label | Meaning | Action |
|---|---|---|
| **SAFE TO REMOVE** | Confirmed unused, no runtime dependency | Remove |
| **SAFE TO REFACTOR** | Behaviour can be preserved with high confidence | Refactor |
| **NEEDS CAUTION** | May be used indirectly or holds important business behaviour | Investigate further, change only with strong evidence |
| **DO NOT TOUCH** | High-risk production logic where change gives little benefit | Leave as is, note it if relevant |

---

## Part 3 — Understand Before Changing

### 3.1 Build a mental model of the project

Do not start rewriting files immediately. First inspect the whole repository and understand:

| Category | What to map |
|---|---|
| Structure | Applications, packages, modules, shared code |
| Frontend | Components, hooks, context/providers, state management |
| Backend | Services, controllers, APIs, middleware |
| Data | Entities/models, DTOs/types/interfaces, migrations, seeds |
| Access | Authentication system, authorization/roles |
| Platform | Environment configuration, build configuration, deployment files, Docker |
| Integrations | File uploads, external services |
| Supporting | Utilities, dependencies |

### 3.2 Build a dependency map before deleting anything

Before calling something unused, check every way it can be referenced:

- Static imports, dynamic imports, and barrel exports
- Route, API, and database references
- Reflection and decorator usage
- Framework auto-discovery (file-based routing, DI containers, convention-based loading)
- Environment-variable usage
- Build scripts, Docker scripts, and CI/CD
- Migrations, seeds, tests, and configuration
- Runtime references

A text search coming up empty is **not** proof that code is unused. Framework-driven code is often referenced indirectly.

---

## Part 4 — What to Improve

### 4.1 Dead and duplicate code

After verifying usage, remove:

- Dead imports, variables, functions, and components
- Unreachable code and commented-out obsolete code
- Duplicate utilities and duplicate implementations
- Abandoned experimental code
- Redundant wrappers and unnecessary abstractions
- Obsolete constants and unused styles
- Unused dependencies
- Debugging code and development-only `console` statements

Only remove code when doing so cannot affect existing behaviour.

### 4.2 Time complexity

Look for:

- Nested loops and O(n²) operations
- Repeated `.find()`, `.filter()`, or `.map()` over the same dataset
- Duplicate transformations and repeated parsing
- Expensive computations inside render cycles
- Inefficient searching or sorting
- Repeated object/array creation
- Repeated API requests or database lookups
- Unnecessary serialization/deserialization

Where it genuinely helps, use `Map`, `Set`, indexing, memoization, precomputed lookup tables, or better algorithms. Prefer measurable, understandable improvements; do not add complexity just to claim an optimization.

### 4.3 Database performance

Identify and fix, without altering results:

| Problem | Typical fix |
|---|---|
| N+1 queries, queries inside loops | Joins or batched queries |
| Duplicate queries, repeated round trips | Consolidate or reuse results |
| Excessive eager loading, unnecessary relations | Load only what is needed |
| Fetching unnecessary columns | Select specific columns |
| Missing pagination | Add pagination where the contract allows |
| Inefficient filtering or joins | Rewrite the query |
| Missing indexes | Add indexes via a non-destructive migration |

Be extremely careful with migrations, constraints, foreign keys, cascades, transactions, and existing production data. **Never create destructive migrations** unless absolutely necessary, and never drop columns, tables, or data as part of cleanup.

### 4.4 Frontend performance

Review for:

- Unnecessary re-renders and excessive context updates
- Duplicate network or API requests
- Large client bundles and unnecessary client components
- Components that should stay server-side
- Unnecessary state, or derived state stored instead of computed
- Expensive render calculations and repeated transformations
- Poor list rendering and missing stable keys
- Incorrect memoization
- Huge components

Do not blindly add `useMemo`, `useCallback`, or `React.memo` — only where they provide a real benefit. Do not change visible UI or interaction behaviour.

### 4.5 Backend performance

Inspect controllers, services, repositories, guards, middleware, interceptors, DTO validation, database calls, serialization, file handling, authentication, authorization, and logging.

Reduce:

- Duplicate database queries, validation, and transformations
- Repeated business logic
- Excessive abstraction
- Unnecessary service-to-service calls

Keep controllers thin and business logic properly organized.

### 4.6 Architecture

Keep clear separation between UI, business logic, data access, validation, API communication, state, utilities, configuration, types, and constants. Avoid giant files and god classes/components.

Do **not** over-engineer. Skip factories, repositories, managers, adapters, providers, abstract classes, and generic wrappers when a straightforward implementation is easier to understand.

### 4.7 Large files

Split files that are doing too much, along clear responsibilities. For example, `booking.service.ts` should not also hold payment logic, email templates, aircraft scheduling algorithms, PDF generation, or reporting helpers if those can live independently. Do not split code just to produce more files.

### 4.8 File and directory structure

Reorganize only when it brings a real maintainability benefit. Use a predictable, domain-oriented structure. Do not move hundreds of files for aesthetics. Update every reference when a file moves.

### 4.9 DRY — but not extreme DRY

Extract shared logic when it clearly improves maintainability. Do not create overly generic helpers to eliminate three similar lines. Understandable duplication beats an abstraction that is hard to follow.

### 4.10 Shared utilities

Before creating a helper, search for existing similar logic. Consolidate true shared logic so the project does not end up with:

```text
utils/date.ts
helpers/date.ts
lib/date.ts
common/date.ts
```

all solving the same problem.

### 4.11 Naming

Replace meaningless names with domain-specific ones that communicate business intent. Do not rename public APIs unnecessarily.

| Avoid | Prefer |
|---|---|
| `data` | `bookingDetails` |
| `arr` | `passengerList` |
| `res` | `availabilityResponse` |
| `temp`, `value`, `obj`, `result`, `x`, `item2`, `finalData` | A name that says what it holds |

### 4.12 Function quality

Functions should have one responsibility, a descriptive name, predictable inputs and outputs, minimal hidden side effects, and few parameters. Reduce nesting and return early:

```ts
if (!user) {
  throw new Error(...);
}

if (!user.isActive) {
  throw new Error(...);
}

return processUser(user);
```

### 4.13 Type safety

Reduce `any`, unsafe casts, `as unknown as`, non-null assertions, and overly broad object types.

Use proper interfaces, DTOs, enums where appropriate, union types, generics where genuinely useful, shared domain types, and strict return types. Remove duplicate type definitions. Do not trade readability for clever types.

### 4.14 Error handling

Standardize error handling so that:

- Errors are meaningful and logged appropriately
- Sensitive information is never exposed
- API errors have a consistent structure
- User-facing errors stay useful
- Unexpected errors are distinguishable from expected validation errors

Never silently swallow failures. Avoid:

```ts
catch (error) {
  console.log(error);
}
```

### 4.15 Logging

Remove unnecessary `console.log()`, `console.debug()`, and temporary development messages. Keep useful production logging for errors, important system events, and critical operations.

Never log passwords, tokens, secrets, or sensitive customer information.

### 4.16 Comments

Remove comments that repeat the code:

```ts
// increment count
count++;
```

Keep comments that explain **why**: decisions, business rules, non-obvious edge cases, framework workarounds, security considerations, and performance choices.

### 4.17 Business rules

Make business-specific behaviour easy to understand by explaining why the rule exists:

```ts
// A booking may contain multiple flight sectors because
// repositioning and passenger sectors are managed under one booking.
```

This is far more useful than `// loop through sectors`.

### 4.18 Constants

Centralize repeated strings, status values, role values, limits, URLs, configuration, and magic numbers — using an established domain constant or enum where the architecture supports it:

```ts
// Instead of repeating:
if (role === 'super_admin') { ... }

// Use the domain constant:
if (role === Role.SuperAdmin) { ... }
```

Do not centralize values that are only used once.

### 4.19 Environment variables

Ensure that:

- Environment variables are validated at startup
- Missing required variables fail clearly
- Names are consistent and duplicates are removed where safe
- Server-only secrets never leak to the client

Never hardcode, print, or alter secret values.

### 4.20 Dependencies

Identify unused, duplicate, and obsolete packages, packages that duplicate framework/runtime features, and large libraries used for tiny operations. Remove a package only after confirming it is unused.

Do not perform risky major-version upgrades during cleanup — treat upgrades as separate work.

### 4.21 Security

While refactoring, look for obvious problems in:

- Authentication, authorization, and permission checks
- Input validation and injection
- File uploads and path traversal
- CORS
- Secrets, token handling, and password handling
- Sensitive logging

Fix clear defects when the fix does not change legitimate functionality. Document significant security changes.

### 4.22 Developer and LLM friendliness

A new developer or AI assistant should understand the project without reverse engineering it. Improve file names, folder names, module boundaries, types, service responsibilities, function names, constants, configuration, and documentation.

For complex modules, add short documentation covering:

- Purpose and main entry point
- Important dependencies
- Data flow
- Important business rules
- Common extension points

Do not flood the codebase with comments.

### 4.23 Tests and validation

Use existing tests. Run unit, integration, and E2E tests, type checking, linting, and builds where available. If a high-risk area lacks tests, add focused regression tests **before** refactoring it. Do not rewrite the whole test suite.

After significant changes, every app and package must build with **no new**:

- TypeScript or ESLint errors
- Broken imports or missing modules
- Circular dependency errors
- Build failures or runtime configuration errors

### 4.24 Do not hide errors

Do not silence errors with shortcuts:

```ts
// @ts-ignore
// @ts-nocheck
// eslint-disable
value as any
value as unknown as Foo
```

Fix the root cause unless there is a legitimate, unavoidable reason — and say what it is.

---

## Part 5 — Workflow

Work through these phases in order. Run validation at the end of each phase that modifies code.

### Phase 1 — Repository audit

Inspect the complete repository and form an understanding of its applications, packages, architecture, dependencies, data flow, and critical business logic. Rank findings:

| Severity | Covers |
|---|---|
| **Critical** | Potential bugs, security issues, data-loss risks |
| **High** | Major performance or architecture issues |
| **Medium** | Duplicated logic, overly complex modules, poor organization |
| **Low** | Formatting, naming, minor cleanup |

Do not modify code until you have enough context.

### Phase 2 — Establish a baseline

Record the project's current health before making large changes. Adapt the commands to the repository:

```bash
git status
pnpm install
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

Record existing failures separately. Do not attribute pre-existing issues to your refactoring.

### Phase 3 — Safe cleanup

Start with low-risk work: dead imports and variables, unreachable code, duplicate imports, debug logging, stale comments, obviously unused private helpers, simple naming fixes, and formatting inconsistencies.

### Phase 4 — Duplication cleanup

Find repeated business logic, validation, transformations, API logic, formatting logic, and database queries. Extract only meaningful reusable abstractions.

### Phase 5 — Performance optimization

Optimize confirmed inefficiencies. For each significant change, record:

- **Before** — what was inefficient
- **After** — what changed
- **Complexity** — e.g. `O(n²) → O(n)`, or a practical measure such as `101 queries for 100 bookings → 2 queries`

### Phase 6 — Architecture cleanup

Refactor overly complex modules. Improve separation of concerns, dependency direction, module boundaries, naming, reusability, and testability — without over-engineering.

### Phase 7 — Documentation

Create or update `README.md`, `ARCHITECTURE.md`, and `CONTRIBUTING.md` only where useful. An architecture document should cover:

1. Project overview
2. Repository structure
3. Applications
4. Core modules
5. Data flow
6. Authentication and authorization
7. Database architecture
8. API architecture
9. Environment variables
10. Development workflow
11. Build process
12. Deployment architecture
13. Important business rules
14. How to add a new feature safely

Documentation must describe the actual implementation, never imaginary architecture.

### Phase 8 — Final validation

Run all linting, type checking, tests, and builds. Review the full `git diff` and confirm:

- [ ] No features were accidentally removed
- [ ] No UI was unintentionally changed
- [ ] No routes were changed
- [ ] No API contract was broken
- [ ] No migration destroys data
- [ ] No secrets were committed
- [ ] No debug files remain

---

## Part 6 — Reporting

### Progress updates

Periodically summarize important changes in this format. Keep it concise and skip trivial formatting changes.

```text
Area:
Problem:
Change:
Benefit:
Risk:
Validation:
```

### Final report

At the end, provide:

1. **Executive summary** — what improved overall.
2. **Files / modules changed** — the important areas modified.
3. **Removed code** — significant dead or duplicate code removed, and why it was safe.
4. **Performance improvements** — only improvements actually made:

   | Operation | Before | After |
   |---|---|---|
   | Passenger lookup | O(n²) | O(n) |
   | Booking DB loading | N+1 queries | Batched |
   | Repeated transformation | 4 passes | 1 pass |

5. **Architecture improvements** — structural changes.
6. **Type-safety improvements** — changes to TypeScript types.
7. **Security improvements** — security-related changes.
8. **Documentation added/updated** — and what a new developer should read first.
9. **Validation results** — clearly separating pre-existing failures from new ones:

   ```text
   Lint:
   Typecheck:
   Tests:
   Build:
   ```

10. **Remaining recommendations** — improvements intentionally not made because they:
    - Require product decisions
    - Could break compatibility
    - Need a database migration
    - Need infrastructure changes
    - Require major dependency upgrades
    - Need production performance measurements

---

## Most Important Instruction

Do not optimize for lines deleted or files changed. Optimize for:

> **clarity + maintainability + performance + reliability + compatibility**

When you finish, another experienced developer — or another LLM — should be able to open the repository and quickly understand where functionality belongs, how data flows, where business rules live, how modules depend on each other, and how to extend the system safely.

The final application must keep the same **UI, UX, features, behaviour, API compatibility, and business logic**.

**Begin by auditing the repository before making any changes.**
