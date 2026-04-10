---
description: "Investigate GitHub Actions CI/CD failures - find root cause, check flakiness, suggest fix"
---

# GitHub Actions Investigation

You are debugging a GitHub Actions failure. Be thorough and systematic.

## 1. Get failure info
```bash
gh run list --status failure --limit 5
```

Pick the most recent failure (or the one the user specified) and get details:
```bash
gh run view <RUN_ID> --log-failed
```

## 2. Identify the failing step
Extract the exact error message and failing command. Quote it verbatim.

## 3. Check if flaky
```bash
gh run list --workflow <WORKFLOW_NAME> --limit 20
```
Look at pass/fail pattern. If it alternates, it's likely flaky. Report the flakiness ratio.

## 4. Find the breaking commit
```bash
gh run list --workflow <WORKFLOW_NAME> --limit 10 --json headSha,conclusion,createdAt
```
Identify the first failing run and the commit that introduced it:
```bash
git log --oneline <last_passing_sha>..<first_failing_sha>
```

## 5. Check for existing fixes
```bash
gh pr list --search "fix CI" --state open
gh pr list --search "fix workflow" --state open
gh pr list --search "fix test" --state open
```

## 6. Diagnose root cause
Read the relevant workflow file and the failing code. Identify:
- Is it a code bug, dependency issue, config issue, or infra issue?
- Is the fix in our control or upstream?

## 7. Report
Present findings as:
- **Error**: exact error message
- **Flaky**: yes/no (with ratio)
- **Breaking commit**: sha + message
- **Root cause**: one sentence
- **Suggested fix**: specific action to take
