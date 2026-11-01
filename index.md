---
type: index
read_when: Always. This is the entry point for every session and every agent.
then: agent.md
---

# Docs index

This folder tells any coding agent how to work in this project. The owner writes prompts and does not touch the
keyboard otherwise. You read, decide, build, check, record and report.

All paths in these files are relative to this folder, unless they say "project root". The project root is the folder
that holds this one.

## Start of every session

1. Read `agent.md` (hard rules) and `quality.md` (quality bar).
2. Read `project-description.md` and `overview.md`. If the front matter of `overview.md` says `status: template`, stop and run `setup.md` first, then come back to
   the owner's prompt.
3. Read `progress.md` and `lessons.md`.
4. Match the owner's prompt to the table below. Read only the files that row names.
5. Follow `workflow.md` from step 1.

Do not read the whole folder. Audits and standards are long, and reading them when they do not apply wastes context.
Read `architecture.md` and `decision.md` when the task touches code or a design choice, which is most
tasks.

## Route the prompt

| The prompt is about | Read | Writes to |
|---|---|---|
| Setting up these docs in a project | `setup.md` | The project files, `Setup-Report.md` |
| `go`, "review my prompt", or `prompt.md` | `prompt.md`, then `prompt-review.md` | **Reviewed prompt** in `prompt-review.md` |
| `continue`, "what's next", no clear task | `progress.md`, then `workflow.md` | `progress.md` |
| A new feature or change | `task-brief.md`, `implementation.md` | Code, project files, `Implementation-Report.md` when needed |
| A vague idea, or a Large task whose best approach is unclear | `task-brief.md`, then `professional.md` | `professional-report.md` |
| A bug, crash, failing test, wrong behaviour | `debugging.md` | Code, test, `Debugging-Report.md` when needed |
| Writing code in a stack | `language.md`: Shared Standards, that stack's section, Final Checklist | Nothing extra |
| Any visible UI change | `laws-of-ux.md`: At a glance and Checklist | Nothing extra |
| A UI with no design supplied | `Frontend-Design-Build.md` | `Frontend-Design-Report.md` |
| Auth, user input, secrets, payments, uploads, permissions | `secure-coding.md` | Code, `Secure-Coding-Report.md` when needed |
| Database change, public API change, new dependency, deleting or moving a lot | `risky-changes.md` | `decision.md`, `Risky-Changes-Report.md` when needed |
| Testing, "does it work", finishing a change | `verification.md` | `progress.md`, `Verification-Report.md` when needed |
| Choosing effort, or a task got harder or easier than expected | `effort.md` | Nothing extra |
| Deploying, release notes, production problem | `release.md` | `progress.md`, `Release-Report.md` |
| Setting up plugins, or which plugin suits a job | `plugins-setup.md` | `Plugin-Setup-Report.md` for setup |
| A diagram, only when the owner asks for one | Diagram Rule in `plugins-setup.md` | `diagrams/` in the project root |
| What the project is, or a change of direction | `project-description.md` | `project-description.md` |
| The owner's plans, a roadmap, "make phases" | Phases in `workflow.md`, `project-description.md` | `phases.md` |
| "What can be better", or doing a suggestion | `suggestion.md`, and Suggestions in `workflow.md` | `suggestion.md` |
| "Remember this", or the owner corrects you | `lessons.md` | `lessons.md` |
| "Why did we do X" | `decision.md` | Nothing |
| Full security audit | `security.md` | `security-report.md` |
| Full API audit | `API-Security.md` | `API-Security-Report.md` |
| Full backend review | `Backend-Consideration.md` | `Backend-Consideration-Report.md` |
| Worst-case or load testing | `System-Test-Simulation.md` | `System-Test-Simulation-Report.md` |
| Repo-wide code review | `code-quality.md` | `Code-Quality-Report.md` |
| Repo-wide cleanup with no behaviour change | `optimization.md` | Code, final report in your reply |

If a prompt matches several rows, read all of them. If it matches none, use `task-brief.md`. When a row leads you to the
real task, as `continue` and `go` do, match that task against this table too.

**Audits run only when asked.** A normal task never starts a full audit on its own. If you think one is needed, add it
to `suggestion.md`.

## Which rule wins

When two files disagree, go down this list and stop at the first that decides it:

1. The owner's words in the current prompt.
2. `agent.md`.
3. `lessons.md`, the owner's standing corrections.
4. `decision.md`, the choices already made in this project.
5. The playbook or audit for the current task.
6. What the existing code already does. An existing project keeps its stack and style.
7. `language.md` and `laws-of-ux.md`.
8. Plugin defaults and plugin advice.

Two exceptions:

- A rule that protects production, secrets or user data always stands unless the owner lifts it in so many words, for
  that one time.
- If an audit says not to commit or not to change code, that holds for the whole audit, even though `agent.md` tells
  you to commit at milestones.

Fix the conflict you found by updating the lower-ranked file if it is a project file. If it is a generic file, mention
it in your final message.

## File types

Every file except `prompt.md`, `suggestion.md` and `phases.md` starts with front matter: `type`, `read_when` and `then` (where to go next).

| Type | Meaning | May you edit it? |
|---|---|---|
| `index` | This file | No |
| `rule` | Applies to every task | No |
| `playbook` | Steps for one kind of work. Writes a report file when needed. | No, except the **Reviewed prompt** section of `prompt-review.md` |
| `audit` | A full review. Always writes a report file. | No |
| `standard` | Reference you consult while working | No |
| `input` | `prompt.md`, the owner's raw prompt and nothing else. It may be empty. | No |
| `output` | `suggestion.md`, your open suggestions and nothing else. Empty when there are none. | **Yes. Update it after every task.** |
| `output` | `phases.md`, the phased plan. Empty until the owner asks for phases. | **Only when the owner asks, or to tick off finished work.** |
| `state` | The project files: `project-description.md`, `overview.md`, `architecture.md`, `decision.md`, `progress.md`, `lessons.md` | **Yes. You keep these current.** |

Only the project files hold facts about this project. Everything else is generic and shared between projects, so never
put project facts in it.

**This folder stays flat. Never create a folder inside it.** Report files and diagrams go in the project root, not here.

## Words used in these files

| Word | Meaning |
|---|---|
| **Owner** | The human who writes the prompts |
| **You** | The coding agent reading this |
| **Check commands** | The lint, type check, test and build commands listed in `overview.md`. Skip any marked `None`. |
| **Milestone** | Work that stands on its own and passes the check commands |
| **Report file** | A file in the project root recording one piece of work. `workflow.md` says when to create one. |
| **Your report** | Your final message to the owner |
| **Needs Verification** | The label for anything you could not confirm. Never present these as fact. |
| **Stop and ask** | End your turn with one clear question. Do not guess past it. |
