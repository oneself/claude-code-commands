---
description: Review uncommitted or recent git changes with critical feedback
argument-hint: [optional scope, e.g. "last commit" or "since main"]
---

# Code Review

## Purpose

Review uncommitted or recently committed git changes and provide critical
feedback to the engineer who wrote the code. Output a structured review file
the engineer can work through.

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Read scope:** Take any scope hint from `$ARGUMENTS` (e.g. "last commit",
   "since main"). Default to uncommitted changes if no hint is given.
2. **Identify files:** Use `git diff --name-only` for uncommitted changes, or
   `git log --name-only -1` (or the equivalent for the requested scope) to
   list the files that need review.
3. **Show file list:** Show the user the list of files to review, each with a
   one-line description of the changes. Then ask whether to proceed ("Go" or
   "Stop").
4. **Wait for confirmation:** Pause and wait for the user to respond with
   "Go" before continuing.
5. **Read each file:** For each file, read the full contents and identify
   the overall purpose and main functionality. Run `git diff` (or
   `git show`) to see the actual changes.
6. **Review changes:** For each file, review the changes themselves and the
   surrounding code for context. Focus on:
   - Potential bugs
   - Performance issues
   - Code duplication
   - Removing dead code
   - Making code easy to understand
   - Adherence to style conventions
   - Avoiding magic numbers
   - Missing documentation
   - Missing tests
   - Missing logging
   - **MOST IMPORTANT:** Is there any way to simplify the implementation?
7. **Generate output:** Write the review file with a one-line description per
   file and a list of feedback items. Each item should describe what needs to
   be done and why.

## Output Format

- **Format:** markdown (`.md`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-[feature-name]-review.md`
  (`[feature-name]` is determined from a summary of the changes)
- **Style:** Keep to 80 character row length. Trim trailing whitespace. End
  files with an empty line.

## Output Template

```markdown
# [feature-name] - Review

High-level description of the nature of the changes in this review.

- [ ] 1.0 [path/to/file1.js](path/to/file1.js) — One-line description
  - [ ] 1.1 Feedback item description
  - [ ] 1.2 Feedback item description
- [ ] 2.0 [path/to/file2.js](path/to/file2.js) — One-line description
  - [ ] 2.1 Feedback item description
```

## Interaction Model

The process requires a pause after generating the initial file list. Get user
confirmation before reviewing file contents. This ensures the high-level plan
to review aligns with expectations before the expensive analysis.

## Target Audience

Assume the primary reader of the review is a **junior developer** who needs
to understand how to fix the issues.

## Important

- Do NOT start implementing the feedback.
- Do NOT include files that have no actionable feedback. Only list files
  that need changes.

