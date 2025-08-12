# Task List Management

Guidelines for managing task lists in markdown files to track progress on completing a PRD

## Task Implementation
- **One sub-task at a time:** Do **NOT** start the next sub‑task until you ask the user for permission and they say "yes" or "y"
- **Completion protocol:**  
  1. When you finish a **sub‑task**, immediately mark it as completed by changing `[ ]` to `[x]`.
  2. If **all** subtasks underneath a parent task are now `[x]`, follow this sequence:
    - **First**: Run the full test suite (`pytest`, `npm test`, `bin/rails test`, etc.)
    - **Only if all tests pass**: Stage changes (`git add .`)
    - **Clean up**: Remove any temporary files and temporary code before committing
    - **Document changes**: Save a quick overview of the changes in `tasks/changeDocs/` (see Change Documentation section below)
    - **Commit**: Use a descriptive commit message that:
      - Uses conventional commit format (`feat:`, `fix:`, `refactor:`, etc.)
      - Summarizes what was accomplished in the parent task
      - Lists key changes and additions
      - References the task number and PRD context
      - **Formats the message as a single-line command using `-m` flags**, e.g.:

        ```
        git commit -m "feat: add payment validation logic" -m "- Validates card type and expiry" -m "- Adds unit tests for edge cases" -m "Related to T123 in PRD"
        ```
  3. Once all the subtasks are marked completed and changes have been committed, mark the **parent task** as completed.
- Stop after each sub‑task and wait for the user's go‑ahead.

## Change Documentation

After completing each parent task (when all subtasks are `[x]` and code is committed), create documentation in `tasks/changeDocs/`:

### Running Changes Log
- **File**: `tasks/changeDocs/CHANGES.md`
- **Purpose**: Maintain a chronological list of all completed tasks and their key changes
- **Format**: 
  ```markdown
  # Change Log
  
  ## [Date] - Task X.X: [Task Title]
  - Brief summary of what was implemented
  - Key files modified/created
  - Notable decisions or approaches taken
  
  ## [Date] - Task Y.Y: [Another Task Title]
  - ...
  ```

### Individual Task Documentation
- **File**: `tasks/changeDocs/task-[number]-[brief-name].md`
- **Purpose**: Detailed overview of changes for each completed parent task
- **Content**:
  - Task title and number
  - Brief description of what was implemented
  - List of files created/modified with explanations
  - Key implementation decisions
  - Any challenges encountered and solutions
  - Test results summary

**Example**: For task "1.0 Setup payment validation", create `tasks/changeDocs/task-1-payment-validation.md`

## Task List Maintenance

1. **Update the task list as you work:**
   - Mark tasks and subtasks as completed (`[x]`) per the protocol above.
   - Add new tasks as they emerge.

2. **Maintain the "Relevant Files" section:**
   - List every file created or modified.
   - Give each file a one‑line description of its purpose.

## AI Instructions

When working with task lists, the AI must:

1. Regularly update the task list file after finishing any significant work.
2. Follow the completion protocol:
   - Mark each finished **sub‑task** `[x]`.
   - Mark the **parent task** `[x]` once **all** its subtasks are `[x]`.
3. Add newly discovered tasks.
4. Keep "Relevant Files" accurate and up to date.
5. Before starting work, check which sub‑task is next.
6. After implementing a sub‑task, update the file and then pause for user approval.
7. **After completing each parent task**: Create change documentation in `tasks/changeDocs/` before marking the parent task as complete.
8. **Ensure the `tasks/changeDocs/` directory exists** before attempting to write documentation files.