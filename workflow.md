---
type: playbook
read_when: Every task. This is the main loop that the other playbooks plug into.
then: Wait for the next prompt.
---

# Workflow

The owner gives prompts and nothing else. Treat every prompt as: take this all the way to done and verified, then tell
me what happened. Do not hand work back that you can do yourself. Run the commands, read the logs, open the browser and
fix what fails.

## Step 0: Size the task

| Size | Signs | Run these steps |
|---|---|---|
| **Small** | One obvious change, no risky area, under about 30 lines | 1, 2, 5, 6, 7, 8, 9 |
| **Medium** | One feature or bug, several files | All. The brief goes in your reply. |
| **Large** | Several modules, new data model, unclear design, or more than one session | All. The brief and plan go in `progress.md`. |

A task can grow. If a Small task touches anything in Step 3, treat it as Medium.

If plugins are installed, use them as Phase 4 of `plugins-setup.md` says. They are optional, so never stop for a missing
one. Then set your effort level using `effort.md`, and change it whenever the work gets harder or easier. Also decide
whether the task needs a report file, using [Report files](#report-files) below.

## The loop

### 1. Understand the request

Use `task-brief.md`. Work out the real goal and what "done" means. For `continue`, follow the rule at the top of
`progress.md`, then treat the item you pick up as the task.

### 2. Understand the code

Read the code the change touches and follow the real flow end to end. Check `architecture.md` and
`decision.md` first so you do not undo an earlier choice. Never work from memory or from a summary when the
source is there to read.

### 3. Check the risk

| If the task touches | Read |
|---|---|
| Auth, input, secrets, permissions, files, payments, personal data | `secure-coding.md` |
| Database, public API, dependencies, config, deleting or moving a lot of code | `risky-changes.md` |

### 4. Plan

Use `implementation.md`. For a bug, `debugging.md` replaces this step and step 5. For a Medium task, a short list in your head or your reply is enough. For a Large task, write
the plan in `progress.md` as milestones, because that is what survives the end of a session.

### 5. Build

Use `implementation.md`, and `language.md` for the stack. For a bug, use `debugging.md` instead.

### 6. Verify

Use `verification.md`. Nothing is done until you have seen it work. Review your own diff before you call it finished.

### 7. Record

Update the project files in the same commit as the code, so that the docs can never lag behind:

| What happened | Update |
|---|---|
| Any task | `progress.md` and `suggestion.md` |
| Work from a phase was finished, or the plan changed | `phases.md` |
| The owner changed the project's direction | `project-description.md` |
| A real choice between options | `decision.md` |
| Structure, data model, modules or a new integration changed | `architecture.md` |
| Commands, environments or stack changed | `overview.md` |
| The owner corrected you, or a mistake cost real time | `lessons.md` |

### 8. Commit

Follow `agent.md`: at each milestone, on the working branch, never push.

### 9. Report

Use the format at the end of this file.

## Decide or ask

The owner's time is the scarcest thing in this system. Each question stops the work until they come back.

**Decide yourself, and state the decision in your report:**

- Naming, structure, internal patterns and which file something goes in.
- Which of two reasonable approaches to take, using the project's existing style.
- Details the owner did not specify, using the most common choice for this kind of product.
- Anything you can find out by reading the code, running it or searching.
- Anything easy to undo.

**Stop and ask only when:**

- The answer would change what you build, you cannot work it out, and a wrong guess wastes real work.
- The change is in the "ask the owner first" column of `risky-changes.md`. `continue` is not approval for these.
- It needs production access, a real credential, a payment or a login only the owner can do.
- The prompt conflicts with `decision.md` or `lessons.md` in a way that may not be intended.
- Two business rules conflict and the choice is the owner's.

When you ask, do everything that does not depend on the answer first. Then ask one specific question, give your
recommended answer, and say what you will do once they reply.

## When you get stuck

1. If the same approach has failed twice, stop repeating it. Change the approach or gather new evidence.
2. After three different failed approaches, stop. Write in your report what you tried, what you learned and your best
   next idea.
3. Never hide a failure. Do not disable a test, weaken a check, catch and ignore an error, or mark work done to get past
   a problem.
4. If a blocker affects one part of the task, finish the rest and report the blocked part.

## When the owner changes direction

- `Stop` means stop now. Leave the code in a state that builds, and say what is half done.
- A correction replaces the old instruction immediately. Add it to `lessons.md` if it applies beyond this task.
- Keep finished work unless the correction removes the need for it.

## Long tasks and handoffs

Assume that your context can end at any time and the next agent knows nothing. After each milestone, make sure
`progress.md` could brief a stranger. Whenever you end a turn with work unfinished, fill in its **Handoff**
section. If your tool can
run agents in parallel, use them for independent work such as separate modules, and review what they return before you
trust it.

## Phases

`phases.md` holds the phased plan for the whole project. It stays completely empty until the owner gives their plans and
asks for phases. Never create phases on your own, and never add them during setup.

`phases.md` is the whole route. `progress.md` says where you are on it. The plan for one Large task stays in `progress.md`.

**When the owner asks for phases:**

1. Read the owner's plans, `project-description.md`, `overview.md`, `architecture.md` and `decision.md`.
2. Split the work into phases, in dependency order. Each phase must leave the product working and be possible to check.
3. Keep every item from the owner's plans. Your own ideas go in `suggestion.md`.
4. Write `phases.md` using the format below.
5. Show the owner and stop. Start the work only when they say `go`, `continue` or name a phase.

**While working through phases:**

- Work in order, unless the owner says otherwise.
- Put the task in hand under **Now** in `progress.md`.
- Tick a task as soon as it is finished, in the same commit as the work.
- When every **Done when** line holds, set the phase to `Done` and the next one to `In progress`.
- If the owner changes the plan, rewrite the phases it affects, but never rewrite a `Done` phase.

Use this format:

```markdown
# Phases

**Goal:** <what the whole plan achieves>

## Phase 1: <name>

**Status:** <Not started / In progress / Done>
**Goal:** <what this phase delivers>
**Depends on:** <an earlier phase, or nothing>

- [ ] <task>
- [ ] <task>

**Done when:**
- <testable result>
```

## Suggestions

After every finished task, of every size, stop and ask what could be done better. Write the answer in `suggestion.md` in
this folder. Create the file if it is missing. It holds open suggestions and nothing else: no title, no notes, no front
matter.

**A suggestion can be:**

- A better way to build what you just worked on.
- Something that would make the product better for its users.
- Code or structure that makes future work slower or riskier.
- A missing test, document, tool or automation that would have helped.

**It is not:**

- A bug or a security problem. Those go in **Next** in `progress.md`, and in your report.
- Part of the current task. Finish that instead.
- General advice such as "add more tests". If it does not name a real place and a real change, leave it out.

**After every task:**

1. Read `suggestion.md`.
2. Remove anything that is done or no longer true.
3. Add what this task taught you, and merge any duplicates.
4. Put the most valuable first, and keep the ten best.
5. **If no real suggestion is left, leave the file completely empty.** No headings, no "none". Never invent a suggestion to
   fill it.

A suggestion is an idea, not approved work. Do not act on one until the owner asks, and `continue` never picks one up.
When the owner asks for one, run it as a normal task and remove it when it is done.

Use this format for each entry:

```markdown
## <short title>

**Where:** <the file, screen or area>
**Now:** <what is weak today>
**Better:** <what to do instead>
**Why it matters:** <the gain for users, safety, speed or cost>
**Size:** <Small / Medium / Large>
```

## Report files

A report file is the written record of a piece of work. It always goes in the project root, never in this folder. Audits
always write theirs. The playbooks below write one whenever it is necessary.

**Create a report file when:**

- The task is Large, or runs across more than one session.
- A bug took real investigation, or it touched data, money or security.
- The change is in the "ask the owner first" column of `risky-changes.md`.
- The change adds or alters login, permissions or payments, or you found a real vulnerability.
- You are preparing a release, running the launch gate or handling a production problem.
- The owner asks for one.

**Skip it for** Small tasks, questions and routine Medium tasks. Your reply is enough for those.

| Playbook | Report file |
|---|---|
| `setup.md` | `Setup-Report.md` (always) |
| `plugins-setup.md` | `Plugin-Setup-Report.md` (always) |
| `implementation.md` | `Implementation-Report.md` |
| `debugging.md` | `Debugging-Report.md` |
| `verification.md` | `Verification-Report.md` |
| `secure-coding.md` | `Secure-Coding-Report.md` |
| `risky-changes.md` | `Risky-Changes-Report.md` |
| `release.md` | `Release-Report.md` |

**Rules:**

- Create the report file first, before any other step.
- Update it after each step. Every step must have its results recorded.
- One playbook gets one report file, always with the name in the table. Each new run (iteration) clears that file and
  writes the new report and findings into it. Never create a second, dated or numbered report file.
- One task gets one report file. If a later playbook applies to the same task, add a section to the existing file.
- If you revisit a step, update its entry instead of adding a duplicate.
- Do not invent results. Mark anything unconfirmed as **Needs Verification**.
- Commit it with the work it describes. The exception is a report that lists unfixed security problems: leave that one
  uncommitted and tell the owner.
- Say in your final message which report file you wrote.

## Reporting to the owner

Write in plain, short sentences. Lead with the outcome, unless something is urgent. Use this format, and leave out any line with nothing to say.

```markdown
**Urgent:** <a security or data problem the owner must see first>
**Done:** <what now works, in one or two sentences>
**Changed:** <the main files or areas, only if useful>
**Checked:** <what you ran or looked at, and the result>
**Decided:** <choices you made that the owner may want to know about>
**Not done / risks:** <anything skipped, failing or uncertain>
**Suggestions:** <how many are open in `suggestion.md`>
**Needs you:** <only what the agent cannot do>
```

Report failures as plainly as successes. If tests fail, say so and show the output. If you did not check something, say
that. Never write "should work" about something you could have run.
