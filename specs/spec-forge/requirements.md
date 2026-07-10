# Requirements — spec-forge

> A Claude Code skill that turns an initial prompt into an SDD specification
> (EARS requirements + technical design), asking clarifying questions when the
> context is insufficient.

## Overview

`spec-forge` takes a natural-language description of a feature or project and
produces two versionable artifacts: `requirements.md` (the *what*, in EARS
notation) and `design.md` (the *how*, technical). When the initial prompt is
ambiguous or incomplete, the skill narrows down with precise, essential questions
before generating any file.

## Functional Requirements (EARS)

### Activation & input assessment
- **[UBIQUITOUS]** The skill SHALL produce a specification composed of two artifacts: `requirements.md` (EARS requirements) and `design.md` (technical design).
- **[EVENT]** WHEN the user provides a prompt describing a feature or project, the skill SHALL assess whether the context is sufficient to generate the spec.

### Clarification gate (the *what*)
- **[UNWANTED]** IF the initial prompt is vague, incomplete, or ambiguous, THEN the skill SHALL ask clarifying questions before generating any file.
- **[UNWANTED]** IF clarification is needed, THEN the skill SHALL ask only the essential questions required to remove ambiguity, avoiding anything inferable from the context already provided.
- **[STATE]** WHILE essential ambiguities remain unresolved, the skill SHALL stay in the clarification phase and SHALL NOT generate the spec files.

### Requirements generation
- **[UBIQUITOUS]** The skill SHALL write every functional requirement in EARS notation.
- **[UBIQUITOUS]** The skill SHALL write the generated specification in English, regardless of the prompt's language.
- **[EVENT]** WHEN generating requirements, the skill SHALL include acceptance criteria and cover edge cases and error conditions.
- **[UNWANTED]** IF the user includes implementation details (stack, library, database) in the description, THEN the skill SHALL move them to `design.md` and keep `requirements.md` technology-free.

### Non-functional requirements (relevance-gated)
- **[OPTIONAL]** WHERE the user states non-functional constraints (performance, security, scalability, accessibility), the skill SHALL record them as dedicated EARS requirements.
- **[UNWANTED]** IF the user does not mention non-functional requirements, THEN the skill SHALL assess which NFR categories are relevant to the described context and ask about those only.
- **[UBIQUITOUS]** The skill SHALL base NFR relevance on context signals — e.g., accessibility when the software is user-facing or serves specific audiences; performance/scalability when large scale is implied; security when the system leaves a local or trusted boundary.
- **[UNWANTED]** IF an NFR category is not relevant to the context, THEN the skill SHALL NOT add it, avoiding generic non-functional boilerplate.

### Quality & robustness
- **[EVENT]** WHEN a requirement involves an external dependency or a failure-prone operation, the skill SHALL specify the expected error/exception behavior as an EARS unwanted-behavior requirement.
- **[UNWANTED]** IF observability is relevant to the context (e.g., a running service rather than a one-off script), THEN the skill SHALL ask whether logging/monitoring requirements should be captured, and record the relevant ones.
- **[UBIQUITOUS]** The skill SHALL treat error handling, logging, and observability as behavior and NFRs within the spec — not as implementation details deferred entirely to code.

### Requirements review checkpoint
- **[EVENT]** WHEN the requirements are drafted, the skill SHALL present them for user review before producing the design.
- **[EVENT]** WHEN the user approves the requirements, the skill SHALL proceed to the technical design.

### Design clarification & generation (the *how*)
- **[EVENT]** WHEN starting the design, the skill SHALL ask the essential technical questions needed to shape it — e.g., preferred stack, testing approach, and coverage expectations.
- **[OPTIONAL]** WHERE the user prefers not to decide a given technical choice, the skill SHALL decide based on the approved requirements AND document the decision and its rationale in `design.md`.
- **[EVENT]** WHEN the requirements are approved and technical direction is set, the skill SHALL generate `design.md` covering architecture, components, data flow, testing strategy, and technical decisions that satisfy each requirement.
- **[UBIQUITOUS]** The skill SHALL ensure every functional requirement maps to at least one design element (requirement → design traceability).

### Artifact output
- **[UBIQUITOUS]** The skill SHALL write the artifacts to `specs/<feature-name>/` as `requirements.md` and `design.md`.
- **[UNWANTED]** IF a `specs/<feature-name>/` folder already exists, THEN the skill SHALL warn the user and request confirmation before overwriting.
- **[UNWANTED]** IF the request spans multiple distinct features, THEN the skill SHALL suggest splitting them into separate specs.

## Acceptance criteria

- A well-detailed prompt produces `requirements.md` + `design.md` with no unnecessary questions.
- A vague prompt triggers clarifying questions — and only the essential ones.
- No functional requirement appears outside EARS notation.
- `requirements.md` contains no technology decisions; those live in `design.md`.
- Non-functional requirements appear only when relevant to the context — never as generic boilerplate.
- Error/exception behavior is captured for failure-prone operations.
- Every requirement is traceable to a corresponding design element.

## Out of scope (non-goals)

- The skill does NOT generate implementation code — it stops at design.
- The skill does NOT produce the task breakdown (`tasks.md`) — planned as a future iteration.
- The skill does NOT execute or validate the generated code.