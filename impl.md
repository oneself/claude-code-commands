# Task List Management

Guidelines for managing task lists in markdown files to track progress on completing a PRD.

## Task Implementation
- **One sub-task at a time:** Do **NOT** start the next sub‑task until you ask
  the user for permission and they say "yes" or "y"
- **Completion protocol:**
  1. When you finish a **sub‑task**, immediately mark it as completed by changing `[ ]` to `[X]`.
  2. If **all** subtasks underneath a parent task are now `[X]`, also mark the **parent task** as completed.
- Stop after each sub‑task and wait for the user’s go‑ahead.

## Task List Maintenance
1. **Update the task list as you work:**
   - Mark tasks and subtasks as completed (`[X]`) per the protocol above.
   - Add new tasks as they emerge.

2. **Maintain the "Relevant Files" section:**
   - List every file created or modified.
   - Give each file a one‑line description of its purpose.

## AI Instructions
When working with task lists, the AI must:

1. Regularly update the task list file after finishing any significant work.
2. Follow the completion protocol:
   - Mark each finished **sub‑task** `[X]`.
   - Mark the **parent task** `[X]` once **all** its subtasks are `[X]`.
3. Add newly discovered tasks.
4. Keep “Relevant Files” accurate and up to date.
5. Before starting work, check which sub‑task is next.
6. After implementing a sub‑task, update the file and then pause for user approval.

## Code Style
- Focus on readability.
- Try and keep to 120 character row length.
- Trim empty characters in line ends.
- IMPORTANT: Always end files with an empty line.

## Images
- DO NOT attempt to generate images, (e.g. SVG, favicon.ico, etc.).
- If an image is needed, add a placeholder with the image path and a descriptive
  `alt` tag.
- Then add the image to an image tasks file called
  `[YYYY-MM-DD]-[feature-name]-images.org` in the `/tasks/` directory, where
  `[feature-name]` matches the base name of the input PRD file and [YYYY-MM-DD]
  is the current date (e.g., if the input was
  `2025-05-25_user-profile-editing-prd.org`, the output is
  `2025-05-26_user-profile-editing-images.org`).
### Images Output Format
The generated task list _must_ follow this structure:

```org-mode
## Images
- [ ] =[path-to-image1]= :: Alt description of image 1
- [ ] =[path-to-image2]= :: Alt description of image 2
```
### Updating Generated Image Status
- If an image file exists in the path specified in the images tasks file. Marked
  it as completed with a `[X]` mark.
