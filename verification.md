---
type: playbook
read_when: You have finished a change and need to prove it works, or the owner asks about testing.
then: workflow.md step 7 (Record)
---

# Prove it works

The owner is not going to test this for you. Passing the build shows the code compiles, not that it works. Done means
you saw the behaviour work, and you can show how.

## Step 0: Create the report file (when needed)

Create `Verification-Report.md` when the task is Large or risky, or the owner asks whether it works. Skip it otherwise.

Before doing anything else:
1. Check whether `Verification-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it exists from an earlier run, clear it and write this run's report and findings into the same file. If it
   belongs to the run still in progress, carry on in it. Never create a second, dated or numbered report file.
4. Add the date, project name, branch/commit, and a one-line summary of the task at the top.

Write the results of **every step** into it as each step is completed. Do not wait until the end. Record: the baseline, each command and its result, what you exercised, the diff review and the definition of done.

If this task already has a report from another playbook, add a section there instead of creating a second file. The rules
for reports are in `workflow.md`.

## Step 1: Run the check commands

Run all the check commands from `overview.md`. They must pass.

If they already failed before your change, compare against that baseline and report it. You are responsible for not
adding failures, and for saying clearly which ones already existed.

## Step 2: Exercise the change

Run the thing itself. Pick the rows that apply:

| You changed | How to prove it |
|---|---|
| API endpoint | Call it with a real request. Check success, invalid input, no auth and the wrong role. |
| Business logic | Unit test with real cases and edge cases, including the boundary values |
| Database | Run the migration on a scratch database, check the result, then run the rollback. See `risky-changes.md`. |
| UI | Open it in a browser at phone and desktop widths, in both themes, as each role that sees it. Use webapp-testing if it is installed. |
| Background job or webhook | Trigger it. Run it twice to check that repeats are safe. |
| Script or CLI | Run it, including with missing input |
| Config or env | Start the app with it, and with it missing |
| Integration | Use the sandbox or a mock. Check the failure path, not only success. |
| Bug fix | The original reproduction, as in `debugging.md` |
| Refactor | Same tests pass before and after, with no behaviour change |

Then check what could have broken: other callers of what you changed, and other screens that use the same data.

If you cannot run something, say so and mark that part **Needs Verification**. Never imply you checked it.

## Step 3: Write the tests that matter

Leave behind the smallest set of tests that would fail if this logic broke.

**Must have a test:** money, permissions, data changes, parsing, branches with business rules, and every bug fix.

**Does not need one:** trivial getters, framework behaviour, and config that has no logic.

- Test behaviour through the public interface, not private details.
- Use the project's existing test framework and patterns. Do not add a new one.
- A test must be able to fail. If you are unsure, break the code briefly and watch it go red.
- Do not mock the thing you are testing. Mock external services at the edge, and prefer a real test database.
- Cover the failure path: invalid input, no permission, not found, a duplicate, an empty list.
- Never change or delete a test only to make it pass. If a test is wrong, say why in your report.

## Step 4: Review your own diff

Read `git diff` as if someone else wrote it and you have to approve it. If they are installed, also run `/security-review`
before committing code, and Code Review before finishing a Medium or Large task. They add to this step and do not replace it.

**Correctness**

- Does every line trace back to the brief?
- Are the error paths handled, and do they return something useful?
- Are nulls, empty lists, zero and concurrent requests handled?
- Are all callers of anything you changed still correct?

**Security** (see `secure-coding.md` for sensitive areas)

- Does anything trust the client that it should not?
- Are permission checks on the server, for this specific record?
- Has any secret or personal data reached the code, logs or responses?

**Clean-up**

- No servers or background processes left running, and no temp files left behind.
- No debug logs, commented-out code or leftover TODOs.
- No unused imports, files or helpers.
- No unrelated formatting changes.
- No secrets, `.env` files, build output or scratch files staged.

**Fit**

- Does it look like the rest of the codebase?
- Could the next developer or agent understand it without you?

Fix what you find, then re-run the check commands.

## Definition of done

Every item must be true, or be called out plainly in your report:

- [ ] Every **Done when** item from the brief holds
- [ ] Check commands pass, or failures are recorded as existing before your change
- [ ] You exercised the change itself, not only the build
- [ ] Tests cover the risky logic, and fail if it breaks
- [ ] You read your own diff
- [ ] `secure-coding.md` was followed if the change is sensitive
- [ ] `risky-changes.md` was followed if the change is risky
- [ ] Project files are updated, as listed in `workflow.md` step 7
- [ ] `suggestion.md` is updated, or empty if there are no suggestions
- [ ] Your report says what you checked and how

## When a full audit fits

These are large, and run only when the owner asks. Add one to `suggestion.md` if it seems due:

| Situation | Audit |
|---|---|
| Before launch, or after large auth changes | `security.md`, `API-Security.md` |
| A public API or heavy traffic is coming | `System-Test-Simulation.md`, `Backend-Consideration.md` |
| The codebase has become hard to change | `code-quality.md`, `optimization.md` |
