---
type: playbook
read_when: A new task arrives, or a prompt is short, vague or could mean several things.
then: implementation.md, or debugging.md for a bug.
---

# Explain the task to yourself

The owner writes short prompts on purpose. Your job is to turn a short prompt into a clear task before you write code.
Most wrong work comes from solving the wrong problem well. This step prevents that.

## Step 1: Read it literally

Separate what the prompt actually says from what you assume. Note every noun: a screen, a role, a field, a word from the
domain. Look each one up in `overview.md` and in the code. A word the owner uses always refers to something real
in this project, so find it.

## Step 2: Find the real goal

Ask what the owner is trying to achieve, and who benefits. A prompt usually names a solution. If the solution would not
reach the goal, say so.

Check for what the prompt leaves out but the goal needs: empty states, errors, permissions, mobile layout, existing data,
and other screens that show the same thing.

## Step 3: Check it against the project

- `project-description.md` and `phases.md`: does this fit what we are doing, and does it belong to a phase?
- `decision.md`: does this reverse an earlier choice?
- `lessons.md`: is there a standing rule about this?
- `progress.md`: has this been started or blocked already?
- The code: does it already exist, partly or fully? Is the owner's description of the current behaviour right?

## Step 4: Decide what done means

Write acceptance criteria the owner could check by looking at the product. Each one must be testable. "Better" is not
testable. "Loads in under 2 seconds on the bookings page with 10,000 rows" is.

If the prompt gives no result, work out the obvious one yourself. Ask only if a wrong guess would waste real work.

## Step 5: Fence the scope

List what you will not do. Things you notice but will not change go in your report, not in the diff. Security problems
follow `secure-coding.md`.

## Step 6: Handle the unknowns

For each unknown, in this order:

1. Can the code, the data or a quick test answer it? Then find out.
2. Is there a common default and is it easy to change later? Then assume it, and write down the assumption.
3. Would a wrong guess waste real work or be hard to undo? Then stop and ask, following `workflow.md`.

## The brief

For a Medium task, put this in your reply, in a few lines, before you start building. For a Large task, put it in `progress.md`. For a Small
task, keep it in your head.

```markdown
**Goal:** <the outcome, and who it is for>
**Done when:**
- <testable result>
- <testable result>
**Not in scope:** <what you will leave alone>
**Assumptions:** <what you decided without asking>
**Risk:** <security, data or breaking changes; "none" is a valid answer>
```

Do not wait for approval of the brief unless the owner asked for a plan first. Write it, then carry on.

## Reading common vague prompts

| The owner says | Find out | Usually means |
|---|---|---|
| "Fix the dashboard" | What is wrong now. Run it and look. | One visible bug or a broken flow, not a redesign |
| "It's slow" | Which action, and how slow. Measure it. | One slow query or a heavy page |
| "Make it better" | What would a user complain about? | Use `professional.md` to find what matters |
| "Clean this up" | Which part, and why now? | Readability with no behaviour change |
| "Add auth" | Who logs in, and what can each role do? | A full flow, including `secure-coding.md` |
| "Same as X" | Read X closely. | Reuse its pattern and components exactly |
| "Make it work on mobile" | Which pages, and at what widths? | Check every page the change affects |
| "Why is this happening?" | The answer, with evidence. | An explanation. Do not change code unless asked. |
| "Plan this" | The design and its steps. | A plan only. No code until the owner agrees. |

## Questions versus tasks

If the prompt is a question, answer it. Do not change code because of a question. Read what you need so that the answer
is correct, and offer the change in one line if one is obvious.

## Worked example

**Prompt:** `add rate limiting to login`

**Reading it:** The code has `POST /auth/login` and also `POST /auth/otp/verify`. The real goal is to stop password
guessing, and the OTP route has the same weakness, so leaving it open would not reach the goal.

```markdown
**Goal:** Stop password and OTP guessing against any account.
**Done when:**
- 6th failed attempt within 15 minutes gets a 429 with a clear message.
- The limit applies per account and per IP, so rotating IPs does not bypass it.
- A successful login resets the count.
- Tests cover the limit, the reset and the bypass attempt.
**Not in scope:** Signup throttling, CAPTCHA.
**Assumptions:** 5 attempts per 15 minutes, using the Redis instance the project already has.
**Risk:** Could lock out real users. Limits sit in config so they can be tuned.
```
