---
description: Check task list status against actual code implementation
argument-hint: [path to tasks file]
---

# Check Task List Status

## Purpose

Compare each task in a task list against the code and update the list with
tasks that have actually been implemented. Halt on the first incomplete
task so the user can decide what to do next.

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Locate sources:** Read the tasks file from `$ARGUMENTS`. If a project
   overview file exists in `/tasks/` (typically named
   `[project-name]-overview.md`), read it for context.
2. **Read tasks:** Build a mental model of all tasks and their statuses.
3. **Review incomplete tasks in order:** For each task currently marked
   `[ ]`, look at the code to determine whether it has been implemented.
4. **Update the task list:** For each task that turns out to be implemented,
   apply the completion protocol:
   - Mark each finished sub-task `[x]`.
   - Mark a parent task `[x]` once all its sub-tasks are `[x]`.
5. **Halt on first miss:** Process incomplete tasks in order. Stop on the
   first task confirmed in code as not yet implemented and report which one
   it is.

## Important

- Do NOT start implementing missing tasks. Only update statuses.
- Treat the code, not assumptions, as the source of truth for what is
  actually done.

