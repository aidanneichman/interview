# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a structured workflow system for AI-assisted development centered around Product Requirements Documents (PRDs) and task management. The project facilitates breaking down feature requests into PRDs, then generating actionable task lists for implementation.

## Directory Structure

- `/docs/` - Contains workflow documentation and process rules
- `/tasks/` - Destination directory for generated PRDs and task lists (to be created during development)

## Key Workflow Process

The project follows a three-phase development process:

1. **PRD Generation** (`docs/create-prd.md`):
   - AI asks clarifying questions about user's feature request
   - Generates comprehensive PRD in `/tasks/prd-[feature-name].md`
   - PRDs include goals, user stories, functional requirements, and success metrics

2. **Task List Creation** (`docs/generate-tasks.md`):
   - Analyzes existing PRD to create implementation tasks
   - Two-phase approach: parent tasks first, then detailed sub-tasks after user confirmation
   - Generates task list in `/tasks/tasks-[prd-file-name].md`

3. **Task Execution** (`docs/process-task-list.md`):
   - Implements one sub-task at a time with user approval
   - Follows strict completion protocol: mark completed → run tests → commit changes
   - Uses conventional commit format with detailed messages

## Important Rules

- When finishing tasks, run `notify-send "<title>" "<body>" -e -a "Claude Code"` at the end, replacing the two values.
- A PostToolUse hook is configured to play a sound (Glass.aiff) when the Task tool is used.

### PRD Development
- Always ask clarifying questions before generating PRDs
- Target audience is junior developers - be explicit and clear
- Save PRDs as `prd-[feature-name].md` in `/tasks/` directory
- Do NOT start implementation during PRD phase

### Task Management
- One sub-task at a time - wait for user permission between tasks
- Completion protocol for sub-tasks:
  1. Mark sub-task as `[x]` when finished
  2. When all sub-tasks under a parent are complete: run full test suite
  3. If tests pass: stage changes with `git add .`
  4. Clean up temporary files/code
  5. Document changes in `tasks/changeDocs/` (see Change Documentation below)
  6. Commit with descriptive conventional commit message using `-m` flags
  7. Mark parent task as `[x]`

### Change Documentation
- After completing each parent task, create documentation in `tasks/changeDocs/`
- Maintain `tasks/changeDocs/CHANGES.md` with chronological list of completed tasks
- Create individual task docs as `tasks/changeDocs/task-[number]-[brief-name].md`
- Ensure `tasks/changeDocs/` directory exists before writing documentation

### Task List Format
```markdown
## Relevant Files
- `path/to/file.ext` - Description of file purpose

## Tasks
- [ ] 1.0 Parent Task Title
  - [ ] 1.1 Sub-task description
  - [ ] 1.2 Sub-task description
```

## Current Project Context

Based on `docs/project-plan.md`, the initial development target is:
- Python backend service with `/summarize` endpoint
- Claude API integration for text summarization
- Minimal HTML/JS frontend
- Python Poetry for dependency management
- pytest for testing, optional Playwright for UI testing

## Testing Strategy

- Unit tests should be co-located with source files
- Use `npx jest [optional/path]` for JavaScript/TypeScript projects
- Use `pytest` for Python projects
- Always run full test suite before committing completed parent tasks

## Workflow File Dependencies

The three-phase process is defined across multiple documentation files:
- `docs/create-prd.md` - PRD generation rules and structure
- `docs/generate-tasks.md` - Task list creation from PRDs (two-phase: parent tasks → sub-tasks)
- `docs/process-task-list.md` - Implementation protocol and change documentation