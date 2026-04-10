---
description: "Test-Driven Development: write failing tests first, implement, verify, double-check"
---

# TDD Workflow

You are implementing a feature or fix using strict TDD. Follow this cycle for EACH unit of work.

## Phase 1: Write Failing Tests
- Understand the requirement. Ask if unclear.
- Write test(s) that define the expected behavior.
- Run the tests. They MUST fail. If they pass, the tests are wrong - fix them.
- Commit the failing tests:
```bash
git add <test_files>
git commit -m "test: add failing tests for <feature>"
```

## Phase 2: Implement
- Write the MINIMUM code to make the tests pass. No more.
- Do not refactor yet. Do not add extras. Just pass the tests.
- Run the tests. They must all pass now.

## Phase 3: Verify (Critical)
After tests pass, perform these checks:

1. **Are tests trivially passing?** Review each test assertion. Would it pass with a dummy/empty implementation? If yes, the test is useless - rewrite it.

2. **Negative cases covered?** Are there tests for invalid input, edge cases, error conditions?

3. **Double-check table**: Create a mental checklist:
   - [ ] Happy path tested
   - [ ] Edge cases tested
   - [ ] Error cases tested
   - [ ] Tests fail when implementation is wrong (mutate a line and verify failure)

4. **Run full test suite** to check for regressions:
```bash
<project-specific test command>
```

## Phase 4: Refactor (Optional)
- Only if the code is ugly or duplicated.
- Tests must still pass after refactoring.
- Commit separately:
```bash
git add <files>
git commit -m "refactor: clean up <what>"
```

## Rules
- NEVER write implementation before tests.
- NEVER skip the verification phase.
- Each cycle should be small. If a feature needs many tests, break it into sub-features and cycle through each.
- If unsure about test quality: deliberately break the implementation and confirm tests catch it.
