---
description: Generate a detailed task list from a PRD (and optionally a TSD)
argument-hint: [path to prd file] [optional path to tsd file]
---

# Generate a Task List from a PRD

## Purpose

Create a detailed, step-by-step task list in markdown based on an existing
Product Requirements Document (PRD), and optionally a Technical Specification
Document (TSD). The task list should guide a junior developer through the
implementation.

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Receive references:** Read the PRD path (and optional TSD path) from
   `$ARGUMENTS`.
2. **Analyze sources:** Read and analyze the functional requirements, user
   stories, and other sections of the PRD. If a TSD is provided, read it as
   well to ground sub-tasks in the chosen technical approach.
3. **Phase 1 — Generate parent tasks:** Create the file and generate the
   main, high-level tasks required to implement the feature. Use judgment on
   how many parent tasks to create (typically about 5). Present these tasks
   to the user without sub-tasks yet, then ask whether to proceed with
   sub-tasks ("Go" or "Wait").
4. **Wait for confirmation:** Pause and wait for the user to respond with
   "Go" before continuing.
5. **Phase 2 — Generate sub-tasks:** Break down each parent task into
   smaller, actionable sub-tasks. Ensure each sub-task logically follows from
   its parent and covers the implementation details implied by the PRD/TSD.
6. **Identify relevant files:** Based on tasks and the PRD/TSD, identify
   potential files to be created or modified. List them under the "Relevant
   Files" section, including test files if applicable.
7. **Generate final output:** Combine parent tasks, sub-tasks, relevant
   files, and notes into the final markdown structure.
8. **Save task list:** Save in `/tasks/` with the filename
   `[YYYY-MM-DD]-[feature-name]-tasks.md`, where `[feature-name]` matches the
   base name of the input PRD file. Get the current date by running
   `date +%Y-%m-%d`.

## Output Format

- **Format:** markdown (`.md`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-[feature-name]-tasks.md`
- **Style:** Keep to 80 character row length. Trim trailing whitespace. End
  files with an empty line.

## Output Template

The generated task list must follow this structure:

```markdown
# [feature-name] - Task List

## Relevant Files

- [path/to/prd.md](path/to/prd.md) — Feature Name - Product Requirements
  Document
- [path/to/tsd.md](path/to/tsd.md) — Feature Name - Technical Specification
  Document
- [path/to/potential/file1.ts](path/to/potential/file1.ts) — Brief
  description of relevance
- [path/to/file1.test.ts](path/to/file1.test.ts) — Unit tests for `file1.ts`
- [path/to/another/file.tsx](path/to/another/file.tsx) — Brief description
- [path/to/another/file.test.tsx](path/to/another/file.test.tsx) — Unit
  tests for `another/file.tsx`

## Notes

- Unit tests should be placed alongside the code files they test.
- Replace the test command below with whatever the project uses (check
  `package.json` scripts, `Makefile`, etc.).

## Tasks

- [ ] 1.0 Parent Task Title
  - [ ] 1.1 Sub-task description 1.1
  - [ ] 1.2 Sub-task description 1.2
- [ ] 2.0 Parent Task Title
  - [ ] 2.1 Sub-task description 2.1
- [ ] 3.0 Parent Task Title (may not need sub-tasks if structural or config)
```

## Inline File References

When referencing a specific file inline, use a markdown link:

- Good: There is important info in
  [important_file.ts](path/to/important_file.ts). Take a look.
- Bad: There is important info in `important_file.ts`. Take a look.

## Interaction Model

The process requires a pause after generating parent tasks to get user
confirmation ("Go") before generating detailed sub-tasks. This ensures the
high-level plan aligns with expectations before diving into details.

## Target Audience

Assume the primary reader of the task list is a **junior developer** who will
implement the feature.

