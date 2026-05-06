---
description: Generate a Technical Specification Document from a PRD
argument-hint: [path to prd file]
---

# Generate a Technical Specification Document (TSD)

## Purpose

Create a detailed Technical Specification Document (TSD) in markdown based on
an existing Product Requirements Document (PRD). The TSD outlines the system
design, technical approach, and architectural decisions needed to implement
the feature. It bridges the gap between "what to build" (PRD) and "how to
build it step by step" (task list).

## Process

Steps must be executed in numerical order. Complete each step before moving to
the next.

1. **Receive PRD reference:** Read the PRD path from `$ARGUMENTS`.
2. **Analyze PRD:** Read and understand the goals, user stories, functional
   requirements, and constraints defined in the PRD.
3. **Ask clarifying questions:** Before writing the TSD, ask technical
   questions to gather sufficient detail about the existing system and the
   desired approach. Use the `AskUserQuestion` tool when available.
4. **Phase 1 — Generate high-level architecture:** Present the proposed system
   design, key components, and data flow at a high level. Do NOT include
   implementation details yet. Then ask whether to proceed with the detailed
   specification ("Go" or "Wait").
5. **Wait for confirmation:** Pause and wait for the user to respond with
   "Go" before continuing.
6. **Phase 2 — Generate full TSD:** Expand the high-level architecture into
   the complete specification using the structure outlined below.
7. **Save TSD:** Save as `[YYYY-MM-DD]-[feature-name]-tsd.md` in `/tasks/`,
   where `[feature-name]` matches the base name of the input PRD file. Get
   the current date by running `date +%Y-%m-%d`.

## Clarifying Questions (Examples)

Adapt questions to the feature. Common areas:

- **Current Architecture:** What does the relevant part of the existing
  system look like?
- **Tech Stack:** Are there technology or framework constraints to follow?
- **Data Model:** Are there existing data models or schemas this feature
  interacts with?
- **API Conventions:** Are there existing API patterns or conventions to
  follow?
- **Authentication/Authorization:** Are there auth requirements for this
  feature?
- **Third-Party Dependencies:** Does this feature rely on external services
  or libraries?
- **Performance:** Are there performance requirements or expected scale?
- **Migration:** Does this feature require data migration or backward
  compatibility?
- **Testing Strategy:** Are there specific testing requirements or patterns
  in use?

## TSD Structure

The generated TSD must include the following sections:

1. **Overview** — Briefly restate the feature goal from the PRD. Describe the
   technical approach at a high level.
2. **Architecture** — Describe the system architecture for this feature.
   Include component relationships, data flow, and integration with the
   existing system. Use ASCII diagrams where helpful.
3. **Data Model** — Define new or modified data models, schemas, and their
   relationships. Include field names, types, constraints, and indexes.
4. **API Design** — Specify API endpoints, request and response shapes,
   status codes, and error handling. Follow existing project conventions.
5. **Logic and Processing** — Describe core business logic, algorithms, and
   data transformations. Explain decision points and processing flows.
6. **Security and Authorization** — Outline authentication, authorization,
   input validation, and other security considerations relevant to this
   feature.
7. **Error Handling** — Define expected error states, how they are surfaced
   to the user, and recovery strategies.
8. **Performance Considerations** *(optional)* — Note caching strategies,
   query optimization, rate limiting, or other performance decisions.
9. **Dependencies** — List new libraries, services, or infrastructure
   changes required.
10. **Testing Strategy** — Outline the testing approach: unit tests,
    integration tests, and any manual testing steps. Note edge cases to
    cover.
11. **Open Questions** — List only questions that require the user's input
    or decision. Do NOT use this section for design decisions, implementation
    notes, or explanations of how things work. Number them (1., 2., 3., ...).
    For each one, describe the issue, options if any, and a recommendation.
    If there are none, write "None."

## Target Audience

Assume the primary reader of the TSD is a **junior developer**. The
specification should be explicit and avoid unexplained jargon. Provide enough
context to understand why each technical decision was made, not just what the
decision is.

## Output Format

- **Format:** markdown (`.md`)
- **Location:** `/tasks/`
- **Filename:** `[YYYY-MM-DD]-[feature-name]-tsd.md`
- **Style:** Keep to 80 character row length. Trim trailing whitespace. End
  files with an empty line.
- **Header:** Start the file with:

  ```markdown
  # [feature-name] - Technical Specification Document

  > PRD: [path/to/prd.md](path/to/prd.md)
  ```

## Interaction Model

The process requires a pause after presenting the high-level architecture.
Get user confirmation before generating the detailed specification. This
ensures the technical direction aligns with expectations before investing in
details.

## Important

- Do NOT start implementing anything.
- The TSD describes technical design, not implementation steps (that is the
  task list's job).
- Make sure to ask clarifying questions about the existing system.
- Take the user's answers and improve the TSD.

