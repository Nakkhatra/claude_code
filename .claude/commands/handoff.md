---
description: "Create a handoff document capturing current progress for context-fresh continuation"
---

# Create Handoff Document

Generate `.claude/HANDOFF.md` summarizing the current work state. This document will be used to resume work in a fresh conversation with minimal token cost.

## Structure

Write the following to `.claude/HANDOFF.md`:

```markdown
# Handoff - [DATE]

## Goal
<What we're trying to accomplish. One paragraph max.>

## Progress
- [x] <completed step>
- [x] <completed step>
- [ ] <next step>
- [ ] <remaining step>

## Key Decisions
<Non-obvious decisions made and WHY. Only things not evident from the code.>

## What Worked
<Approaches that succeeded. Be specific about commands/patterns.>

## What Didn't Work
<Dead ends. Include WHY they failed so the next session doesn't retry them.>

## Files Modified
<List of files touched in this session with one-line description of change.>

## Next Steps
<Exact instructions for the next conversation to pick up where we left off. Be specific enough that a fresh Claude can execute without re-reading everything.>
```

## Rules
- Be ruthlessly concise. Every line must earn its place.
- Don't describe code that's self-evident from reading the files.
- Focus on CONTEXT that would be lost between conversations.
- Include exact file paths, not descriptions of where things are.
- After writing, tell the user: "Start a new conversation and say: read .claude/HANDOFF.md and continue from where we left off"
