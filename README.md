# Claude Code Commands

A collection of structured command templates for use with Claude Code to
streamline development workflows.

## Installation

Copy all `.md` files at the root to your Claude commands directory:

```bash
cp *.md ~/.claude/commands/
```

## Commands

### Task & Project Planning

- **prd.md** — Generate a Product Requirements Document (PRD) from a user
  prompt
- **tsd.md** — Generate a Technical Specification Document (TSD) from a PRD
- **tasks.md** — Generate a detailed task list from a PRD (and optional
  TSD)
- **impl.md** — Work through tasks one sub-task at a time with
  junior-developer safeguards

### Code Quality & Review

- **review.md** — Review uncommitted or recent git changes with critical
  feedback
- **pr-review.md** — Checkout and review a GitHub PR with a structured
  report
- **security-review.md** — Security review of pending changes on the
  current branch

### Development Workflow

- **build.md** — Build the project and fix compilation errors / failing
  tests
- **check.md** — Check task list status against actual code implementation
- **commit.md** — Commit staged code with a descriptive message

Each command is a self-contained markdown file with YAML frontmatter, a
purpose, an ordered process, an output format, and explicit interaction
gates where appropriate.

## How to Start?

The recommended flow:

1. **Create a PRD:** `/prd here is what I want you to build`
2. **Design the technical approach:**
   `/tsd @tasks/2026-05-05-feature-name-prd.md`
3. **Break down to tasks:**
   `/tasks @tasks/2026-05-05-feature-name-prd.md @tasks/2026-05-05-feature-name-tsd.md`
4. **Start implementation:**
   `/impl @tasks/2026-05-05-feature-name-tasks.md`
5. **Review before committing:** `/review`
   (or `/pr-review <PR>` / `/security-review` for deeper passes)
6. **Commit code:** `/commit`

