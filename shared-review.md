# Shared Code Review

Help a code reviewer understand the structure of the project, a component, a
file, a function, or a part of the project.

## Output
- **Format:** org-mode (`.org`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-[feature-name]-shared-review.org` (e.g., `2025-05-25_user-profile-editing-review.org`)
* **Style:** Try and keep to 80 character row length. Trim empty characters in
  line ends. VERY IMPORTANT: Always end files with an empty line.

## Process
1. **Identify Files:** Identify the main files which contain the functionality we
   need to review.
2. **Write List:** Show user list of files to review with a one line
   description.
3. **Wait for Confirmation:** Pause and wait for the user to respond with "Go".
4. **Review Files:** For each file, review the contents and identify overall
   purpose for the file and main functionality contained within.
5. **Generate Final Output:** Write out a list of files with a one line
   description for each and a paragraph describing the contents in more
   detail. Mention main functions, classes, or components that are need to
   understand what it does.

## Output Format
The generated task list _must_ follow this structure:

```org-mode
#+STARTUP: overview
#+TITLE: [feature-name] - Shared Review
#+STARTUP: showall

Detailed description of how the system works. Whenever a component name,
function name, variable name, etc is mentioned. Include the
[[file:path/to/file1.js][path/to/file1.js]] which it's defined in.

* [[file:path/to/file1.js][path/to/file1.js]] :: One line description
Paragraph long description.
* [[file:path/to/file2.js][path/to/file2.js]] :: One line description
Paragraph long description.
* [[file:path/to/file3.js][path/to/file3.js]] :: One line description
Paragraph long description.
```

## Interaction Model
The process explicitly requires a pause after generating initial file list to
get user confirmation ("Go") before proceeding to review file contents. This
ensures the high-level plan to review aligns with user expectations before
diving into details.


## Target Audience
Assume the primary reader of the task list is a **junior developer** who will
need to understand how this code works.
