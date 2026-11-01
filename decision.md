---
type: state
read_when: Before changing a design or a major choice, or when someone asks why something is the way it is.
then: Return to the step of workflow.md you came from.
---

# Decisions

This is the record of why the project is the way it is. Code shows what was done, this file shows why, and what was
turned down. Read it so that you do not reverse a deliberate choice or repeat an abandoned approach.

## When to add an entry

**Add one when:**

- You chose between real options and the choice will be costly to change: a library, a data model, an auth approach, a
  structure.
- You deliberately took a shortcut, with a known limit.
- The owner made a product decision that is not obvious from the code.
- You rejected something a future agent would be tempted to try.
- The owner left a value or convention open, you chose one, and other code will follow it.

**Do not add one for** one-off naming, formatting, bug fixes or anything the code already makes obvious.

## Rules

- Add new entries at the top of the log. Number them in order and never reuse a number.
- Never rewrite an old decision. If it changes, add a new entry, and set the old one to `Replaced by D-<number>`.
- Before going against an `Active` decision, stop and ask. It may have been made for a reason you cannot see. You may
  change an `Inferred` one for a good reason, if you say so in your report.
- Use `Inferred` when you worked out a choice from the code and nobody confirmed why.
- Keep each entry short. A few honest lines are enough.

## Format

```markdown
## D-<number>: <the choice, as a statement>

**Date:** <YYYY-MM-DD>  **Status:** <Active / Inferred / Replaced by D-number>  **By:** <owner / agent>

**Context:** <the problem, and what forced a choice>
**Decision:** <what was chosen>
**Rejected:** <the other options, and why each lost>
**Consequences:** <what this makes easier and harder, and any limit to watch for>
**Revisit when:** <the condition that would change this>
```

## Example

```markdown
## D-002: Use Postgres full-text search, not Elasticsearch

**Date:** 2026-03-14  **Status:** Active  **By:** agent

**Context:** Staff need to search 20,000 bookings by name and reference.
**Decision:** A Postgres `tsvector` column with a GIN index.
**Rejected:** Elasticsearch: another service to run, for a dataset Postgres handles easily.
**Consequences:** No new infrastructure. Fuzzy search is limited.
**Revisit when:** Search passes 2M rows, or fuzzy matching becomes a real requirement.
```

## Log

<!-- Newest first. -->

None yet.
