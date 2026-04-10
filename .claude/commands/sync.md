---
description: "Pull latest changes from remote, rebase current branch, report status"
---

# Sync with Remote

Bring the current branch up to date with the remote. Follow these steps:

## 1. Check current state
```bash
git status
git branch --show-current
```

## 2. Stash if dirty
If there are uncommitted changes:
```bash
git stash push -m "auto-stash before sync $(date +%Y%m%d-%H%M%S)"
```

## 3. Pull with rebase
```bash
git fetch origin
git rebase origin/main
```

If rebase conflicts occur:
- Show the conflicting files
- Ask the user how to resolve (don't auto-resolve)

## 4. Restore stash if needed
```bash
git stash pop
```

If stash pop conflicts, show the conflicts and ask for guidance.

## 5. Report
Show: current branch, commits ahead/behind origin, any untracked files. One-line summary.
