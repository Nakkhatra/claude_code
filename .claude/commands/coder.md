---
description: "Spawn a coding sub-agent with isolated context to execute a specific task"
---

Spawn a sub-agent using the Agent tool to execute this coding task in a separate context. Pass the task description and the coding standards below into the agent prompt.

**Task from user:** $ARGUMENTS

Use the Agent tool with these parameters:
- description: short summary of the task (3-5 words)
- subagent_type: "general-purpose"
- prompt: Include ALL of the following in the prompt:

---BEGIN AGENT PROMPT---

# Coding Agent

You are executing ONE specific coding task. Do exactly that task. Nothing more.

## Task
$ARGUMENTS

## Constraints
- Read ONLY files directly relevant to your task. Do NOT scan the whole repo.
- If something is ambiguous, pick the most reasonable interpretation and note your assumption in a code comment.
- Do NOT ask questions.

## Coding Standards

### Style
- Follow existing file conventions. Match indentation, naming, and patterns already in the file.
- If no existing convention: use the project's linter/formatter config.

### Linting & Formatting
Before completing your task, run the project's formatter/linter. Fix all lint errors your changes introduced. Do not fix pre-existing lint errors in untouched code.

### Docstrings & Comments
- Add docstrings to public functions/methods you CREATE (not ones you modify).
- Match existing docstring style in the project.
- Add inline comments ONLY where logic is non-obvious.

### Type Safety
- Add type annotations to function signatures you create.
- Do not add types to existing untyped code unless asked.

## Execution Steps
1. Identify affected files — use grep/glob, don't scan the whole repo.
2. Read only those files (or relevant sections via offset/limit).
3. Implement the change.
4. Run the formatter/linter for the languages you touched.
5. Run relevant tests if they exist. Fix if broken by your change.
6. Report back: list files modified, what you changed (one line each), any assumptions made.

---END AGENT PROMPT---
