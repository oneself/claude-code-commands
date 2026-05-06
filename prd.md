---
description: Generate a Product Requirements Document
argument-hint: [brief description of the feature]
---

# Generate a Product Requirements Document (PRD)

## Purpose

Create a detailed Product Requirements Document (PRD) in markdown based on an
initial user prompt. The PRD should be clear, actionable, and suitable for a
junior developer to understand and implement the feature.

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Receive initial prompt:** Read the brief description of the feature or
   functionality from `$ARGUMENTS`.
2. **Ask clarifying questions:** Before writing the PRD, ask questions to
   gather sufficient detail. Goal is to understand the "what" and "why", not
   the "how". Use the `AskUserQuestion` tool when available.
3. **Generate PRD:** Based on the initial prompt and the user's answers,
   generate a PRD using the structure outlined below.
4. **Save PRD:** Save as `[YYYY-MM-DD]-[feature-name]-prd.md` in the `/tasks/`
   directory. Get the current date by running `date +%Y-%m-%d`.

## Clarifying Questions (Examples)

Adapt questions to the prompt. Common areas:

- **Problem/Goal:** What problem does this feature solve? What is the main goal?
- **Target User:** Who is the primary user of this feature?
- **Core Functionality:** What key actions should a user be able to perform?
- **User Stories:** Could you provide user stories? (As a [user], I want to
  [action] so that [benefit].)
- **Acceptance Criteria:** How will we know when this feature is successful?
- **Scope/Boundaries:** Are there things this feature should NOT do (non-goals)?
- **Data Requirements:** What data does this feature need to display or
  manipulate?
- **Design/UI:** Are there existing mockups or UI guidelines? Describe the
  desired look and feel.
- **Edge Cases:** Are there potential edge cases or error conditions to
  consider?

## PRD Structure

The generated PRD must include the following sections:

1. **Introduction/Overview** — Briefly describe the feature and the problem it
   solves. State the goal.
2. **Goals** — List specific, measurable objectives for this feature.
3. **User Stories** — Detail user narratives describing feature usage and
   benefits.
4. **Functional Requirements** — List specific functionalities. Use clear
   language. Number each requirement.
5. **Non-Goals (Out of Scope)** — Clearly state what this feature will NOT
   include to manage scope.
6. **Design Considerations** *(optional)* — Link to mockups, describe UI/UX
   requirements, mention relevant components or styles.
7. **Technical Considerations** *(optional)* — Note known technical
   constraints, dependencies, or suggestions.
8. **Success Metrics** — How will the success of this feature be measured?
9. **Open Questions** — List only questions that require the user's input or
   decision. Do NOT use this section for design decisions, implementation
   notes, or explanations of how things work. If a question can be resolved by
   the author without user input, resolve it inline in the relevant section
   instead. Number open questions (1., 2., 3., ...). For each one, describe
   the issue, options if any, and a recommendation. If there are none, write
   "None."

## Target Audience

Assume the primary reader of the PRD is a **junior developer**. Requirements
should be explicit, unambiguous, and avoid jargon. Provide enough detail to
understand the feature's purpose and core logic. Avoid technical implementation
details.

## Output Format

- **Format:** markdown (`.md`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-[feature-name]-prd.md`
- **Style:** Keep to 80 character row length. Trim trailing whitespace. End
  files with an empty line.
- **Header:** Start the file with:

  ```markdown
  # [feature-name] - Product Requirements Document
  ```

## Important

- Do NOT start implementing the PRD.
- Make sure to ask clarifying questions before writing the PRD.
- Take the user's answers and improve the PRD.

