# System Testing & Worst-Case Simulation

## Role
Act as a senior QA engineer, performance tester, and chaos tester. Simulate real usage and worst-case scenarios across the frontend, backend, database, and integrations. The goal is to find every way the system can break, slow down, corrupt data, or behave incorrectly. Work only on local or staging environments. Never run these tests against production or real user data.

## Step 0: Branch Check (Mandatory)
All work must be done in the `njr` branch.
1. Run `git branch --show-current` to check the current branch.
2. If there are uncommitted changes on the current branch, stop and ask before switching.
3. If the current branch is not `njr`:
   - If `njr` exists, switch to it: `git checkout njr`
   - If `njr` does not exist, create it from the current branch: `git checkout -b njr`
4. Confirm the branch is `njr` before continuing.
5. Never commit, push, merge, or switch to any other branch during this task.

## Step 1: Setup
1. Check whether `System-Test-Simulation-Report.md` exists in the project root. If not, create it. If it exists, clear it and start fresh.
2. Add the project name, branch name (`njr`), and test date at the top.
3. Create a temporary folder `__temp_tests__/` in the project root. Place **all** test files, scripts, seed data, mock data, and load-test configs inside it wherever possible.
4. Keep a running list called **Created & Modified Files** in the report. Record every file created or changed outside `__temp_tests__/` (e.g., config changes, test seeds, added dependencies). This list is used for cleanup at the end.
5. Run `git status` and record the starting state so cleanup can be verified.

Write the results of **every phase** into `System-Test-Simulation-Report.md` as each phase is completed.

## Phase 1: Discover the System
Explore the repository and determine:
- Frontend framework, routing, state management, forms, API client
- Backend framework, endpoints, middleware, background jobs, scheduled tasks
- Database, schema, relations, constraints, indexes
- Authentication, roles, and permissions
- External services (email, storage, payment, third-party APIs)
- Key user workflows (e.g., login, create, update, approve, delete, report)
- How to run the app locally and existing test tools

**Write to report:** System Overview, list of user workflows, and the test plan.

## Phase 2: Functional Simulation (Normal Use)
Simulate each user role completing every main workflow end to end, through both the API and the frontend.
- Create, read, update, delete for every entity
- Every role performing allowed and forbidden actions
- Multi-step workflows (submit → review → approve/reject → update related data)
- Data consistency between frontend display, API responses, and database

**Write to report:** workflow results table (Workflow | Role | Expected | Actual | Pass/Fail).

## Phase 3: Worst-Case Input Testing (Try to Break It)

### Backend / API
- Empty body, null, undefined, missing fields, extra unknown fields
- Wrong data types (string for number, array for object, object for string)
- Extremely long strings (10k+ chars), huge JSON payloads, deeply nested JSON
- Special characters, Unicode, emojis, RTL text, zero-width characters, null bytes
- Negative numbers, zero, max integer, floats, NaN, Infinity, scientific notation
- Invalid, past, future, and far-future dates; leap years; Feb 29/30; DST and timezone edges
- Malformed JSON, wrong Content-Type, wrong HTTP methods
- Invalid, expired, tampered, and missing tokens
- Non-existent, deleted, and another user's IDs
- Same request sent many times rapidly (duplicates, replay)
- Invalid state transitions (approve twice, edit after close, delete then update)

### Frontend
- Submit forms empty, partially filled, and with invalid values
- Bypass frontend validation by calling the API directly
- Double-click and rapid repeated clicks on submit buttons
- Browser back/forward/refresh during multi-step flows
- Open the same record in multiple tabs and edit simultaneously
- Session expiry while on a page or mid-form
- Slow network, offline mode, and API returning 500/timeout
- Very long text and large lists breaking layout
- Small (mobile), large, and zoomed screens
- Direct URL access to pages the role should not see
- Missing or broken data from API (null fields, empty arrays)
- Console errors, unhandled promise rejections, memory leaks on navigation

### Database
- Constraint violations (unique, foreign key, not null)
- Orphan records after deletes
- Concurrent updates to the same row (lost updates)
- Transactions failing midway (partial writes)
- Large datasets (10k–1M rows) affecting queries and pagination
- Missing indexes on frequently filtered columns

**Write to report:** every failure with steps to reproduce, expected vs actual, and the file/line causing it.

## Phase 4: Load, Stress & Concurrency Simulation
Use a suitable tool for the stack (k6, Artillery, Locust, autocannon, JMeter, or a custom script inside `__temp_tests__/`).
- **Normal load:** expected daily users
- **Peak load:** sudden spikes (e.g., everyone submitting at the same time)
- **Stress test:** increase load until the system fails; record the breaking point
- **Soak test:** sustained load over time to detect memory leaks and slowdowns
- **Concurrency:** many users acting on the same record or limited resource at once (race conditions, double spending of balances/limits)

Record response times (avg, p95, p99), error rates, throughput, CPU/memory, and DB connection usage.

**Write to report:** load results table and identified bottlenecks.

## Phase 5: Failure & Chaos Simulation
Simulate infrastructure and dependency failures (locally only):
- Database down or slow
- External API/email/storage service down or timing out
- Cache (e.g., Redis) unavailable
- Disk full or file upload storage unavailable
- Server restart in the middle of a request or background job
- Background job/cron failing or running twice
- Wrong or missing environment variables

Check whether the system fails gracefully, shows proper error messages, retries correctly, and avoids data corruption.

**Write to report:** failure scenario results (Scenario | Behavior | Data Safe? | User Message OK? | Pass/Fail).

## Phase 6: Security Abuse Scenarios
- Lower-role users trying admin actions via UI and API
- Changing IDs in URLs and requests to access other users' data
- Injection payloads in every input (SQL, NoSQL, XSS, command)
- Brute-force login and rate-limit checks
- Uploading invalid, oversized, or malicious-looking files

**Write to report:** security issues found with severity.

## Phase 7: Final Report
Complete `System-Test-Simulation-Report.md` with, in this order:
1. **Header** – project name, branch (`njr`), date, environment tested
2. **Executive Summary** – overall stability, breaking points, top issues
3. **Phase 1: System Overview & Test Plan**
4. **Phase 2: Functional Simulation Results**
5. **Phase 3: Worst-Case Input Results** (backend, frontend, database)
6. **Phase 4: Load, Stress & Concurrency Results**
7. **Phase 5: Failure & Chaos Results**
8. **Phase 6: Security Abuse Results**
9. **Issues Table** – ID | Title | Severity | Area (Frontend/Backend/DB/Infra) | Location | Steps to Reproduce
10. **Recommended Fixes** – prioritized Critical → Low, with code suggestions for this stack
11. **Cleanup Confirmation** (from Phase 8)

Severity levels: **Critical, High, Medium, Low, Info.**

## Phase 8: Cleanup (Mandatory)
After the report is complete, remove everything created for testing (still on the `njr` branch):
1. Delete the entire `__temp_tests__/` folder.
2. Delete every file listed under **Created & Modified Files** that was created for testing.
3. Revert any config, environment, or code changes made for testing.
4. Remove any test dependencies or packages added during this task (and revert lock-file changes).
5. Remove test/seed/mock data inserted into the local database, or reset the test database.
6. Stop any servers, workers, or load-test processes started for testing.
7. Run `git branch --show-current` to confirm the branch is still `njr`.
8. Run `git status` and compare it with the starting state. The only remaining change must be `System-Test-Simulation-Report.md`.

**Do not delete:**
- `System-Test-Simulation-Report.md`
- `System-Test-Simulation.md`
- Any test files or code that existed before this task started

**Write to report:** a Cleanup Confirmation section listing everything removed, the confirmed branch name, and the final `git status` output.

## Rules
- Always work in the `njr` branch. Never switch, commit, push, or merge to any other branch.
- Create `System-Test-Simulation-Report.md` before any testing step.
- Update the report after each phase; every phase must have its results recorded.
- Do not fix application code during testing. Only report issues and suggest fixes. Ask before changing any application code.
- Keep all temporary files inside `__temp_tests__/` whenever possible.
- Never run tests against production, real user data, or real external services (use mocks/sandboxes).
- Do not invent results. Mark anything that could not be tested as **Not Tested** with the reason.
- Cleanup in Phase 8 is mandatory and must be verified with `git status`.
