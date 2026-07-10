# Design — {{feature-name}}

> **Status:** {{Draft | Approved}} · **Last updated:** {{YYYY-MM-DD}}
> **Companion:** [requirements.md](./requirements.md) (the *what*)

> Technical design for {{feature-name}}. Describes *how* the system is built and
> behaves, satisfying the requirements in [requirements.md](./requirements.md).
> No implementation code lives here — this is the blueprint.

## Overview

{{Short technical summary: the shape of the solution, the chosen approach, and
how it maps to the requirements at a high level.}}

## Architecture

<!-- Describe the overall structure: layers, services, boundaries, and how they
     fit together. All diagrams in this document MUST use Mermaid. -->

```mermaid
flowchart TD
    {{architecture diagram — replace with the real components and edges}}
```

## Components

<!-- One subsection per component: its responsibility and its collaborators. -->

**`{{component 1}}`** — {{responsibility; which requirements it serves}}.

**`{{component 2}}`** — {{responsibility; which requirements it serves}}.

## Data flow

<!-- Conditional — include only when data movement is non-trivial. -->

{{How data moves through the system for the primary scenarios: inputs,
transforms, stores, outputs. Use a Mermaid sequence or flow diagram.}}

```mermaid
sequenceDiagram
    {{data-flow diagram — replace with the real actors and messages}}
```

## Data model

<!-- Conditional — include only if the feature has persistent or structured data. -->

{{Entities, their key fields, and relationships. No vendor-specific schema unless
the stack is fixed. Prefer a Mermaid `erDiagram` when relationships matter.}}

## Technical decisions

<!-- Record each significant choice AND its rationale. WHERE the user declined to
     decide a technical choice, state that the decision was made from the approved
     requirements and give the reasoning. -->

- **{{Decision — e.g. Stack / language}}:** {{choice}}. Rationale: {{why}}.
- **{{Decision — e.g. Storage}}:** {{choice}}. Rationale: {{why}}.
- **{{Decision — e.g. Error-handling strategy}}:** {{choice}}. Rationale: {{why}}.

## Testing strategy

<!-- Conditional — always include for buildable features; omit only for pure
     documentation specs. -->

{{How the system is verified: test levels (unit / integration / e2e), coverage
expectations, and how the acceptance criteria are exercised.}}

- {{test approach 1}}
- {{coverage expectation}}

## Requirement → design traceability

<!-- Every functional requirement group in requirements.md maps to at least one
     design element here. No requirement may be left unaddressed. -->

| Requirement group (`requirements.md`) | Satisfied by (design element) |
|---|---|
| {{requirement group 1}} | {{component / decision / step}} |
| {{requirement group 2}} | {{component / decision / step}} |
| {{requirement group N}} | {{component / decision / step}} |
