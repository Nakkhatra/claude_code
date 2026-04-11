# Claude Code Configuration

Reusable Claude Code configuration files - slash commands, project rules, and settings. Drop these into any project's `.claude/` directory to get a consistent workflow.

Based on tips from [ykdojo/claude-code-tips](https://github.com/ykdojo/claude-code-tips).

## File Structure

```
.
├── CLAUDE.md                          # Project-level rules
├── .claude/
│   ├── settings.local.json            # Permissions, hooks, auto-sync
│   ├── agents/
│   │   └── coder.md                   # /coder (sub-agent)
│   └── commands/
│       ├── add-and-commit.md          # /add-and-commit
│       ├── init-refactor.md           # /init-refactor
│       ├── sync.md                    # /sync
│       ├── handoff.md                 # /handoff
│       ├── gha.md                     # /gha
│       ├── tdd.md                     # /tdd
│       └── review.md                  # /review
```

## What Each File Does

### `CLAUDE.md`
Project-wide rules loaded into every conversation. Covers:
- Communication style (no fluff, be blunt)
- Token efficiency (surgical reads, no re-reading, no global scans)
- Multi-phase planning with `.claude/current_plan.md`
- TDD protocol, git workflow, self-verification

### `.claude/settings.local.json`
- **Allowed commands**: git, gh, npm test/lint/format - no prompt interruptions for safe ops
- **Denied commands**: `git push --force`, `rm -rf`, `--dangerously-skip-permissions`, push to main
- **Auto-sync hook**: Runs `git pull --rebase` automatically when creating a new branch

### Slash Commands

| Command | What it does |
|---------|-------------|
| `/add-and-commit` | Stages only necessary files (never `git add .`), creates a typed branch (`feat/`, `fix/`, etc.), commits, pushes, creates PR to main, adds GitHub Copilot as reviewer |
| `/init-refactor` | Preserves custom CLAUDE.md project rules while reinitializing project structure. Backs up rules, runs init, merges custom sections into new config |
| `/sync` | Pulls latest from remote with rebase. Auto-stashes dirty working tree, restores after. Reports ahead/behind status |
| `/handoff` | Creates `.claude/HANDOFF.md` with goal, progress, decisions, dead ends, and next steps. For resuming work in a fresh conversation with minimal tokens |
| `/gha` | Investigates GitHub Actions failures. Fetches logs, checks flakiness ratio, finds breaking commit, checks for existing fix PRs, suggests root cause and fix |
| `/tdd` | Strict TDD cycle: write failing tests first, commit, implement minimum code, verify tests aren't trivially passing, refactor separately. Each step is committed independently |
| `/coder` | Sub-agent for delegated coding tasks. Runs in isolated context, executes one specific task following project linting/formatting/docstring standards without loading full conversation |
| `/review` | Interactive code review. Categorizes changes by risk, checks correctness/security/performance/test coverage. User controls depth: blockers-only, deep-dive, security-focus |

## Usage

### Drop into a project
```bash
cp CLAUDE.md /path/to/your/project/
cp -r .claude/ /path/to/your/project/.claude/
```

### Or symlink for shared config
```bash
ln -s /path/to/claude_code/CLAUDE.md /path/to/your/project/CLAUDE.md
ln -s /path/to/claude_code/.claude /path/to/your/project/.claude
```

### Typical workflow
```
/sync              # pull latest
/tdd               # implement with tests
/add-and-commit    # branch, commit, PR with Copilot review
/handoff           # save context if continuing later
```
