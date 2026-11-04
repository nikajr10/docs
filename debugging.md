---
type: playbook
read_when: The task is a bug, crash, failing test, regression, or behaviour that looks wrong.
then: verification.md
---

# Fix a bug

A bug report names a symptom. Your job is to find the cause. A fix you cannot explain is a guess, and a guess that
happens to work comes back later.

## Step 0: Create the report file (when needed)

Create `Debugging-Report.md` when the cause was not obvious, it took more than a few attempts, or the bug touched data, money or security. Skip it otherwise.

Before doing anything else:
1. Check whether `Debugging-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it exists from an earlier run, clear it and write this run's report and findings into the same file. If it
   belongs to the run still in progress, carry on in it. Never create a second, dated or numbered report file.
4. Add the date, project name, branch/commit, and a one-line summary of the task at the top.

Write the results of **every step** into it as each step is completed. Do not wait until the end. Record: the reproduction, the evidence, the cause in one sentence, every affected caller, the fix and the proof.

If this task already has a report from another playbook, add a section there instead of creating a second file. The rules
for reports are in `workflow.md`.

## Step 1: Reproduce it

Make the bug happen yourself before you touch any code. Use the real path: run the app, call the endpoint, or write a
failing test.

- If it reproduces, keep that exact command or steps. They become your proof.
- If it will not reproduce, compare what differs: data, role, browser, timezone, environment, order of actions. Check
  whether it was already fixed. Do not change code on a hunch. If you still cannot reproduce it, report what you tried
  and ask for one specific detail.

## Step 2: Gather evidence

- Read the full error and stack trace, from the first line. The first error usually matters and the rest often follow
  from it.
- Read the logs around the failure.
- Check `git log` on the affected files. If it used to work, find the change that broke it. `git bisect` is worth using
  when the commit is not obvious.
- Look at the real data, on a local database only.

## Step 3: Trace to the cause

Follow the value or the flow backwards, from where it fails to where it first went wrong. The place that throws is often
not the place that is broken.

Write the cause as one sentence you could defend: "`X` happens because `Y` passes `Z` when `W`". If you cannot, you have
not finished this step.

Test one idea at a time. Add a log or an assertion, run it, and look. Remove temporary logging afterwards.

## Step 4: Find every place it applies

Before you edit, search for everything that calls the broken code and every place that copies the same pattern.

- If several callers are affected, fix the shared code once. One guard in the shared function is a smaller and safer
  change than a guard in every caller.
- Input from outside is different. If a request can leave a value out, check it at the boundary, as in
  `secure-coding.md`, and keep the shared code strict. A guard deep inside can stop the crash and still let bad data in.
- If the ticket names one path and three others have the same flaw, fix all of them. The owner reported one symptom,
  not one bug. If a fix would need the "ask the owner first" column of `risky-changes.md`, ask about that one.

## Step 5: Fix it

- Write the test first when you can, and watch it fail for the right reason.
- Change as little as fixes the cause. Do not refactor at the same time.
- Do not patch the symptom. Do not add a null check to hide a value that should never be null. Find out why it is null.
- Do not loosen a type, disable a test, widen a catch, add a retry or add a timeout to make the failure go away, unless
  that really is the correct fix and you can say why.

## Step 6: Prove it

1. The original reproduction no longer fails.
2. The new test passes, and it failed before the fix.
3. The check commands pass.
4. Nearby behaviour still works. See `verification.md`.

## Step 7: Record

- Say the cause, the fix and how you proved it in your report.
- If this bug could easily recur or cost real time, add it to `lessons.md`.

## Common traps

| Symptom | Often really is |
|---|---|
| Works locally, fails in staging | Env variable, build-time versus run-time config, case-sensitive file paths |
| Fails sometimes | Race condition, missing `await`, shared state, test order, timezone or clock |
| Works for admin, fails for others | Permission check, or a query that filters by role |
| Wrong number | Floating-point money, timezone boundary, double-counting from a join |
| UI shows old data | Cache, stale query key, missing invalidation |
| Fails only with real data | Null or empty values, unicode, large lists, old records from before a migration |
| Fix did nothing | Wrong file, old build, server not restarted, cached output. Prove your code is running. |
| Passes alone, fails in the suite | Test isolation: shared database rows, mocks or globals left behind |

## Special cases

- **Flaky test.** Do not re-run until green. Run it repeatedly to get the failure rate, then find the cause. Flakiness
  often points to a real race.
- **Slow code.** Measure first. Find the actual slow step with a profiler, query plan or timing, then fix that. See
  `optimization.md` for repo-wide work.
- **Production problem.** See `release.md`. Do not connect to production.
