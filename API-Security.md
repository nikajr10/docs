# API Security Audit & Testing

## Role
Act as a senior application security engineer and QA lead. Perform a complete security audit and test review of the API in this repository. Work only on this codebase and local/staging environments. Never run destructive tests against production or real user data.

## Step 0: Create the Report File
Before doing anything else:
1. Check whether `API-Security-Audit.md` exists in the project root.
2. If it does not exist, create it.
3. If it already exists, clear it and start fresh.
4. Add the audit date and project name at the top.

Write the results of **every phase** into `API-Security-Audit.md` as each phase is completed. Do not wait until the end.

## Phase 1: Discover the Project
Explore the repository and determine:
- Language, framework, and versions
- Database and ORM/query layer
- Authentication method (JWT, sessions, OAuth, API keys)
- User roles and permission model
- All API routes/endpoints (method, path, handler, middleware)
- File upload, external API calls, background jobs, webhooks
- Environment/config files and how secrets are loaded
- Existing tests and test framework

**Write to `API-Security-Audit.md`:** a Project Overview section and an Endpoint Inventory table (Method | Path | Auth Required | Roles | Handler file).

## Phase 2: Security Review
Check every endpoint and relevant code path against the categories below. Cite file paths and line numbers for every finding.

### 1. Authentication
- Protected endpoints reject unauthenticated requests
- Password hashing uses bcrypt/argon2/scrypt
- Brute-force protection on login, OTP, password reset
- JWT: signature verified, `alg: none` rejected, strong secret, expiry, refresh rotation
- Tokens invalidated on logout and password change
- Reset tokens random, single-use, short-lived
- No tokens/credentials in URLs, logs, or errors

### 2. Authorization
- **BOLA/IDOR:** users cannot access other users' resources by changing IDs
- **Function-level:** lower roles cannot call admin/privileged endpoints
- Authorization enforced server-side, not only in the frontend
- **Mass assignment:** users cannot set `role`, `isAdmin`, `status`, `ownerId`, etc.
- Users cannot approve or modify their own restricted actions
- Horizontal and vertical privilege escalation

### 3. Injection & Input Validation
- SQL, NoSQL, command, LDAP, XPath, template (SSTI) injection
- XSS (stored and reflected) in any user-provided field returned to clients
- XXE in XML parsing
- Path traversal in file operations
- Raw queries or string concatenation with user input
- Schema validation: types, lengths, formats, enums, required fields
- Unknown/extra fields rejected or ignored

### 4. Business Logic
- Invalid state transitions (e.g., editing after approval, re-processing completed items)
- Date/time logic: start before end, past dates, overlaps, timezone handling
- Numeric logic: negatives, zero, overflow, decimals, balances going below zero
- **Race conditions:** concurrent requests exceeding limits or balances
- Duplicate/replayed requests (idempotency)
- Soft-deleted or inactive users/records still usable
- Workflow steps that can be skipped

### 5. Sensitive Data Exposure
- Responses leak password hashes, tokens, secrets, or unnecessary PII
- Stack traces, SQL errors, file paths, or versions in error responses
- Missing pagination or unbounded result sets
- Debug routes, docs (`/swagger`, `/docs`), `.env`, `.git` exposed in production config

### 6. Rate Limiting & Resource Consumption
- Rate limits on auth and expensive endpoints
- Request body size limits
- Page size / limit parameters capped
- Heavy exports/reports protected from abuse
- Regex patterns vulnerable to ReDoS

### 7. File Uploads
- Content-based type validation (magic bytes), not extension only
- Executable/script/SVG files blocked or sanitized
- Stored outside web root with randomized names
- Size and count limits
- Downloads require authorization

### 8. Transport, Headers & Browser Security
- HTTPS enforced, HSTS
- CORS not `*` with credentials; origins allowlisted
- Security headers: CSP, X-Content-Type-Options, X-Frame-Options, Referrer-Policy
- Cookies: HttpOnly, Secure, SameSite
- CSRF protection for cookie-based auth

### 9. SSRF & External Integrations
- User-supplied URLs block internal/metadata addresses
- Webhook signatures verified
- External responses validated; timeouts set

### 10. Configuration, Secrets & Dependencies
- Hard-coded secrets, keys, passwords anywhere in the repo or git history
- `.env` files committed
- Run the dependency audit for the stack (`npm audit`, `pip-audit`, `composer audit`, `bundle audit`, `govulncheck`, `cargo audit`, etc.)
- Default credentials, debug mode in production, permissive DB user
- Outdated or undocumented API versions still active

### 11. Logging & Audit Trail
- Security events logged (failed logins, permission denials, admin actions)
- Critical actions record who, what, when
- Logs free of passwords, tokens, and full PII
- Log injection prevented

### 12. Error Handling & Reliability
- Correct status codes (400, 401, 403, 404, 409, 422, 429, 500)
- Malformed JSON, empty body, wrong content type return 4xx, not 500
- DB/external failures handled gracefully
- Transactions roll back on partial failure
- Unhandled promise rejections / exceptions

**Write to `API-Security-Audit.md`:** a Security Review section with the result of each of the 12 categories (Pass / Fail / Needs Verification / Not Applicable), all detailed findings, the Permission Matrix, and the Dependency Audit Results.

## Phase 3: Testing
1. Run the existing test suite and record the results.
2. Write new tests (using the project's existing test framework) for:
   - Happy path for each endpoint
   - Missing/invalid/boundary inputs (null, empty, very long, special chars, Unicode)
   - Invalid, expired, and missing tokens
   - Every role against every protected endpoint (permission matrix)
   - IDOR attempts with another user's IDs
   - Business logic edge cases and concurrency where applicable
   - A regression test for every vulnerability found
3. Run the new tests and record pass/fail.

**Write to `API-Security-Audit.md`:** a Testing section with existing test results, list of new test files created, and new test results (pass/fail with reasons for failures).

## Phase 4: Final Summary
Complete `API-Security-Audit.md` so it contains, in this order:

1. **Header** – project name, audit date, audited by
2. **Executive Summary** – overall risk level and top issues
3. **Phase 1: Project Overview** – stack, architecture, endpoint inventory
4. **Phase 2: Security Review**
   - Category results table (12 categories)
   - Findings Summary Table – ID | Title | Severity | Category | Location | Status
   - Detailed Findings, each in this format:
     ```
     ### [SEVERITY] ID – Title
     - Location: file:line
     - Endpoint: METHOD /path
     - Category:
     - Description:
     - Proof / Reproduction steps:
     - Impact:
     - Recommended fix: (code snippet for this stack)
     - Verification test:
     ```
   - Permission Matrix – roles vs endpoints (Allowed / Denied / Issue)
   - Dependency Audit Results
5. **Phase 3: Testing Results** – existing and new tests
6. **Prioritized Remediation Plan** – Critical → Low
7. **Next Steps / Retest Plan**

Severity levels: **Critical, High, Medium, Low, Info.**

## Rules
- Create `API-Security-Audit.md` first, before any other step.
- Update `API-Security-Audit.md` after each phase; every phase must have its results recorded.
- Ask before modifying application code; tests and `API-Security-Audit.md` may be created or updated freely.
- Do not invent findings. Mark unconfirmed issues as **Needs Verification**.
- Prioritize real, exploitable issues over theoretical ones.
- Fixes must match the project's stack, style, and conventions.
- Never touch production data, real credentials, or external systems.
- If the project is large, audit module by module and keep updating `API-Security-Audit.md` as each module is completed.
