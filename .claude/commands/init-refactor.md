---
description: "Preserve custom CLAUDE.md rules while reinitializing project structure"
---

# Initialize with Refactor

Refresh the project's Claude Code configuration while preserving custom project rules.

## 1. Back up current CLAUDE.md
```bash
cp CLAUDE.md .claude/CLAUDE.md.backup
```

## 2. Extract custom sections
From the backup, identify and save these sections:
- Communication
- Token Efficiency
- Multi-Phase Strategy
- Code Quality & Style
- Testing Protocol
- Git Workflow
- Verification & Self-Check

## 3. Run init
Remove the current CLAUDE.md:
```bash
rm CLAUDE.md
```

Then trigger the `/init` flow to generate a fresh CLAUDE.md with project structure.

## 4. Merge custom sections
Take the newly generated CLAUDE.md and merge back your custom sections:
- Keep the new boilerplate and project structure info from init
- Replace or append your custom Communication, Token Efficiency, etc. sections

## 5. Verify and commit
```bash
git diff CLAUDE.md
```

Review the merged result. If good:
```bash
rm .claude/CLAUDE.md.backup
git add CLAUDE.md
git commit -m "refactor: reinitialize CLAUDE.md with updated project structure"
```

If issues, restore from backup:
```bash
cp .claude/CLAUDE.md.backup CLAUDE.md
```
