# Project Rules

## Communication
- No fluff. No "I understand." No summaries of what you just did. Direct output or direct questions only.
- Use shorthand. Be blunt. Grammar doesn't matter.
- In Plan Mode: identify all unknowns, ask unresolved questions BEFORE finalizing.

## Token Efficiency
- Never re-read a file already in conversation history. Reference existing context.
- Use `grep` to find line numbers first, then `read(file, offset, limit)` for files >300 lines.
- No global repo scans unless explicitly requested. Map only files affected by current phase.
- Verify edits by reading back only edited lines, not the whole file.
- Start fresh conversations for new topics. Context degrades over long conversations.

## Multi-Phase Strategy
- Save plans to `.claude/current_plan.md`. Implement one phase at a time.
- After each phase, confirm next phase is still valid based on code changes.
- Refer to `current_plan.md` to maintain state without re-summarizing chat history.

## Code Quality & Style
- Break complex bash into multiple simple commands. Avoid complex pipes.
- Never use `2>&1`. Never use `--dangerously-skip-permissions` on host.
- For git in other dirs: `cd <path> && git ...`
- Ask "why did you add this line?" if code seems overcomplicated. Simplify aggressively.

## Testing Protocol
- Write failing tests FIRST (TDD). Commit tests before implementing.
- After implementation, verify tests pass AND review tests aren't trivially passing.
- Double-check every claim. Make a verification table if multiple assertions.

## Git Workflow
- Let Claude handle commits and branching. Allow pull automatically.
- Do NOT push without explicit permission.
- Use draft PRs for low-risk, Claude-managed PR creation.
- Disable attribution noise - focus on the code.

## Verification & Self-Check
- After completing each step, verify the output works before moving on.
- Use `git diff` to review changes before committing.
- For UI changes: start dev server, test golden path + edge cases in browser.
- "Double check everything, every single claim. Make a table of what you were able to verify."
