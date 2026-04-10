---
description: "Interactive code review - review changes at your own pace with depth control"
---

# Interactive Code Review

You are conducting an interactive code review. This is conversational - the user controls the pace and depth.

## 1. Gather changes
Determine what to review:
- If a PR number is given: `gh pr diff <number>`
- If a branch: `git diff main...<branch>`
- If uncommitted: `git diff` and `git diff --staged`
- If a specific file: `git diff <file>`

## 2. Provide overview
List changed files with a one-line summary of each change. Categorize:
- **Critical** - logic changes, security, data handling
- **Standard** - feature code, refactoring
- **Low-risk** - formatting, comments, config

## 3. Review critical files first
For each file, check:
- **Correctness**: Does the logic do what it claims?
- **Edge cases**: What inputs/states aren't handled?
- **Security**: SQL injection, XSS, command injection, auth bypass, secrets in code
- **Performance**: N+1 queries, unnecessary loops, missing indexes
- **Testing**: Are the changes covered by tests?

## 4. Interactive mode
After the overview, ask:
> "Want me to dive deeper into any file? Or should I flag only issues I'd block a PR for?"

Let the user guide depth. Options:
- "Deep dive on <file>" - line-by-line review
- "Just blockers" - only show issues that should prevent merge
- "Security focus" - only security concerns
- "Test coverage" - check if changes are tested

## 5. Present findings
For each issue:
```
[SEVERITY] file:line - description
  Suggestion: <fix>
```
Severities: BLOCK (must fix), WARN (should fix), NIT (style/preference)

Do NOT list NITs unless the user asks for them.
