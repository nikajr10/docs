---
type: state
read_when: Every session, and whenever the prompt is `continue`.
then: lessons.md
---

# Progress

This file is the project's short-term memory, and what lets a new session carry on as if nothing stopped. Write it for a
reader who knows nothing about the last session.

## Rules

- Update it in the same commit as the work.
- **Now** and **Next** must always reflect the truth. Replace old content. Do not let it pile up.
- Keep **Log** to the last 15 entries, and delete older ones. Git history keeps them.
- `continue` means: pick up **Handoff** if it has content, then finish **Now**. If both are empty, start the top item in
  **Next** that is not blocked. If **Next** is empty too, take the next open task in the current phase of `phases.md`.
  Do one item, then report and stop, unless the owner says to do more.

## Now

<!-- What is in progress. For a Large task, put the brief and plan here. -->

Nothing in progress.

## Next

<!-- Order: anything exposing data or accounts right now, the owner's requests, other security work, then other bugs.
     Ideas go in `suggestion.md`. -->

None yet.

## Blocked

<!-- What is stuck, what it is waiting for, and who must act. -->

Nothing blocked.

## Plan

<!-- For a Large task, use this shape. Delete it when the task ends.

**Goal:** <the outcome>
- [x] Milestone 1: <result>
- [ ] Milestone 2: <result>
- [ ] Milestone 3: <result>
-->

## Notes for next release

<!-- Migrations, new env variable names, deploy order and manual steps. `release.md` reads this. -->

None yet.

## Check results

<!-- The latest state of the check commands. -->

| Check | Result | Date |
|---|---|---|
| Lint | Not run | |
| Type check | Not run | |
| Tests | Not run | |
| Build | Not run | |

## Log

<!-- Newest first. One line for each milestone. Format:
- YYYY-MM-DD: <what changed>. Checked: <what you ran>. -->

None yet.

## Handoff

<!-- Fill this in when a session ends with work unfinished. Clear it once picked up.

**Stopped at:** <the exact point>
**Tried so far:** <what worked and what did not>
**Do next:** <the first concrete step>
**Watch out for:** <anything non-obvious>
-->
