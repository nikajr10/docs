---
type: state
read_when: A task touches code and you need to know where things live or how they connect.
then: Return to the step of workflow.md you came from.
---

# Architecture

<!-- Filled in by the agent during setup.md, and kept current by every change that alters structure.
     Describe what is true now, not the plan. Point to paths instead of pasting code, because pasted code goes stale. -->

## System map

```text
<Draw the moving parts and how they talk. For example:

Browser -> Next.js app -> NestJS API -> Postgres
                              |-> Redis (queue)
                              |-> Payment provider>
```

## Modules

| Module or folder | Job | Depends on |
|---|---|---|
| `<path>` | <what it owns> | <what it uses> |

## Main flows

Follow one important path through the system, such as a booking from click to database row.

1. <step, with file path>

## Data model

| Table or entity | Holds | Key relations |
|---|---|---|
| <name> | <what> | <links> |

**Rules the data must always follow:** <for example, a booking always has a user; totals equal the sum of items>

## Auth and permissions

- **Login:** <how a user proves who they are, and where that code is>
- **Permissions:** <where role and object checks live>
- **Public routes:** <which ones, and why>

## External services

| Service | Used for | Code | Failure behaviour |
|---|---|---|---|
| <name> | <purpose> | `<path>` | <what happens if it is down> |

## Background work

<Queues, cron jobs and webhooks: what triggers each, and where it lives. Write "None" if there are none.>

## Where new code goes

| To add | Put it in | Copy the pattern from |
|---|---|---|
| An API endpoint | `<path>` | `<example file>` |
| A page | `<path>` | `<example file>` |
| A database change | `<path>` | `<example file>` |
| A test | `<path>` | `<example file>` |

## Patterns to follow

<The conventions used across this codebase. Only list what a newcomer would get wrong.>

## Known weak spots

<Parts that are fragile, slow or due for change, and why.>
