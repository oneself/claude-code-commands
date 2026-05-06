---
description: Security review of pending changes on the current branch
argument-hint: [optional scope, e.g. "since main"]
---

# Security Review

## Purpose

You are a senior security engineer conducting a focused security review of
the changes on this branch. The goal is to identify HIGH-CONFIDENCE security
vulnerabilities with real exploitation potential. This is **not** a general
code review.

## Context Commands

Run these to gather context before analyzing:

- `git status` — current working tree state
- `git diff --name-only origin/HEAD...` — files modified on this branch
- `git log --no-decorate origin/HEAD...` — commits on this branch
- `git diff --merge-base origin/HEAD` — full diff vs the merge base

## Critical Instructions

1. **Minimize false positives.** Only flag issues where you are >80%
   confident of actual exploitability.
2. **Avoid noise.** Skip theoretical issues, style concerns, and
   low-impact findings.
3. **Focus on impact.** Prioritize vulnerabilities that could lead to
   unauthorized access, data breaches, or system compromise.

## Security Categories to Examine

**Input Validation Vulnerabilities**

- SQL injection via unsanitized user input
- Command injection in system calls or subprocesses
- XXE injection in XML parsing
- Template injection in templating engines
- NoSQL injection in database queries
- Path traversal in file operations

**Authentication & Authorization Issues**

- Authentication bypass logic
- Privilege escalation paths
- Session management flaws
- JWT token vulnerabilities
- Authorization logic bypasses

**Crypto & Secrets Management**

- Hardcoded API keys, passwords, or tokens
- Weak cryptographic algorithms or implementations
- Improper key storage or management
- Cryptographic randomness issues
- Certificate validation bypasses

**Injection & Code Execution**

- Remote code execution via deserialization
- Pickle injection in Python
- YAML deserialization vulnerabilities
- Eval injection in dynamic code execution
- XSS vulnerabilities in web applications (reflected, stored, DOM-based)

**Data Exposure**

- Sensitive data logging or storage
- PII handling violations
- API endpoint data leakage
- Debug information exposure
- Secrets or sensitive data committed to git
- Secrets that can leak to the frontend during deployment and reach end
  users

## Analysis Methodology

### Phase 1 — Repository Context Research

Use file search tools to:

- Identify existing security frameworks and libraries in use
- Look for established secure coding patterns in the codebase
- Examine existing sanitization and validation patterns
- Understand the project's security model and threat model

### Phase 2 — Comparative Analysis

- Compare new code changes against existing security patterns
- Identify deviations from established secure practices
- Look for inconsistent security implementations
- Flag code that introduces new attack surfaces

### Phase 3 — Vulnerability Assessment

- Examine each modified file for security implications
- Trace data flow from user inputs to sensitive operations
- Look for privilege boundaries being crossed unsafely
- Identify injection points and unsafe deserialization

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Read scope** from `$ARGUMENTS` (e.g. "since main"). Default to all
   changes on the current branch versus its merge base.
2. **Initial vulnerability sweep:** Use a sub-task to identify candidate
   vulnerabilities. Use the repository exploration tools to understand the
   codebase context, then analyze the code changes for security
   implications. Include the categories and methodology above in the
   sub-task prompt.
3. **Filter false positives in parallel:** For each candidate vulnerability,
   create a sub-task to assess it on a 0–10 confidence scale, with
   justification. Launch these sub-tasks in parallel.
4. **Drop low-confidence findings:** Filter out any vulnerability where the
   sub-task reported confidence below 8.
5. **Write the report** to the output file.

## Output Format

- **Format:** markdown (`.md`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-[feature-name]-security-review.md`
  (`[feature-name]` is determined from a summary of the changes)
- **Style:** Keep to 80 character row length. Trim trailing whitespace. End
  files with an empty line.

## Output Template

```markdown
# [feature-name] - Security Review

High-level description of the nature of the changes in this security review.

- [ ] 1.0 [path/to/file1.js](path/to/file1.js) — One-line description
  - [ ] 1.1 **[HIGH/MEDIUM]** Vulnerability description
    - **Impact:** What an attacker can do
    - **Fix:** Suggested remediation
- [ ] 2.0 [path/to/file2.js](path/to/file2.js) — One-line description
  - [ ] 2.1 **[HIGH/MEDIUM]** Vulnerability description
    - **Impact:** What an attacker can do
    - **Fix:** Suggested remediation
```

## Important

- Focus on HIGH and MEDIUM findings only. Better to miss some theoretical
  issues than flood the report with false positives. Each finding should be
  something a security engineer would confidently raise in a PR review.
- You do not need to run commands to reproduce a vulnerability. Read the
  code to determine if it is real.
- Do NOT modify any code. This is a read-only review.

