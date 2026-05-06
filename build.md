---
description: Build the project and fix compilation errors and failing tests
---

# Build Project

## Purpose

Build a clean version of the project, then run tests, fixing any errors and
warnings along the way.

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Find the build and test commands:** Check the project's `README.md`,
   `CLAUDE.md`, `Makefile`, or `package.json` scripts to find the right
   commands. Common defaults are `make build` / `make test`,
   `npm run build` / `npm test`, or `bun run build` / `bun run test`. Ask
   the user if you cannot tell.
2. **Build:** Run the build command and fix any errors and warnings.
   Repeat until the build is clean.
3. **Test:** Run the test command and fix any failing tests and printed
   errors. Repeat until tests pass.

## Important

- Fix root causes. Do not silence warnings or skip failing tests just to
  get a green build.
- If a fix is non-trivial, stop and ask the user before making it.

