---
type: playbook
read_when: Once per project, when `overview.md` says `status: template` or the owner asks to set up these docs.
then: The owner's original prompt, if there was one. Otherwise wait for a task.
---

# Set up this folder in a project

This turns the generic folder into one that knows this project. Do it once. Do all of it yourself. The only thing the
owner should have to do is answer questions you cannot answer from the code.

## For the owner: install and update

Install, from the project root. If the project already has a `docs` folder, clone into another name such as `agent-docs`.

```bash
git clone --depth 1 https://github.com/nikajr10/docs.git docs && rm -rf docs/.git
```

Then give the agent this prompt: `Read docs/setup.md and do it.`

To update the generic rules later, run this. It adds any new files, and keeps the project files, `prompt.md`, `suggestion.md` and
`phases.md`, which belong to this project.

```bash
git clone --depth 1 https://github.com/nikajr10/docs.git /tmp/docs-new \
  && rsync -a --ignore-existing --exclude .git /tmp/docs-new/ docs/ \
  && rsync -a --exclude .git --exclude /prompt.md --exclude /suggestion.md --exclude /phases.md \
     --exclude /project-description.md --exclude /overview.md --exclude /architecture.md \
     --exclude /decision.md --exclude /progress.md --exclude /lessons.md /tmp/docs-new/ docs/ \
  && rm -rf /tmp/docs-new
```

Then commit the updated docs on their own, as one docs-only commit.

## Step 0: Create the report file

Create `Setup-Report.md` when you run this setup, which is always.

Before doing anything else:
1. Check whether `Setup-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it exists from an earlier run, clear it and write this run's report and findings into the same file. If it
   belongs to the run still in progress, carry on in it. Never create a second, dated or numbered report file.
4. Add the date, project name, branch/commit, and a one-line summary of the task at the top.

Write the results of **every step** into it as each step is completed. Do not wait until the end. Record: what you found, which check commands pass, each file you filled in, and each **Needs Verification** item.

If this task already has a report from another playbook, add a section there instead of creating a second file. The rules
for reports are in `workflow.md`.

## Step 1: Check where you are

1. Find the project root: the folder that holds this one.
2. If this folder has its own `.git`, stop and tell the owner. It is either the template repository, where nothing should
   be filled in, or a clone that still needs its `.git` removed. Never delete it yourself: that cannot be undone.
3. If the project root has no `.git`, run `git init` there.
4. Follow the branch rule in `agent.md` before you write anything.

## Step 2: Make agents load this folder automatically

Agents only read a docs folder if something tells them to. Tools load a fixed file from the project root, so that file
must point here. Use this folder's real name in place of `docs`.

**`CLAUDE.md`** in the project root (Claude Code):

```markdown
@docs/index.md
```

**`AGENTS.md`** in the project root (Codex, Cursor and most other agents):

```markdown
# Agent instructions

Before doing anything else, read `docs/index.md` and follow it. It routes every task to the right file.
```

If either file already exists, add the line at the top and keep what is there. If it contains rules, leave them in
place and copy any that conflict with `agent.md` into `lessons.md` as open questions for the owner.

## Step 3: Read the project

Read the real thing, not just the README. Look at:

- Package and lock files, runtime version files, and the scripts they define.
- Folder structure and entry points.
- Database schema and migrations.
- Routes or pages, auth and role checks.
- Environment example files. Never open a real `.env` to copy values from it.
- CI config, Dockerfiles and deploy config.
- Tests, and how they run.
- `git log --oneline -30`, for the project's commit style and recent direction.

Then run the check commands you found, and note which ones pass today.

## Step 4: Fill in the project files

Fill in these files from what you found. In `project-description.md`, `overview.md` and `architecture.md`, replace each `<placeholder>` and delete
the `<!-- -->` comments. In `decision.md`, `progress.md` and `lessons.md`, only add entries. Keep their rules, formats
and comments, because later work uses them.

| File | Fill in |
|---|---|
| `project-description.md` | If the owner already wrote it, keep it and treat it as the truth. If not, write it from the code or the brief. |
| `overview.md` | What the product is, stack, commands, environments, roles, domain words. Then set `status: filled`. |
| `architecture.md` | Modules, data flow, data model, auth, integrations, where new code goes. |
| `decision.md` | Only choices you can see were deliberate, marked `Inferred`. Do not invent reasons. Leave it empty if there are none. |
| `progress.md` | Today's state: what works, what is unfinished, what fails, and the check command results. |
| `lessons.md` | Leave the log empty unless Step 2 found rules to carry over. |
| `phases.md` | Leave it empty. Phases are made only when the owner asks. |
| `suggestion.md` | What could be better in this project, using the format in `workflow.md`. Leave it empty if there is nothing real. |

Write only what you confirmed. If you could not work something out, write **Needs Verification** beside it. A short true
file is far more useful than a long guessed one. If the project has no such command or section, write `None`.

For a brand-new project with no code, fill in `project-description.md` and `overview.md` from the owner's brief, confirm the stack using
`language.md`, and leave the rest as templates until there is code.

## Step 5: Commit

Commit the docs folder, the root pointer files and `Setup-Report.md` as one commit on the working branch, following
`agent.md`. This folder's `.gitignore` only keeps the template's README out of git, so leave it.

## Step 6: Report

Tell the owner:

- What the project is, in two sentences, so they can catch a wrong understanding early.
- Which check commands pass and which fail.
- Whether the plugins in `plugins-setup.md` are installed. Do not install them unless the owner asks.
- Each **Needs Verification** item you could not resolve, as a specific question.

Ask nothing else. When the owner answers one of these, write the answer into the file that needed it.

If another prompt brought you here, go back to it now. Otherwise wait for a task.
