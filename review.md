# Code Review

Review uncommitted or recently committed git changes and provide critical
feedback to the engineer who wrote the code.

## Output
- **Format:** org-mode (`.org`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-[feature-name]-review.org` (e.g., `2025-05-25_user-profile-editing-review.org`).
  [feature-name] should be determined based on summary of changes.
* **Style:** Try and keep to 80 character row length. Trim empty characters in
  line ends. VERY IMPORTANT: Always end files with an empty line.

## Process
1. **Identify Files:** Identify the files which you need to review by examining
   changed git files using command `git diff --name-only`. If no changes are
   available, examine the last commit instead using `git log --name-only -1`.
2. **Write List:** Show user list of files to review with a one line
   description of the changes.
3. **Wait for Confirmation:** Pause and wait for the user to respond with "Go".
4. **Review Files:** For each file, review the contents and identify overall
   purpose for the file and main functionality contained within. Run `git diff`
   commands to identify the changes made.
5. **Review Changes:** For each file, review the changes made since last commit
   or in the last commit. Also review code around the changes to ensure you have
   the right context.
6. **Provide Feedback:** For each file, create a list of improvements that
   should be made. Focus on:
   - Potential bugs
   - Performance issues
   - Code duplication
   - Making code easy to understand
   - Adherence to style conventions
   - Missing documentation
   - Missing tests
5. **Generate Final Output:** Write out a list of files with a one line
   description for each and list of feedback items. Describe what needs to be
   done and why.

## Output Format
The generated task list _must_ follow this structure:

```org-mode
#+STARTUP: overview
#+TITLE: [feature-name] - Review
#+STARTUP: showall

High level description of the nature of the changes in this review.

- [ ] 1.0 [[file:path/to/file1.js][path/to/file1.js]] :: One line description [2/0]
  - [ ] 1.1 [Feedback item description]
  - [ ] 1.2 [Feedback item description]
- [ ] 2.0 [[file:path/to/file2.js][path/to/file2.js]] :: One line description [1/0]
  - [ ] 2.1 [Feedback item description]
```

## Interaction Model
The process explicitly requires a pause after generating initial file list to
get user confirmation ("Go") before proceeding to review file contents. This
ensures the high-level plan to review aligns with user expectations before
diving into details.

## Target Audience
Assume the primary reader of the task list is a **junior developer** who will
need to understand how to fix issues.

## Final instructions
- Do NOT start implementing the feedback.
