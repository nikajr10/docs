---
type: playbook
read_when: The owner asks to set up plugins, or you need to know which plugin suits a job (Phase 4).
then: workflow.md
---

# Claude Code Plugins & Skills Setup

## Role
Act as a senior developer setting up Claude Code for this project. Install and verify the approved plugins and skills listed below, then use each one only in the situations described. Run every install yourself with the `claude plugin` shell commands below, so the owner does not need to type anything. The **diagram skills are installed but must never run unless the user explicitly asks for a diagram.**

## Step 0: Create the Report File
Before doing anything else:
1. Check whether `Plugin-Setup-Report.md` exists in the project root.
2. If it does not exist, create it.
3. If it already exists, clear it and write this run's report and findings into the same file. Never create a second, dated or numbered report file.
4. Add the setup date, project name, and Claude Code version (`claude --version`) at the top.

Write the results of **every phase** into `Plugin-Setup-Report.md` as each phase is completed.

## Phase 1: Pre-Check
Confirm before installing:
- Claude Code is installed and up to date
- Node.js is on the PATH for non-interactive shells (needed by Ponytail hooks; check this if nvm is used on macOS)
- Git is installed (needed to add marketplaces)
- Which plugins and marketplaces are already installed (`claude plugin list`, `claude plugin marketplace list`)
- Install scope to use: **user** (all projects) or **project** (this repo only). Default: **user**, unless the user says otherwise.

**Write to `Plugin-Setup-Report.md`:** a Pre-Check table (Check | Result | Notes) and the list of already-installed plugins.

## Phase 2: Install Plugins & Skills
Install in this order. Skip anything already installed. Add `--scope project` to an install command if that is the scope chosen in Phase 1. After each install, run `claude plugin details <plugin>` and confirm it only adds what is expected (skills, agents, hooks, MCP servers). New hooks load at the next session, so this check comes before they can run.

### 1. Clean & Minimal Code
| Plugin | Install Commands | Purpose |
|---|---|---|
| Ponytail | `claude plugin marketplace add DietrichGebert/ponytail` → `claude plugin install ponytail@ponytail` | Less code, simpler solutions, marked shortcuts |
| Superpowers | `claude plugin marketplace add obra/superpowers-marketplace` → `claude plugin install superpowers@superpowers-marketplace` | Plan-first, test-driven workflow |
| Feature Dev (official) | `claude plugin install feature-dev@claude-plugins-official` | Structured multi-phase feature building |

### 2. Code Review
| Plugin | Install Commands | Purpose |
|---|---|---|
| Code Review (official) | `claude plugin install code-review@claude-plugins-official` | Parallel review agents for bugs and edge cases |
| PR Review Toolkit (official) | `claude plugin install pr-review-toolkit@claude-plugins-official` | Review before merging |

### 3. Security
| Plugin | Install Commands | Purpose |
|---|---|---|
| /security-review | Built in, no install | Vulnerability scan of pending changes |
| Security Guidance (official) | `claude plugin install security-guidance@claude-plugins-official` | Security warnings while editing |
| Trail of Bits skills | `claude plugin marketplace add trailofbits/skills` → install the static-analysis plugin from that marketplace | CodeQL / Semgrep based analysis |

### 4. Frontend & Testing
| Plugin | Install Commands | Purpose |
|---|---|---|
| Frontend Design (official) | `claude plugin install frontend-design@claude-plugins-official` | Better, non-generic UI |
| Anthropic example skills | `claude plugin marketplace add anthropics/skills` → install the skills set containing **webapp-testing**, **skill-creator**, **mcp-builder** | Playwright UI testing, creating skills, building MCP servers |

### 5. Diagrams (Install Only — Do Not Run)
| Plugin | Install Commands | Purpose |
|---|---|---|
| CCC Excalidraw | `claude plugin marketplace add ooiyeefei/ccc` → `claude plugin install ccc-skills@ccc` | Architecture diagrams from the codebase as `.excalidraw` |

**If an install command fails:** do not guess. Run `claude plugin list --available --json`, find the correct plugin name in the added marketplace, and record the exact name used. If a plugin cannot be found, mark it **Not Installed** with the reason.

After all installs, tell the owner to **restart Claude Code** so hooks and skills load. You cannot do this yourself, so put it under **Needs you** in your report.

**Write to `Plugin-Setup-Report.md`:** an Installation table (Plugin | Marketplace | Scope | Status: Installed / Already Installed / Failed | Commands/Skills Added | Notes).

## Phase 3: Verify
For each installed plugin:
- Confirm it appears as enabled in `claude plugin list`
- Confirm its skills and commands with `claude plugin details <plugin>`
- Run only **harmless help/status commands** to confirm it works (e.g. `/ponytail-help`). A plugin installed in this session is not loaded until the restart, so mark that check **Needs Verification**.
- **Do not run** any diagram skill, full review, or audit during verification

**Write to `Plugin-Setup-Report.md`:** a Verification table (Plugin | Enabled | Commands Visible | Test Command | Result).

## Phase 4: Usage Rules
Plugins are optional help. If one is not installed, carry on without it. Never stop a task for a missing plugin. Use each tool only in these situations:

| Situation | Use |
|---|---|
| Writing or changing code | Ponytail (default mode: **lite** or **full**, not ultra, unless asked) |
| Building a new feature | Superpowers or Feature Dev (plan → tests → build) |
| Before committing code | `/security-review` |
| Before merging / finishing a task | Code Review, PR Review Toolkit |
| Full security audit, when the owner asks | Trail of Bits skills + `security.md` or `API-Security.md` |
| Code quality review, when the owner asks | Code Review + Ponytail review/audit + `code-quality.md` |
| Building UI | Frontend Design + `Frontend-Design-Build.md` |
| Checking UI works | webapp-testing (Playwright) |
| Turning `.md` guides into skills | skill-creator |
| Building MCP servers | mcp-builder |
| **Architecture / workflow diagram** | **CCC Excalidraw — ONLY when the user explicitly asks** |

**Review levels:** follow `effort.md`. Never choose the `max` or `ultra` level of a review yourself, and never switch to ultracode.

### Diagram Rule (Important)
- **Never run a diagram skill automatically**, not after setup, not after a feature, not during reviews or audits.
- Run it **only** when the user clearly asks, e.g. "make a diagram", "draw the architecture", "show the workflow diagram".
- When asked, save diagrams to a `diagrams/` folder in the project root (e.g. `diagrams/system-architecture.excalidraw`) unless the user gives another path. Never save them inside this docs folder, which stays flat.
- When updating an existing diagram, read the old one first and update it instead of starting over.

### Conflict Rules
- Every file in this folder has priority over plugin defaults. `index.md` gives the full order.
- Superpowers and Feature Dev work inside `workflow.md`. They do not replace its steps, and the record and report steps still apply.
- Ponytail's "less code" must never remove validation, auth checks, error handling, or security guards.
- If two plugins give different advice, follow the project's `.md` guides and note the conflict in the report.

**Write to `Plugin-Setup-Report.md`:** a Usage Rules section copying the table above, plus any conflicts noticed.

## Phase 5: Final Summary
Complete `Plugin-Setup-Report.md` so it contains, in this order:
1. **Header** – project name, date, Claude Code version
2. **Summary** – how many installed, already installed, failed
3. **Pre-Check results**
4. **Installation table**
5. **Verification table**
6. **Usage Rules** (including the Diagram Rule)
7. **Failed / Skipped plugins** – reason and suggested fix
8. **Next Steps** – e.g. turn project `.md` guides into skills with skill-creator

## Rules
- Create `Plugin-Setup-Report.md` first, before any other step.
- Update `Plugin-Setup-Report.md` after each phase.
- Install only plugins from the list above; ask before installing anything else.
- Run `claude plugin details` on each plugin you install. If it adds unexpected hooks, MCP servers, or permissions, run `claude plugin disable <plugin>`, then stop and ask.
- Never guess plugin names; check the marketplace and record the exact name.
- **Diagram skills: install only, run only when the user explicitly asks.**
- Do not run full reviews, audits, or refactors during setup; verification uses help/status commands only.
- Never weaken security, validation, or error handling because a plugin suggests less code.
- Never touch production data, real credentials, or live systems.