# Check Task List Status

Check each tasks against the code and see which are implemented and which are
not.

## Process
1. **Examine Project:** Read project overview file in the `/tasks` directory
    typically named `[project-name]-overview.org`.
2. **Examine Tasks:** Read and examine tasks in tasks file.
3. **Review Incomplete Tasks:** Review tasks in order. For each incomplete tasks
   `[ ]`, review the code to determine if the task has been implement in code.
4. **Update Task List:** For each task marked as incomplete, but that has been
   completed, mark the task as complete. Follow the completion protocol:
   - Mark each finished **sub‑task** `[X]`.
   - Mark the **parent task** `[X]` once **all** its subtasks are `[X]`.
5. **Halt Condition:** While processing tasks marked incomplete in order, halt
   processing on the first task confirmed in code to be not implemented.
