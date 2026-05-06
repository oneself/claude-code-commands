---
description: Commit staged code with a descriptive message
---

# Commit Code

## Purpose

Commit staged code with a descriptive message that a non-technical reader
can understand. Confirm scope with the user before committing or pushing.

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Review staged and unstaged files:** If there are unstaged files, show
   which ones you suggest including, then ask whether to stage them ("Stage
   suggested" or "Skip"). Generally prefer staging all related files in one
   commit.
2. **Check `.gitignore` candidates:** If any files look like they should be
   ignored (build artifacts, secrets, local config, etc.), ask whether to
   add them to `.gitignore` ("Add to .gitignore" or "Skip"). If none, skip
   this step.
3. **Review the staged diff:** Look at all staged additions, modifications,
   and deletions since the last commit so the message reflects the actual
   change.
4. **Draft the commit message:** Write a one-line high-level description
   followed by a bulleted list of important files and what changed in each.
   See the format below.
5. **Confirm and commit:** Show the user the drafted message and ask
   whether to commit ("Commit" or "Cancel"). On confirmation, run
   `git commit`.
6. **Ask about pushing:** Ask whether to push to origin ("Push" or "Don't
   push"). If "Push", run `git push`.

## Output Format

```
[One-line description of the change.]

- [file1]: [Description of changes in file1]
- [file2]: [Description of changes in file2]
...
```

## Guidelines

- Start with a high-level description of the change.
- Only list important files and what changed in each.
- Focus on the most significant changes; not every file needs mention.
- The message should be clear for someone non-technical to understand.

## Important

- All files MUST be either committed or added to `.gitignore`.
- NEVER commit or push without explicit user confirmation in steps 5 and 6.
- NEVER use `git push --force` or `--force-with-lease` unless the user
  explicitly asks for it.

