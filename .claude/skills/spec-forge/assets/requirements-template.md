# Requirements — {{feature-name}}

> **Status:** {{Draft | Approved}} · **Last updated:** {{YYYY-MM-DD}}
> **Companion:** [design.md](./design.md) (the *how*)

> {{One- or two-line summary of what this feature/project is and the problem it
> solves. No technology — the *what*, not the *how*.}}

## Overview

{{Short prose description of the feature: who uses it, its purpose, and the core
value it delivers. Keep it technology-free.}}

## Functional Requirements (EARS)

<!-- Every requirement below uses EARS notation. Tag each with its pattern.
     See references/ears-notation.md for the five patterns. -->

### {{Requirement group 1 — e.g. "Activation & input"}}
- **[UBIQUITOUS]** The system SHALL {{response}}.
- **[EVENT]** WHEN {{trigger}}, the system SHALL {{response}}.

### {{Requirement group 2}}
- **[STATE]** WHILE {{state}}, the system SHALL {{response}}.
- **[UNWANTED]** IF {{unwanted condition}}, THEN the system SHALL {{response}}.

### {{Requirement group N}}
- **[OPTIONAL]** WHERE {{feature/configuration}}, the system SHALL {{response}}.

## Non-functional Requirements

<!-- Conditional — include ONLY categories relevant to this context (performance,
     security, scalability, accessibility, observability). Delete this section
     entirely if no NFR category is relevant — do not add generic boilerplate. -->

### {{Relevant NFR category — e.g. "Performance"}}
- **[UBIQUITOUS]** The system SHALL {{measurable constraint, e.g. respond within
  N ms at the P95 percentile under the stated load}}.

### {{Relevant NFR category — e.g. "Security"}}
- **[EVENT]** WHEN {{trigger}}, the system SHALL {{security response}}.

## Error & exception behavior

<!-- Capture expected behavior for each failure-prone operation (external calls,
     I/O, parsing). Written as unwanted-behavior requirements. -->

- **[UNWANTED]** IF {{external dependency fails / times out}}, THEN the system
  SHALL {{recovery / notification response}}.

## Acceptance criteria

{{Bullet list of concrete, checkable outcomes that confirm the requirements are
met. Each should be pass/fail verifiable.}}

- {{criterion 1}}
- {{criterion 2}}

## Out of scope (non-goals)

{{What this feature explicitly does NOT do, to bound expectations.}}

- {{non-goal 1}}
- {{non-goal 2}}
