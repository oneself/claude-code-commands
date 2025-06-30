# Generating a Project Overview Document

Create or update a project overview document in org-mode format, based on user
input and the state of existing PRD files. The project overview should be clear
and suitable for a junior developer to understand.

## Process
1. **Find Existing Project Overview:** Look at the `/tasks` directory and see if
   there is a project overview file already defined. It should be called
   `*-overview.org`.
2. **Review PRDs**: Examine PRD files in the `/tasks` directory. These should be
   named `*-prd.org`. See which ones already appear in the project overview
   file and which do not. Focus on the ones that do not appear yet.
3. **Examine PRD File:** For each PRD file that is not referenced in the
   existing project overview file, identify the following:
   1. **Title:** One line title of the PRD.
   2. **Key Features:** 3-5 key features are defined in the PRD.
   3. **Status:** Examine corresponding tasks file (`*-tasks.org`) to determine
       task completion rate and determine feature status (e.g., not started, in
       progress, completed, partially completed, etc.).
4. **Project Overview**: Create or Update Project Overview (see section below).
5. **List of PRDs**: Create or Update List of PRDs.

## Create or Update Project Overview
* If project overview file does not exist, create it:
* **Location:** `/tasks/`
* **Filename:** `[project-name]-overview.org`
* **Header:** Start file with a org-mode header. Then write or update the
    "Goal" section for the project. Then write or update the "Technical Stack"
    section.
* **Format:** The project overview _must_ follow this structure:
```org-mode
#+STARTUP: overview
#+TITLE: [project-name] - Project Overview
#+STARTUP: showall

* Goal
[Project's goal and short description]

* Technical Stack
- [item 1]
- [item 2]
```

## Create or Update List of PRDs
* Add or update list of PRDs in the project overview file for each PRD file found.
* **Format:** The project overview _must_ follow this structure:
```org-mode
* [One line description of PRD]
- [[file:prd-file-name][prd-file-name]]
- [Status]
- [Key Feature Implemented 1]
- [Key Feature Implemented 2]
```

## Example of Project Overview File
```org-mode
#+STARTUP: overview
#+TITLE: Mineswpr - Project Overview
#+STARTUP: showall

* Goal
Build mobile-first Minesweeper game.

* Technical Stack
- Next.js + TypeScript + Tailwind CSS
- Custom hooks for state management and responsive design
- Comprehensive test suite with Jest + React Testing Library
- Cross-browser compatibility (Chrome, Firefox, Safari, Edge)

* Phase 1 Summary: Core Minesweeper Implementation
- [[file:2025-06-08-minesweeper-v1-prd.org][2025-06-08-minesweeper-v1-prd.org]]
- Status: ✅ 100% Complete - All 35 tasks completed across 5 major areas (setup, game logic, UI components, state management, responsive design)
- Responsive grid generation - Adapts to screen size at game start
- Core game mechanics - Mine placement (15% density), adjacent counting, cascade reveals
- Touch-optimized controls - Left-click/tap to reveal, right-click/long-press to flag
- Modern UI - Clean design with Tailwind CSS, 44px+ touch targets
- Complete game flow - Win/lose detection, reset functionality
```
