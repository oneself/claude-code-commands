# Claude Code Commands

A collection of structured command templates for use with Claude Code to
streamline development workflows.

## Installation

Copy all `.md` files to your Claude commands directory:

```bash
cp *.md ~/.claude/commands/
```

## Commands

### Project Management

- **build.md**: Build project and fix compilation errors/warnings
- **check.md**: Check task list status against actual code implementation
- **start.md**: Start a new coding session and understand project state

### Code Quality & Review

- **review.md**: Review uncommitted/recent git changes with critical feedback
- **shared-review.md**: Generate project structure documentation for code reviewers
- **write-review.md**: Create structured code review documentation

### Task & Project Planning

- **prd.md**: Generate Product Requirements Document (PRD) from user prompts
- **prj.md**: Create/update project overview document from existing PRDs
- **tasks.md**: Generate detailed task lists from PRD files
- **impl.md**: Task implementation with junior developer guidance
- **learn.md**: Progressive teaching approach for junior developers

### Development Workflow

- **commit.md**: Commit code to GitHub with structured commit messages
- **sc.md**: Review latest screenshot in screenshots directory

Each command includes detailed process steps, output formats, and interaction
models tailored for structured development workflows.

## How to Start?

I usually follow this flow:

0. **Start a session**: `/start`
1. **Create a PRD**: `/prd here is what I want you to build`
2. **Break down to tasks**: `/tasks @tasks/2025-06-15_feature-name-prd.org`
3. **Start implementation**: `/impl @tasks/2025-06-15_feature-name-tasks.org`
4. **Commit code**: `/commit`
