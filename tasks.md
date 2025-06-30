# Generate a Task List from a PRD

Create a detailed, step-by-step task list in org-mode format based on an
existing Product Requirements Document (PRD). The task list should guide a
junior developer through the implementation.

## Output
- **Format:** org-mode (`.org`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-[feature-name]-tasks.org` (e.g., `2025-05-25_user-profile-editing-tasks.org`)
* **Style:** Try and keep to 80 character row length. Trim empty characters in
  line ends. VERY IMPORTANT: Always end files with an empty line.

## Process
1. **Receive PRD Reference:** The user points the AI to a specific PRD file
2. **Analyze PRD:** The AI reads and analyzes the functional requirements, user
   stories, and other sections of the specified PRD.
3. **Phase 1: Generate Parent Tasks:** Based on the PRD analysis, create the
   file and generate the main, high-level tasks required to implement the
   feature. Use your judgment on how many high-level tasks to use. It's likely
   to be about 5. Present these tasks to the user in the specified format
   (without sub-tasks yet). Inform the user: "I have generated the high-level
   tasks based on the PRD. Ready to generate the sub-tasks? Respond with 'Go' to
   proceed."
4. **Wait for Confirmation:** Pause and wait for the user to respond with "Go".
5. **Phase 2: Generate Sub-Tasks:** Once the user confirms, break down each
   parent task into smaller, actionable sub-tasks necessary to complete the
   parent task. Ensure sub-tasks logically follow from the parent task and cover
   the implementation details implied by the PRD.
6. **Identify Relevant Files:** Based on the tasks and PRD, identify potential
   files that will need to be created or modified. List these under the
   `Relevant Files` section, including corresponding test files if applicable.
7. **Generate Final Output:** Combine the parent tasks, sub-tasks, relevant
   files, and notes into the final org-mode structure.
8. **Save Task List:** Save the generated document in the `/tasks/` directory
   with the filename `[YYYY-MM-DD]-[feature-name]-tasks.org`, where
   `[feature-name]` matches the base name of the input PRD file and [YYYY-MM-DD]
   is the current date (e.g., if the input was
   `2025-05-25_user-profile-editing-prd.org`, the output is
   `2025-05-26_user-profile-editing-tasks.org`).

## Output Format
The generated task list _must_ follow this structure:

```org-mode
#+STARTUP: overview
#+TITLE: [feature-name] - Task List
#+STARTUP: showall

* Relevant Files
- [[file:path/to/prd.org][path/to/prd.org]] :: Feature Name - Product Requirements Document
- [[file:path/to/potential/file1.ts][path/to/potential/file1.ts]] :: Brief description of why this file is relevant (e.g., Contains the main component for this feature).
- [[file:path/to/file1.test.ts][path/to/file1.test.ts]] :: Unit tests for =file1.ts=.
- [[file:path/to/another/file.tsx][path/to/another/file.tsx]] :: Brief description (e.g., API route handler for data submission).
- [[file:path/to/another/file.test.tsx][path/to/another/file.test.tsx]] :: Unit tests for =another/file.tsx=.
- [[file:lib/utils/helpers.ts][lib/utils/helpers.ts]] :: Brief description (e.g., Utility functions needed for calculations).
- [[file:lib/utils/helpers.test.ts][lib/utils/helpers.test.ts]] :: Unit tests for =helpers.ts=.

* Notes
- Unit tests should typically be placed alongside the code files they are testing (e.g., =MyComponent.tsx= and =MyComponent.test.tsx= in the same directory).
- Use =npx jest [optional/path/to/test/file]= to run tests. Running without a path executes all tests found by the Jest configuration.

* Tasks
- [ ] 1.0 Parent Task Title [2/0]
  - [ ] 1.1 [Sub-task description 1.1]
  - [ ] 1.2 [Sub-task description 1.2]
- [ ] 2.0 Parent Task Title [1/0]
  - [ ] 2.1 [Sub-task description 2.1]
- [ ] 3.0 Parent Task Title (may not require sub-tasks if purely structural or configuration)
```

## Interaction Model
The process explicitly requires a pause after generating parent tasks to get
user confirmation ("Go") before proceeding to generate the detailed
sub-tasks. This ensures the high-level plan aligns with user expectations before
diving into details.

## Target Audience
Assume the primary reader of the task list is a **junior developer** who will
implement the feature.
