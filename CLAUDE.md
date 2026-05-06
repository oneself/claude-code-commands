# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with
the command templates in this repository.

## Repository Overview

This repository contains command templates for the Claude Code CLI that
implement a structured development workflow. The commands are designed to
help developers (especially junior developers) work effectively with AI
assistance through incremental, well-documented steps.

## Command Set and Workflow

The repository implements a PRD → TSD → Tasks → Implementation workflow:

1. `/prd` — Generate a Product Requirements Document from a user
   description
2. `/tsd` — Generate a Technical Specification Document from a PRD
3. `/tasks` — Convert a PRD (and optional TSD) into concrete
   implementation tasks
4. `/impl` — Work through the task list one sub-task at a time
5. `/review` — Critical review of git changes before committing
6. `/commit` — Create a structured git commit with a clear message

Additional commands:

- `/pr-review` — Checkout and review a GitHub PR with a structured report
- `/security-review` — Security review of pending changes on the current
  branch
- `/build` — Build the project and fix compilation errors and failing
  tests
- `/check` — Verify task list status against actual code

## Command Template Structure

All command templates follow the same structure:

- YAML frontmatter with `description:` and (optionally) `argument-hint:`
  and `allowed-tools:`
- `# Title`
- `## Purpose` — 1–2 sentences on what the command does and when to use it
- `## Process` — numbered steps in execution order, with two-phase
  user-confirmation gates where appropriate
- `## Output Format` — for commands that produce a document (markdown
  format, location under `/tasks/`, dated filename pattern)
- `## Output Template` — concrete template with placeholders
- `## Target Audience` — for PRD/TSD/tasks/review: "primary reader is a
  junior developer"
- `## Important` — enforcement rules (no implementing during planning, no
  push without approval, etc.)

## Working with This Repository

When modifying or adding command templates:

- Keep the YAML frontmatter and section structure listed above.
- Use plain markdown (no XML-tag wrappers).
- Update `README.md` if adding or removing commands.
- Test new templates against a small, real-feature workflow.
- Follow the existing naming convention: short, descriptive names with no
  prefix.

## Important Notes

- This is a documentation/template repository — there is no build or test
  step.
- Files at the root should be copied to `~/.claude/commands/` for use with
  Claude Code.
- The workflow emphasizes incremental development with clear task tracking
  and explicit pause-for-approval gates between expensive steps.

