---
type: audit
read_when: Only when the owner asks for a full backend review.
then: workflow.md step 7 (Record)
---

# Backend Engineering Review (Principal-Level)

## Role
Act as a principal/staff-level backend engineer with long production experience. Review the backend of this project the way a most-senior engineer would before approving it for production and scale: correctness, security, reliability, performance, scalability, maintainability, operations, and cost. Judge every technology choice by **"Is it needed now, at this scale, for this problem?"** Recommend tools like Redis, Kafka, or Elasticsearch only when the project actually needs them, and explain why. This is a **review task**: do not modify application code unless explicitly asked.

## Step 0: Branch Check (Mandatory)
All work must be done in the `njr` branch.
1. Run `git branch --show-current`.
2. If there are uncommitted changes on the current branch, stop and ask before switching.
3. If the current branch is not `njr`: switch with `git checkout njr`, or create it with `git checkout -b njr` if it does not exist.
4. Never commit, push, merge, or switch to another branch during this task.

## Step 1: Create the Report File
Before reviewing anything:
1. Check whether `Backend-Consideration-Report.md` exists in the project root.
2. If it does not exist, create it. If it exists, clear it and write this run's report and findings into the same file. Never create a second, dated or numbered report file.
3. Add the project name, branch (`njr`), and review date at the top.

Write results into `Backend-Consideration-Report.md` **after each section is reviewed**. Do not wait until the end.

## Step 2: Discover the Project
Explore the repository and determine:
- Language, framework, and versions
- Folder structure and architecture pattern (monolith, modular monolith, microservices)
- Database(s), ORM, migration tool
- Authentication method and roles
- Main modules, features, and critical user workflows
- Background jobs, queues, scheduled tasks
- Caching, messaging, search, storage already in use
- External integrations
- Testing setup, CI/CD, hosting, deployment method
- Environment and configuration handling

Then estimate the **scale profile** (from code, config, docs, or ask if unknown):
- Number of users (total and concurrent)
- Requests per second (average and peak)
- Data volume and growth rate
- Read-heavy vs write-heavy
- Latency expectations
- Team size and operational capacity
- Budget/hosting constraints

**Write to report:** Project Overview and Scale Profile. All technology recommendations later must be justified against this scale profile.

## Step 3: Review Against Each Area
For every item, mark:
- ✅ **Done** – implemented correctly
- ⚠️ **Partial** – exists but incomplete or has issues
- ❌ **Missing** – not implemented but needed
- ➖ **Not Needed / N/A** – not required at the current scale or not relevant (explain why)

For every ⚠️ and ❌: record **what is missing or wrong, location (file:line), risk/impact, recommended fix (code for this stack), effort, priority.**

---

### 1. Architecture & Design
- Clear layers: Routes/Controllers → Services → Repositories/Models
- Thin controllers; business logic in services; domain rules centralized
- Feature/domain-based modules with clear boundaries
- No circular dependencies; low coupling, high cohesion
- SOLID principles applied sensibly (not dogmatically)
- Dependency injection where it improves testability
- Configuration separated from code
- **Monolith vs microservices decision:**
  - Prefer a **well-structured modular monolith** for small/medium teams and early products.
  - Consider microservices only when: independent scaling needs, separate teams owning domains, different deployment cycles, or clear bounded contexts. Microservices add network failures, distributed transactions, observability and DevOps cost.
- Event-driven design only where decoupling or async processing is truly needed
- Design for failure: what happens when each dependency is down?

### 2. API Design
- RESTful naming, correct methods and status codes
- Consistent response and error format (with error codes)
- **Pagination on every list endpoint.** No endpoint returns an unbounded list.
  - Default page size (e.g., 20) and a hard maximum (e.g., 100) enforced on the server, whatever the client asks for
  - Offset/limit only for small tables; **cursor/keyset pagination** (`WHERE (created_at, id) < (?, ?) ORDER BY created_at DESC, id DESC LIMIT ?`) for large, growing or real-time tables, because deep `OFFSET` scans and skips rows
  - Stable sort with a unique tiebreaker (e.g., `id`) so rows are not duplicated or skipped between pages
  - Total count only when the UI needs it; `COUNT(*)` on large tables is expensive, so cache it or use an estimate
  - Pagination metadata in a consistent shape (`nextCursor`, `hasMore`, or `page`, `pageSize`, `total`)
- Filtering and sorting fields **allow-listed** (prevents injection through `ORDER BY` and slow sorts on unindexed columns)
- Tables load in one request per page. No request per row (no "fetch details for each row" loops); include what the table needs in the list query
- Bulk endpoints for batch actions (bulk update/delete/import) instead of the client calling N times
- Responses return only the fields the client needs (no full DB objects, no internal or sensitive fields)
- Consistent error format, ideally RFC 9457 Problem Details (`type`, `title`, `status`, `detail`, error code)
- Request ID returned in a response header and included in error bodies for support
- `Content-Type` enforced; unexpected content types rejected (415)
- `429 Too Many Requests` with `Retry-After` when rate limited
- Long-running work returns `202 Accepted` with a status endpoint, not a request that hangs
- No state change on `GET`
- API versioning and deprecation strategy (sunset dates, `Deprecation` header)
- Idempotency keys for retryable writes (payments, orders, bookings)
- Backward compatibility
- OpenAPI/Swagger documentation, kept in sync with the code
- **API inventory:** every endpoint, version and environment known; old versions, debug, test and internal endpoints removed or protected (OWASP API9)
- **Third-party API responses treated as untrusted:** validated, size-limited, timeouts set, redirects not blindly followed (OWASP API10)
- **REST vs GraphQL vs gRPC vs WebSockets:**
  - REST: default for most CRUD/business APIs.
  - GraphQL: many clients needing flexible, nested data; avoid for simple CRUD.
  - gRPC: internal service-to-service, high performance, strict contracts.
  - WebSockets/SSE: real-time updates (notifications, live dashboards, chat). SSE for one-way server push; WebSockets for two-way.
  - Polling: acceptable for low-frequency updates at small scale.

### 3. Validation
- Server-side validation for body, params, query, headers
- Schema validator used consistently
- Unknown fields rejected/stripped (mass assignment protection: a user cannot set `role`, `isAdmin`, `ownerId`, `balance`, `price` or `status` through a request body)
- Allow-list validation (type, length, range, format, enum), not block-lists
- Limits on string length, array size, JSON nesting depth and total body size
- Numbers checked for range and overflow; money never accepted as a float
- Dates and date ranges validated (start before end, sensible bounds, explicit timezone)
- IDs validated in format (UUID/integer) before reaching the DB
- Client-side validation never trusted; the server validates everything again
- Business rule validation in services (negative quantities, price from the server not the client, coupon reuse, skipping workflow steps)
- Normalization before validation (trim, lowercase emails, Unicode normalization, consistent date formats)
- Regexes safe from catastrophic backtracking (ReDoS); untrusted input not used to build regexes
- JavaScript: keys like `__proto__`, `constructor`, `prototype` rejected (prototype pollution)
- No unsafe deserialization of untrusted data (Python `pickle`, Java native serialization, `yaml.load` without a safe loader, PHP `unserialize`)
- XML parsers have external entities and DTDs disabled (XXE)

### 4. Authentication & Authorization
**Passwords**
- Hashed with **Argon2id** (preferred; OWASP minimum m=19 MiB, t=2, p=1), scrypt, or bcrypt (work factor ≥ 10, 72-byte input limit). PBKDF2-HMAC-SHA256 with ≥ 600,000 iterations only where FIPS is required
- Never plain text, MD5, SHA-1, or a single fast SHA-256; never encrypted (reversible) passwords
- Unique salt per password (built into the algorithms above); optional pepper kept in the secret manager
- Hash parameters upgraded over time: rehash on next successful login
- NIST SP 800-63B-4 rules: minimum 15 characters when the password is the only factor, 8 when used with MFA; allow at least 64 characters; no forced composition rules; no forced periodic rotation; check new passwords against breached/common password lists (e.g., Have I Been Pwned k-anonymity API)

**Login and account flows**
- Generic error messages on login, signup and password reset ("invalid email or password"); no user enumeration through messages, status codes or response timing
- Brute-force protection: throttling with increasing delays per account and per IP, CAPTCHA after repeated failures; avoid permanent lockout that lets attackers lock out real users
- Password reset tokens: random (≥ 128 bits from a CSPRNG), stored hashed, single-use, short expiry (15–60 min), invalidated when used or when the password changes
- Reset and verification links built from configured base URL, never from the request `Host` header (host header injection)
- All sessions and refresh tokens invalidated after a password change or reset
- Email change requires confirmation from both old and new address; re-authentication for sensitive actions (change email/password, MFA settings, payout details, delete account)
- **Default, test and demo credentials removed or changed** in every environment (app admin, DB, Redis, RabbitMQ `guest/guest`, Grafana `admin/admin`, CMS, cloud consoles); first admin forced to set a password

**Multi-factor authentication**
- MFA available to all users and **required for admin and privileged roles**
- TOTP or WebAuthn/passkeys preferred (phishing-resistant); SMS only as a fallback
- Recovery codes generated once, stored hashed, single-use
- MFA cannot be bypassed through another path (API login, password reset, OAuth link, "remember me")
- OTP codes rate-limited, short-lived and single-use

**Sessions and tokens**
- Session vs JWT choice justified (sessions + Redis for easy revocation; JWT for stateless/distributed)
- Session ID regenerated on login and privilege change (session fixation)
- Cookies: `HttpOnly`, `Secure`, `SameSite=Lax` or `Strict`, `__Host-` prefix where possible, narrow `Path`/`Domain`
- Idle and absolute session timeouts; logout invalidates the session on the server
- **Auth tokens not stored in `localStorage` or `sessionStorage`** (any XSS can read them); use `HttpOnly` cookies, or keep access tokens in memory only
- Access tokens short-lived (5–15 min); refresh tokens rotated on every use with reuse detection, stored hashed, revocable
- Users can see and revoke active sessions/devices

**JWT**
- **Secret is long and random** (≥ 256 bits) from the secret manager, never a default or guessable value (`secret`, `changeme`, the app name), different per environment
- Asymmetric signing (RS256/ES256/EdDSA) when several services verify tokens; key rotation with `kid` and JWKS
- Allowed algorithms pinned on verify; `alg: none` and algorithm confusion rejected
- `exp`, `nbf`, `iss` and `aud` validated on every request
- No sensitive data in the payload (it is only encoded, not encrypted)
- Revocation strategy exists (short expiry + denylist or token version per user)

**OAuth / SSO**
- Authorization Code flow with PKCE; no implicit flow
- `state` and `nonce` checked; redirect URIs matched exactly
- ID tokens validated (signature, issuer, audience, expiry)
- Account linking by verified email only
- SSO/OAuth if needed by organization

**Authorization**
- **Deny by default.** Every protected endpoint checks permission on the server; hidden buttons and client-side role checks are UI only, never security
- **Object-level authorization (BOLA / IDOR, OWASP API1):** every read, update and delete of a record checks the caller owns it or is allowed to access it (`WHERE id = ? AND owner_id = ?`), including nested routes, file downloads, exports and websockets
- **Function-level authorization (OWASP API5):** admin and internal actions check role on the server
- **Property-level authorization (OWASP API3):** users cannot read or write fields they are not allowed to
- Roles, user ID and tenant ID come from the verified session/token, never from the request body, query or headers
- RBAC or ABAC centralized in middleware/policies, not repeated by hand in each handler
- Negative tests prove user A cannot read or change user B's data, and a normal user cannot call admin endpoints
- **Row-Level Security (RLS)** enabled with tested policies on every table reachable directly from the client (Supabase, PostgREST, Firebase rules, Hasura); service role / admin keys only on the server
- API keys: stored hashed, scoped, rotatable, with an identifying prefix; revocable per key
- Service-to-service calls authenticated (mTLS or signed short-lived tokens), not trusted because they are "internal"
- Least privilege for users, services, DB accounts, cloud IAM

### 5. Security
Check every item against real code. For a deeper audit, `security.md` and `API-Security.md` cover these in full.

**Injection**
- **SQL injection:** parameterized queries / ORM bindings only; no string concatenation or template strings in SQL, including `ORDER BY`, `LIMIT`, column and table names (allow-list these)
- Raw-query escape hatches searched and reviewed (`$queryRawUnsafe`, `knex.raw`, `sequelize.literal`, `.extra()`, `DB::raw`, `cursor.execute(f"...")`)
- **NoSQL injection:** input cast to expected types; operator objects (`$ne`, `$gt`, `$where`, `$regex`) rejected from user input
- **Command injection:** no shell execution with user input; use argument arrays (`execFile`, `subprocess.run([...])`), never `shell=True` / `exec` with strings
- No `eval`, `new Function`, or dynamic `require/import` with user input
- Template injection (SSTI): users never control template source
- Path traversal: file paths built from user input normalized and confirmed to stay inside the allowed directory
- Header/CRLF and log injection: newlines stripped from values written to headers and logs
- LDAP/XPath injection where those are used

**Cross-site scripting (XSS)**
- Context-aware output encoding; framework auto-escaping not bypassed (`dangerouslySetInnerHTML`, `v-html`, `|safe`, `{!! !!}`, `innerHTML`) unless sanitized with DOMPurify or a server-side equivalent
- User-supplied rich text/Markdown sanitized on the server with an allow-list
- **Content-Security-Policy** set (nonce- or hash-based; no `unsafe-inline`/`unsafe-eval` for scripts)
- API responses use the correct `Content-Type` with `X-Content-Type-Options: nosniff`
- User-uploaded HTML/SVG served from a separate domain or with `Content-Disposition: attachment`

**CSRF**
- Required whenever auth rides on cookies
- `SameSite` cookies plus a CSRF token (synchronizer token or signed double-submit) on every state-changing request
- `Origin` / `Sec-Fetch-Site` checked on state-changing requests
- No state changes on `GET`

**CORS**
- Explicit allow-list of origins per environment; never `*` with credentials
- Never reflect the request `Origin` back unchecked; `null` origin rejected
- Only needed methods and headers allowed; `localhost` origins not allowed in production

**Security headers and transport**
- HTTPS everywhere; HTTP redirects to HTTPS; TLS 1.2+ (prefer 1.3), weak ciphers disabled
- `Strict-Transport-Security: max-age=31536000; includeSubDomains` (add `preload` when ready)
- CSP, `X-Content-Type-Options`, `frame-ancestors` / `X-Frame-Options` (clickjacking), `Referrer-Policy`, `Permissions-Policy`
- `X-Powered-By` and server version headers removed
- Open redirects blocked: redirect targets checked against an allow-list

**Rate limiting and resource limits (OWASP API4, API6)**
- Rate limits per IP and per user/API key, with a shared store (Redis) when running more than one instance
- Stricter limits on login, signup, password reset, OTP/MFA, email/SMS sending (cost abuse), search, exports and expensive reports
- Request body size, upload size, header size and request timeout limits
- GraphQL: depth, complexity and batching limits; introspection off in production unless the API is public
- Protection for sensitive business flows from automation (mass signups, ticket/stock scalping, coupon abuse, scraping)
- Edge protection (WAF, CDN DDoS protection) for public-facing apps

**File uploads**
- Extension allow-list **and** content check by magic bytes on the server; client `Content-Type` not trusted
- Size limit per file and per request; count limit
- Stored with a random name, outside the web root or in a private bucket; original filename never used as a path
- No execute permission on upload storage; uploads never served from the app domain as HTML
- Images re-encoded and EXIF/GPS metadata stripped
- Malware scan (e.g., ClamAV or a cloud scanner) for files other users will download
- Archive limits (zip bombs, nested archives, path traversal inside zips)
- SVG treated as active content (sanitized or served as attachment)
- Presigned upload URLs short-lived, with content-type and size conditions; downloads through short-lived signed URLs after an authorization check

**SSRF**
- Every feature that fetches a user-supplied URL found (webhooks, link previews, image/URL import, PDF/HTML renderers, integrations)
- Destinations allow-listed where possible; otherwise private, loopback and link-local ranges blocked (IPv4 and IPv6), including cloud metadata `169.254.169.254`
- DNS resolved once and the resolved IP checked and used (DNS rebinding); redirects disabled or re-validated
- Only `http`/`https` schemes; no `file://`, `gopher://`, `ftp://`
- AWS IMDSv2 required; outbound traffic from servers restricted where possible

**Webhooks**
- **Incoming webhook signatures verified** (HMAC over the raw body, constant-time compare) using the provider's SDK where available (Stripe, GitHub, Slack, etc.)
- Timestamp checked (e.g., within 5 minutes) to stop replays; event ID stored so duplicates are processed once
- Webhook handler returns fast and does the work in a background job
- Outgoing webhooks signed, with a secret per subscriber, and protected against SSRF

**Secrets and keys**
- **API secrets kept on the server.** Frontend env vars (`NEXT_PUBLIC_`, `VITE_`, `REACT_APP_`, `EXPO_PUBLIC_`) are public; no private keys there. Third-party calls needing secrets go through the backend
- Supabase `service_role`, Firebase Admin, Stripe secret keys, DB URLs never shipped to the client or mobile app
- Secrets in env/secret manager (Vault, AWS Secrets Manager, GCP Secret Manager, Doppler), none in code, git history, Docker images, CI logs or error messages
- Git history scanned for leaked secrets (gitleaks, trufflehog); leaked secrets rotated, not just deleted
- Separate keys per environment; keys scoped to least privilege; rotation process documented

**Cryptography**
- Tokens, IDs and codes for security generated with a CSPRNG (`crypto.randomBytes`, `secrets`), never `Math.random`
- Sensitive fields encrypted at the application level where required (AES-256-GCM or libsodium) with keys in KMS; no home-made crypto
- Encryption in transit and at rest for sensitive data; backups encrypted
- Secrets and tokens compared in constant time

**Information exposure**
- No stack traces, SQL errors, file paths or framework versions in production responses
- **Source maps not publicly served** in production (upload privately to the error tracker instead)
- Debug mode, debug toolbars, `/actuator`, `/debug`, phpinfo and test routes disabled or protected in production
- Swagger/GraphiQL/admin panels behind auth or IP restriction in production
- `.git`, `.env`, backups and directory listings not served
- Error responses the same for "not found" and "not allowed" where existence itself is sensitive

**Sensitive data in logs**
- Never logged: passwords, tokens, cookies, `Authorization` headers, API keys, OTPs, reset links, full card numbers, CVV, secrets, full request bodies of auth/payment routes
- Redaction applied in the logger itself, not left to each call site
- PII in logs minimized and masked; log access restricted

**Dependencies and supply chain (OWASP A03:2025)**
- Lockfile committed; reproducible installs (`npm ci`, `pip install --require-hashes`, `poetry.lock`)
- **Vulnerable dependencies updated:** `npm audit`, `pip-audit`, `composer audit`, `govulncheck`, Snyk, or Dependabot/Renovate; Critical/High fixed within a defined time
- Abandoned, unmaintained or typo-squatted packages replaced; new packages checked before adding
- Container base images minimal and scanned (Trivy, Grype)
- CI actions pinned to a commit SHA; CI tokens least-privilege
- SBOM generated for production builds where customers or compliance require it

**Infrastructure exposure**
- Databases, Redis, Elasticsearch, MongoDB and queues not reachable from the internet; password/auth enabled on all of them
- Firewall/security groups least privilege; SSH by key only, or no SSH (use a bastion/SSM)
- Admin interfaces on a private network or behind SSO/VPN

**Security testing**
- SAST (Semgrep, CodeQL), secret scanning and dependency scanning in CI
- DAST (OWASP ZAP) against staging for public apps
- Penetration test before major launches or when handling payments/health/personal data
- OWASP Top 10:2025 and OWASP API Security Top 10 (2023) coverage recorded in the report

### 6. Database
- Correct database type for the workload:
  - **Relational (PostgreSQL/MySQL):** default for business data, relations, transactions.
  - **Document (MongoDB):** flexible schema, nested documents, fewer relations.
  - **Key-value (Redis):** cache, sessions, counters, locks — not a primary store.
  - **Time-series (TimescaleDB, InfluxDB):** metrics, logs, sensor data at scale.
  - **Search (Elasticsearch/OpenSearch/Meilisearch):** full-text search, fuzzy search, analytics.
- Proper types, constraints, defaults, normalization (denormalize only for proven performance needs)
- Indexes on filtered/joined/sorted columns; composite indexes in correct order; no unused indexes
- Query plans checked (`EXPLAIN`) for slow queries
- Migrations for every change; reversible; safe for large tables (no long locks)
- Transactions with correct isolation level
- **No queries inside loops (N+1).** Related rows loaded with a JOIN, `WHERE id IN (...)`, or ORM eager loading (`include`, `select_related`/`prefetch_related`, `with()`, `joinedload`); DataLoader for GraphQL resolvers
- **No row-by-row writes in loops.** Bulk insert/update (`INSERT ... VALUES (...), (...)`, `createMany`, `bulk_create`, `insertMany`, `COPY`), in chunks (e.g., 500–1000 rows)
- Large tables never loaded fully into memory; read with keyset pagination or a streaming cursor
- No unnecessary `SELECT *`; only needed columns, especially on wide tables and list endpoints
- Constraints enforce invariants in the DB: `NOT NULL`, `UNIQUE`, `CHECK`, foreign keys (with indexes) and deliberate `ON DELETE` behaviour
- Money stored as `DECIMAL`/`NUMERIC` or integer minor units, never float
- Concurrency: row locks, optimistic locking, atomic updates (`UPDATE ... SET qty = qty - 1 WHERE qty > 0`), unique constraints for duplicates
- Deadlocks and serialization failures retried safely
- Short transactions; no external API calls or slow work inside a transaction
- Statement timeout and lock timeout set
- Slow query log enabled and reviewed
- Soft delete and audit columns where needed (`created_at`, `updated_at`, `created_by`); soft-deleted rows excluded by default
- Dates stored in UTC
- Connection pooling (PgBouncer, ORM pool) sized to DB limits, especially with serverless functions
- **RLS enabled** on every table when clients query the DB directly or in shared-schema multi-tenancy; policies tested for each role; `FORCE ROW LEVEL SECURITY` where table owners must also obey it
- **DB accounts least privilege:** the app user cannot `DROP`/`ALTER`/`TRUNCATE`; migrations use a separate user; no superuser in the app
- DB not publicly accessible; connections use TLS; default DB credentials changed
- Migrations safe on large tables: expand–contract pattern, `CREATE INDEX CONCURRENTLY`, backfills in batches, no long locks
- Sequential IDs not exposed where enumeration matters (use UUIDv7/ULID for public IDs); authorization still checked either way
- Production data never copied to dev/test without masking; seed/test data never in production
- **When to scale the DB:**
  - First: indexes, query optimization, caching.
  - Then: **read replicas** for read-heavy load.
  - Then: **partitioning** for very large tables (logs, history by date).
  - Last: **sharding** only at very large scale; high complexity.
- Archiving old data; retention policies
- Automated backups, point-in-time recovery, tested restore

### 7. Caching
- **When to use caching:**
  - Data read often, changed rarely (settings, holidays, roles, lookups, dashboards)
  - Expensive computations or slow queries
  - Third-party API responses with rate limits
- **When NOT to cache:** data that must always be real-time accurate (balances, approvals) unless invalidation is reliable; low-traffic apps where DB is fast enough.
- **Cache layers:**
  - In-memory (per instance): small, single-server apps.
  - **Redis/Memcached:** shared cache across multiple instances; use Redis when you also need sessions, locks, rate limits, queues, pub/sub.
  - HTTP caching: `Cache-Control`, `ETag`.
  - **CDN** (Cloudflare, CloudFront): static assets, public files, images.
- **Strategies:** cache-aside (default), write-through, write-behind (rare).
- Clear TTLs and invalidation rules for every cached key
- Consistent key naming (`app:module:entity:id`)
- Cache stampede protection (locking, jitter on TTL)
- App still works if cache is down (graceful fallback)

### 8. Redis Usage Review
Check whether Redis is used, needed, or misused for:
- Caching
- Sessions and token blacklists
- Rate limiting
- Distributed locks (cron, payment, balance updates across instances)
- Job queues (BullMQ, Sidekiq, Celery, Laravel Queues)
- Pub/sub for real-time notifications
- Counters, leaderboards
- Redis persistence settings, memory limits, eviction policy, and high availability

### 9. Queues, Messaging & Event Streaming
- **When to use a job queue (BullMQ, Celery, Sidekiq, Laravel Queue, RabbitMQ):**
  - Emails, notifications, PDF/report generation, exports, image processing, imports
  - Anything slow (> ~500ms) that does not need an immediate response
  - Retryable work with external services
- **RabbitMQ / SQS:** reliable task distribution, routing, work queues between services.
- **Kafka (or Redpanda, Kinesis, Pulsar):** use only when you need:
  - Very high throughput event streams (thousands–millions of events/sec)
  - Event replay and long retention
  - Multiple independent consumers of the same events
  - Event sourcing, audit streams, real-time analytics, data pipelines, CDC
  - **Do not use Kafka** for simple background jobs or small apps; it adds heavy operational cost.
- Idempotent consumers; at-least-once delivery handled
- Retries with backoff; dead-letter queues
- Message schema versioning
- **Outbox pattern** to keep DB writes and published events consistent
- Ordering guarantees where required
- Queue monitoring (lag, failures, throughput)

### 10. Background Jobs & Scheduling
- Idempotent jobs; retries with limits; failure handling
- Duplicate cron prevention across instances (distributed lock or single scheduler)
- Explicit timezone for scheduled tasks
- Long jobs chunked and resumable
- Job status visible (dashboard or logs)

### 11. Search
- `LIKE '%term%'` acceptable for small data
- Database full-text search (PostgreSQL `tsvector`, MySQL FULLTEXT) for medium needs
- **Elasticsearch/OpenSearch/Meilisearch/Typesense** when: large data, fuzzy search, relevance ranking, faceted filters, autocomplete, log analytics
- Sync strategy between DB and search index

### 12. File Storage
- Object storage (S3, GCS, Azure Blob, MinIO) instead of local disk for scalable/multi-instance apps
- Private buckets with signed URLs
- CDN for public assets
- Lifecycle rules for old files
- Virus scanning for user uploads where needed

### 13. Error Handling & Resilience
- Central error handler; custom error classes
- No swallowed errors; async errors handled
- **Timeouts** on every external call and DB query
- **Retries with exponential backoff and jitter** (only for safe/idempotent operations)
- **Circuit breakers** for unstable dependencies
- Fallbacks and graceful degradation
- Bulkheads (isolate failures so one slow dependency doesn't take down everything)
- **Fail closed:** when an auth, permission, payment or validation check errors, the request is denied, not allowed (OWASP A10:2025)
- Unhandled promise rejections and uncaught exceptions logged and the process restarted cleanly by the supervisor
- Partial failures rolled back (transactions) so data is never left half-written
- Safe, clear user-facing messages; internal details only in logs

### 14. Concurrency & Consistency
- Race conditions on shared resources (balances, counters, approvals, stock)
- Optimistic vs pessimistic locking choice justified
- Distributed locks when running multiple instances
- Idempotency for duplicate requests
- Eventual consistency understood and communicated where async is used
- **Saga pattern** for multi-service transactions (if microservices)

### 15. Performance
- Response time targets defined (e.g., p95 < 300ms)
- Slow endpoints and queries identified and profiled
- Pagination everywhere (see API Design)
- **Tables and lists:** server-side pagination, filtering and sorting; never send all rows to the client; one query per page, not one per row; client virtualizes very long lists
- **No `await` / DB / HTTP call inside a loop.** Batch it, or run independent calls in parallel with a concurrency limit (`Promise.all` with p-limit, `asyncio.gather` with a semaphore)
- In-memory joins and lookups use maps/sets, not nested loops (O(n²))
- Large exports and reports run as background jobs, streamed to a file, and delivered by download link
- Response compression (gzip/brotli)
- Avoid blocking operations on the main thread/event loop (sync file I/O, heavy JSON, CPU work, sync crypto)
- Batch operations instead of loops of single queries
- Lazy loading vs eager loading chosen correctly
- Indexes support the queries behind every list, filter and sort
- HTTP keep-alive / connection reuse for outbound calls
- Hot read paths cached where justified (see Caching)
- p50, p95 and p99 latency tracked per endpoint; APM or profiling for slow paths
- Memory leaks and large in-memory processing avoided (use streams for large files/exports)

### 16. Scalability
- Stateless application servers (no local sessions/files)
- Horizontal scaling behind a load balancer
- Auto-scaling rules (CPU, memory, queue length)
- Separate scaling for API and workers
- Rate limiting and quotas per user/tenant
- Multi-tenancy strategy if serving multiple organizations (shared DB with tenant ID, schema per tenant, or DB per tenant)
- Capacity planning for 10x growth

### 17. Logging, Monitoring & Observability
- Structured JSON logs with request ID, user ID, timestamps
- Correct log levels; no sensitive data (see Security → Sensitive data in logs)
- **Security events logged and alerted** (OWASP A09:2025): failed and successful logins, MFA changes, password resets, permission denials, admin actions, rate-limit hits, webhook signature failures
- Audit logs append-only and tamper-resistant, with retention defined
- Server clocks synced (NTP) so logs and token expiry line up
- Centralized logs (ELK, Loki, CloudWatch, Datadog)
- **Metrics:** latency, error rate, throughput, saturation (Prometheus + Grafana, Datadog)
- **Distributed tracing** (OpenTelemetry, Jaeger) for multi-service systems
- Error tracking (Sentry)
- Health checks: liveness and readiness
- Alerts with clear thresholds and on-call ownership
- SLIs/SLOs defined for critical flows
- Audit trail for critical business actions

### 18. Configuration & Environments
- Separate dev/staging/production
- Env variables validated at startup (fail fast)
- `.env.example` complete
- Debug off in production; source maps, stack traces and dev tools not exposed
- Secure defaults: a missing setting fails closed, not open (e.g., missing CORS list ≠ allow all, missing JWT secret ≠ default secret)
- No default credentials in config files or Docker images
- Separate secrets and third-party accounts per environment; production secrets not usable from dev
- Feature flags for risky releases
- Staging mirrors production as closely as possible

### 19. Code Quality & Maintainability
- Consistent naming and structure
- Linting/formatting enforced in CI
- No duplication, hard-coded values, dead code, debug logs
- Type safety where supported
- Small, reviewable functions and modules
- Meaningful comments (why, not what)
- Technical debt tracked
- Code review process

### 20. Testing
- Unit tests for business logic
- Integration tests for endpoints and DB
- Contract tests between services (if microservices)
- End-to-end tests for critical flows
- Load/performance tests for critical endpoints
- Regression tests for fixed bugs
- Separate test DB; mocks for external services
- Run existing tests; record results and coverage

### 21. CI/CD & Deployment
- CI: lint, type check, tests, security scan, build
- CI security gates: secret scanning, SAST, dependency audit, container image scan; Critical/High findings block the merge
- Protected main branch, required reviews and passing checks before merge
- CI actions pinned to a commit SHA; CI secrets scoped per environment; production deploy needs approval
- Production builds exclude dev dependencies, test routes and public source maps
- Automated, safe migrations
- Zero-downtime deployments (rolling, blue-green, canary)
- Rollback plan
- Graceful shutdown
- Docker images small and secure; non-root user
- Kubernetes/orchestration only when scale and team justify it
- Infrastructure as Code (Terraform, Pulumi) for repeatable environments
- Deployment documentation

### 22. Reliability & Disaster Recovery
- Backups automated and restore tested
- RPO (acceptable data loss) and RTO (acceptable downtime) defined
- No single points of failure for critical components
- Multi-AZ/replicas for DB and cache where needed
- Incident response process and postmortems

### 23. Data Privacy & Compliance
- Only necessary personal data collected/returned
- Sensitive data masked in responses and logs
- Retention and deletion rules
- Encryption at rest where needed
- Access to personal data restricted and audited
- Inventory of personal data: what is stored, where, why, and who can access it
- Users can export and delete their data where law requires it; deletion reaches backups, search indexes, caches and third parties within a defined time
- **Payments:** card data never touches or is stored on the server (use Stripe Elements/Checkout or another tokenizing provider) to stay in the lightest PCI DSS scope
- Third-party processors (email, analytics, AI, error tracking) receive only the data they need
- Applicable regulations considered (GDPR, local data laws, labor/HR data rules, HIPAA or similar for health data)

### 24. Cost Awareness
- Infrastructure cost appropriate for current scale
- No over-provisioned or unused services
- Heavy tools (Kafka, Kubernetes, Elasticsearch) justified by real needs
- Expensive queries, logs, or storage growth monitored

### 25. Documentation & Knowledge Sharing
- README: setup, env vars, run, test, deploy
- API docs for every endpoint
- Architecture diagram
- **Architecture Decision Records (ADRs)** for major choices
- Business rules documented
- Runbooks for common incidents
- Onboarding guide for new developers

---

## Step 4: Technology Decision Matrix
Add a section in the report evaluating each technology for **this** project:

| Technology | Currently Used? | Needed Now? | Needed at 10x Scale? | Reason | Recommendation |
|------------|-----------------|-------------|----------------------|--------|----------------|
| Redis (cache/sessions/locks) | | | | | |
| Job Queue (BullMQ/Celery/etc.) | | | | | |
| RabbitMQ / SQS | | | | | |
| Kafka / Event Streaming | | | | | |
| Elasticsearch / Search Engine | | | | | |
| CDN | | | | | |
| Object Storage (S3, etc.) | | | | | |
| Read Replicas | | | | | |
| DB Partitioning / Sharding | | | | | |
| WebSockets / SSE | | | | | |
| GraphQL / gRPC | | | | | |
| Microservices | | | | | |
| Docker | | | | | |
| Kubernetes | | | | | |
| Centralized Logging | | | | | |
| Metrics & Tracing | | | | | |
| Error Tracking (Sentry) | | | | | |
| Secret Manager | | | | | |
| Rate Limiter (shared store) | | | | | |
| WAF / DDoS Protection | | | | | |
| SAST / Secret / Dependency Scanning | | | | | |
| Feature Flags | | | | | |
| Infrastructure as Code | | | | | |

Rules for this matrix:
- Recommend the **simplest solution that works** for the current scale.
- Clearly state the **trigger point** for adopting each tool later (e.g., "Add Redis cache when dashboard queries exceed 500ms or app runs on more than one instance").
- Mention the operational cost and complexity of each recommendation.

## Step 5: Final Report Structure
Complete `Backend-Consideration-Report.md` in this order:

1. **Header** – project name, branch, review date
2. **Executive Summary**
   - Overall backend health score (0–100 or A–F) with reasoning
   - Top 5 critical gaps
   - Production-readiness verdict: Ready / Ready with fixes / Not ready
   - Scalability verdict: how far the current design can scale
3. **Project Overview & Scale Profile**
4. **Scorecard Table**
   | Area | Done | Partial | Missing | Not Needed | Score | Status |
   |------|------|---------|---------|------------|-------|--------|
5. **What Is Done Well**
6. **Detailed Review by Area** (all 25 areas)
7. **Technology Decision Matrix**
8. **Security Standards Coverage**: a table for OWASP Top 10:2025 (A01 Broken Access Control, A02 Security Misconfiguration, A03 Software Supply Chain Failures, A04 Cryptographic Failures, A05 Injection, A06 Insecure Design, A07 Authentication Failures, A08 Software or Data Integrity Failures, A09 Logging & Alerting Failures, A10 Mishandling of Exceptional Conditions) and OWASP API Security Top 10 2023 (API1 BOLA, API2 Broken Authentication, API3 Broken Object Property Level Authorization, API4 Unrestricted Resource Consumption, API5 Broken Function Level Authorization, API6 Unrestricted Access to Sensitive Business Flows, API7 SSRF, API8 Security Misconfiguration, API9 Improper Inventory Management, API10 Unsafe Consumption of APIs)
    | Standard | Item | Status (✅ ⚠️ ❌ ➖) | Related Issue IDs |
    |----------|------|---------------------|-------------------|
9. **What Is Missing** – all ❌ items
10. **What Needs Improvement** – all ⚠️ items
11. **Over-Engineering Found** – anything unnecessarily complex for the current scale
12. **Issues Table**
    | ID | Title | Area | Severity | Location | Impact | Effort (S/M/L) | Priority |
    |----|-------|------|----------|----------|--------|----------------|----------|
13. **Detailed Issues**
    ```
    ### [SEVERITY] ID – Title
    - Area:
    - Location: file:line
    - Current State:
    - Problem / Risk:
    - Recommended Fix: (code snippet for this stack)
    - Alternatives Considered:
    - Effort: Small / Medium / Large
    - Priority: P0 / P1 / P2 / P3
    ```
14. **Next Steps / Action Plan (Roadmap)**
    - **Immediate (P0 – before next deployment):** security holes, data loss, crash risks
    - **Short Term (P1 – 1–2 weeks):** reliability, correctness, critical performance
    - **Medium Term (P2 – 1–2 months):** caching, queues, monitoring, testing, documentation
    - **Long Term (P3 – scale stage):** read replicas, search engine, event streaming, service extraction — each with its trigger point
    Every step must be an actionable task linked to an issue ID.
15. **Architecture Recommendations** – current vs recommended architecture (text diagram)
16. **Risks If Nothing Is Changed**
17. **Questions & Assumptions** – anything that needs confirmation from the team

Severity: **Critical, High, Medium, Low, Info.**
Priority: **P0 (urgent), P1 (high), P2 (medium), P3 (low).**

## Rules
- Always work in the `njr` branch.
- Create `Backend-Consideration-Report.md` before reviewing anything.
- Update the report after each area; every area must have its results recorded.
- Do not modify application code. Only review and recommend. Ask before making any change.
- Do not invent findings. Every finding must reference real code (file:line). Mark unconfirmed items as **Needs Verification**.
- Never recommend a tool just because it is popular. Justify every recommendation with the scale profile, and flag over-engineering as clearly as missing features.
- Recommendations must match the project's stack, team size, and budget.
- If the project is large, review module by module and keep updating the report.
- The only file created or changed by this task must be `Backend-Consideration-Report.md`. Confirm with `git status` at the end.
