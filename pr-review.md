---
description: Checkout and review a GitHub PR with a structured report
argument-hint: [PR number or URL]
---

# PR Review

## Purpose

Checkout a GitHub PR locally, rebase it from main, run the project's build
and tests, then review all changes with a structured report highlighting
file-level diffs, data model changes, API changes, and risky modifications.

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Read PR identifier** from `$ARGUMENTS`. If empty or invalid, stop and
   ask for a PR number.
2. **Fetch PR metadata:** Run
   `gh pr view <PR> --json number,title,headRefName,baseRefName,body`.
   Display the PR title, branch name, and a one-line summary. If the PR is
   not found, stop.
3. **Checkout the PR branch:** Stash any uncommitted local changes, then
   check out the PR branch with `gh pr checkout <PR>`. If checkout fails,
   stop and report.
4. **Rebase onto main:** Run `git fetch origin main` and
   `git rebase origin/main`. If conflicts occur, resolve them; do not
   proceed with unresolved conflicts.
5. **Run build and tests (optional):** If the project has obvious build
   and test commands (check `README.md`, `CLAUDE.md`, `package.json`
   scripts, or `Makefile`), run them. If you cannot tell what they are,
   ask the user whether to run anything or skip. If they fail, stop and
   report; the review cannot continue against broken code.
6. **List changed files:** Run
   `git diff --stat origin/main...HEAD` and
   `git diff --name-status origin/main...HEAD`. Show the file list with
   change type (added, modified, deleted) and line counts.
7. **Confirm scope:** Ask whether to proceed with the full review ("Go" or
   "Stop"). Pause and wait for the response.
8. **Per-file deep review:** For each changed file, read the full diff
   (`git diff origin/main...HEAD -- <file>`) and the current file contents
   for context. Group findings into the sections below.

   **Section A: Data Model changes**
   Flag schema changes, database model changes, migration files, enum
   changes, type definition changes.

   **Section B: API changes**
   Flag new or modified API routes, request and response shape changes, and
   anything that affects external contracts.

   **Section C: Infrastructure changes**
   Flag build script changes (e.g. `package.json` scripts, `Makefile`, CI),
   `CLAUDE.md` or `.claude/` command and settings changes, ESLint/Prettier/
   tsconfig changes, Dockerfile or docker-compose changes, env var
   additions/removals, and init/cleanup/setup script changes. For each,
   note what changed and whether it affects all developers (cross-platform
   compatibility, new env vars, etc.).

   **Section D: Changes by file**
   For each file, summarize what changed and why (inferred from context).

   **Section E: Risk assessment**
   Flag anything that looks wrong or risky:
   - Logic errors or potential bugs
   - Missing error handling
   - Security concerns (injection, auth bypass, exposed secrets)
   - Breaking changes to existing interfaces
   - Race conditions or concurrency issues
   - Performance regressions (N+1 queries, missing indexes, large payloads)
   - Incomplete migrations or schema mismatches
   - Dead code or leftover debug statements
   - Hard-coded values that should be configurable

   For each risk, propose a fix.
9. **Write the report** to the output file.

## Output Format

- **Format:** markdown (`.md`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-pr-[PR-NUMBER]-review.md`
- **Style:** Keep to 80 character row length. Trim trailing whitespace. End
  files with an empty line.

## Output Template

```markdown
# PR #[number] - [title] - Review

## Summary

PR: #[number] [title]
Branch: [head-branch] -> [base-branch]
Files changed: [count] | Additions: [+lines] | Deletions: [-lines]
Build: [pass/fail/skipped]
Rebase: [clean/conflicts/skipped]

[1-3 sentence summary of what this PR does]

## A. Data Model Changes

[If none: "No data model changes detected."]

- [Description of the model change and its impact]

## B. API Changes

[If none: "No API changes detected."]

- [Description of the API change and its impact]

## C. Infrastructure Changes

[If none: "No infrastructure changes detected."]

- [Description of the infra change, cross-platform or team impact]

## D. Changes by File

### [path/to/file1](path/to/file1) (added/modified/deleted, +X -Y)
[Summary of changes in this file]

### [path/to/file2](path/to/file2) (added/modified/deleted, +X -Y)
[Summary of changes in this file]

## E. Risk Assessment

[If none: "No significant risks identified."]

- [ ] **[risk-level: HIGH/MEDIUM/LOW]** [path/to/file:line](path/to/file):
  Description of the risk
  - **FIX:** Suggested remediation
```

## Interaction Model

The process requires a pause after the file list (step 7). Get confirmation
before the detailed review so the user can verify scope before the expensive
analysis.

## Important

- Do NOT modify any code in the PR. This is a read-only review.
- Sections A, B, and C should be empty rather than padded if no changes.
- Section E risks should include `file:line` references where possible.
- NEVER create a new branch. Always checkout the PR's existing branch.

