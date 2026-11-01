---
type: playbook
read_when: You are about to write or change code for a feature or improvement.
then: verification.md
---

# Do the task

Build the smallest change that fully meets the brief from `task-brief.md`, in the style of the code around it.

## Step 0: Create the report file (when needed)

Create `Implementation-Report.md` when the task is Large or runs across more than one session. Skip it otherwise.

Before doing anything else:
1. Check whether `Implementation-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it exists from an earlier task, keep anything still open, clear the rest and start fresh. If it belongs to this
   task, carry on in it.
4. Add the date, project name, branch/commit, and a one-line summary of the task at the top.

Write the results of **every step** into it as each step is completed. Do not wait until the end. Record: the brief, a plan table (ID | File | Change | Risk | Tests Needed), changes per milestone, anything that differed from the plan, and the result.

If this task already has a report from another playbook, add a section there instead of creating a second file. The rules
for reports are in `workflow.md`.

## Step 1: Look before you write

Before creating anything, search the project for it. The most common waste in generated code is rewriting something
that already lives a few files away.

- Is there a helper, hook, service, component or type that does this?
- How did the project solve the closest similar problem? Open that code and follow its shape.
- Check `architecture.md` for where this kind of code belongs.

## Step 2: Choose the simplest thing that works

Stop at the first option that holds:

1. Does this need to exist at all?
2. Does the project already have it?
3. Does the language's standard library do it?
4. Does the platform do it? For example, a database constraint, a native HTML input or plain CSS.
5. Does a dependency that is already installed do it?
6. Only then, write new code, as little as works.

Never trim input validation, error handling that protects data, security checks or accessibility to get a smaller
change.

Do not add an abstraction for a single use, a config value that never changes, or code for a future nobody has asked
for. Do add what the brief needs, in full. A smaller change that leaves out part of the request is not simpler, it is
unfinished.

## Step 3: Plan the order

Write the list of files you will touch and the order you will touch them. Build from the inside out, so that each layer
can be tested against the one below:

1. Data: migration, schema, types. Read `risky-changes.md` first.
2. Logic: services, domain rules, permissions.
3. Interface: API route, validation, response shape.
4. UI: data hook, component, states, then styling.
5. Tests, written alongside each layer rather than at the end.

For a Large task, split the list into milestones. Each milestone must pass the check commands and leave the product
working, because each one gets its own commit. Prefer one thin slice that works end to end, then widen it.

## Step 4: Build in small steps

- Change one thing, then run the fastest relevant check. Do not stack up ten changes before running anything.
- Follow `language.md` for the stack, and the existing code where the two differ.
- Match the surrounding naming, formatting, error handling and file layout.
- For any UI, handle the loading, empty and error states, and check `laws-of-ux.md`. If no design exists, use
  `Frontend-Design-Build.md`.
- Comment only on why something is done, when the code cannot show it. Do not narrate what the code does.
- Remove anything your change made unused, including imports, old helpers and dead branches.

## Step 5: Stay in scope

Every line in the diff should trace back to the brief.

| You notice | Do this |
|---|---|
| A bug in the code you are changing that blocks the task | Fix it and mention it in your report |
| A bug elsewhere | Leave it. Add it to **Next** in `progress.md` and mention it in your report. |
| Ugly code nearby | Leave it, unless you are already changing that exact code. Add it to `suggestion.md` if it matters. |
| A security problem anywhere | Follow "If you find a real vulnerability" in `secure-coding.md` |
| The brief was wrong | Update the brief, say so, and carry on if the goal still holds |

## When reality differs from the plan

- **The code is not what the prompt described.** Believe the code. Say what you found. If the task still makes sense,
  continue. If not, stop and ask.
- **Tests fail before you touched anything.** Record this as the baseline in your report. Do not fix or hide them unless
  they block you.
- **The change is much bigger than expected.** Find a smaller way to reach the goal. If there is none, tell the owner
  the real size before going further.
- **The tool or library behaves unexpectedly.** Read its real source or current docs. Do not code from what you remember
  about an API, because versions change.
- **You are guessing at a function or package name.** Stop and look it up. Invented names are a common failure in
  generated code.

## Finished means

The brief's **Done when** items all hold and the code matches the project. Now go to `verification.md`.
