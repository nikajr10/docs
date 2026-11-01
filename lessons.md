---
type: state
read_when: Every session, and whenever the owner corrects you or says "remember".
then: Match the owner's prompt in index.md.
---

# Lessons

This file is how the project gets better over time. The owner should never have to give the same correction twice. A
rule here applies to every future session and outranks every generic playbook.

## When to add an entry

- The owner corrected you, or said "remember", "always" or "never".
- The owner confirmed a non-obvious approach you should keep using.
- A mistake cost real time, or a production problem happened.
- You found a trap in this project that the code does not show.

Add it straight away, before you carry on with the task.

**Do not add** one-off instructions for this task, things the code or `architecture.md` already says, or general
programming knowledge.

## Rules

- Write the rule, not the story. It has to work for an agent who did not see the conversation.
- Before adding, look for an existing entry on the topic, and update it instead of adding a near-duplicate.
- Number in order, and do not reuse numbers.
- Delete a lesson when it stops being true. Stale rules are worse than none.
- If a lesson conflicts with a newer instruction from the owner, the newer one wins. Update the lesson.
- If existing code breaks a new rule, new code and any line you change follow the rule at once. The rest goes in **Next**
  in `progress.md`, unless the owner says to fix it now.
- Never write secrets or personal data here.

## Format

```markdown
## L-<number>: <the rule, in a few words>

**Rule:** <what to do or not do>
**Why:** <what went wrong, or what the owner said>
**Applies when:** <the situation that should trigger this>
```

## Example

```markdown
## L-003: Staff see local time, the database stores UTC

**Rule:** Convert booking times to Asia/Kathmandu in the UI only. Never in queries or the API.
**Why:** A report showed bookings on the wrong day. The owner flagged it twice.
**Applies when:** Any code displays or filters by date.
```

## Log

None yet.
