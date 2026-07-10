# EARS Notation Reference

**EARS** (Easy Approach to Requirements Syntax) is a constrained way of writing
requirements in plain language. Every requirement follows one of five patterns.
The patterns eliminate ambiguity by forcing each requirement to name its trigger,
its precondition, and the system response — and nothing else.

Use these rules when writing every functional requirement in `requirements.md`.

## Universal rules

- The system is always the subject and uses **SHALL** for obligations
  (**SHALL NOT** for prohibitions). Never "should", "must", "will", or "can".
- One requirement states **one** behavior. Split compound requirements.
- Requirements describe observable behavior — **the *what*, never the *how***.
  No stack, library, database, algorithm, or API names. Those belong in
  `design.md`.
- Keep the response testable: a reader must be able to write a pass/fail check
  from the sentence alone.
- Tag each requirement with its pattern, e.g. `**[EVENT]**`, so reviewers can
  see the shape at a glance.

## The five patterns

### 1. Ubiquitous

An always-active requirement — no trigger, no precondition. It holds for the
entire lifetime of the system.

**Template:**
> The `<system>` SHALL `<response>`.

**Examples:**
- The system SHALL store every transaction with a unique identifier.
- The system SHALL present all monetary values in the user's selected currency.

Use it for invariants and global properties. If you find yourself adding "when"
or "if", it is not ubiquitous — pick another pattern.

### 2. Event-driven

A response triggered by a discrete event or a completed action.

**Template:**
> WHEN `<trigger / event>`, the `<system>` SHALL `<response>`.

**Examples:**
- WHEN a user submits the registration form, the system SHALL send a
  verification email to the provided address.
- WHEN an order is confirmed, the system SHALL decrement the available stock for
  each purchased item.

Use it for the main "something happens → system reacts" behaviors.

### 3. State-driven

A response that stays in effect **while** the system is in a particular state.
The behavior is continuous for the duration of the state, not a one-time
reaction.

**Template:**
> WHILE `<in a state>`, the `<system>` SHALL `<response>`.

**Examples:**
- WHILE a payment is being processed, the system SHALL disable the "Pay" button.
- WHILE the user is offline, the system SHALL queue outgoing messages locally.

Contrast with event-driven: WHEN fires once at a transition; WHILE holds
throughout a state.

### 4. Unwanted-behavior

The system's response to errors, failures, invalid input, or any undesired
condition. This is the pattern for error handling, validation, and exception
behavior.

**Template:**
> IF `<unwanted condition>`, THEN the `<system>` SHALL `<response>`.

**Examples:**
- IF the payment gateway does not respond within the configured timeout, THEN
  the system SHALL cancel the transaction and notify the user.
- IF the uploaded file exceeds the maximum size, THEN the system SHALL reject it
  and report the allowed limit.
- IF a required field is empty on submission, THEN the system SHALL block
  submission and highlight the missing field.

Every failure-prone operation (external calls, I/O, parsing, network) should have
at least one unwanted-behavior requirement describing what happens when it fails.

### 5. Optional (feature-conditional)

A requirement that applies only **where** a particular feature, configuration, or
capability is present. Use it for behavior gated behind an optional feature — not
for "maybe we'll build this".

**Template:**
> WHERE `<feature / configuration is included>`, the `<system>` SHALL
> `<response>`.

**Examples:**
- WHERE two-factor authentication is enabled, the system SHALL require a
  second-factor code at login.
- WHERE the deployment includes an offline mode, the system SHALL synchronize
  pending changes once connectivity is restored.

Non-functional requirements that apply only under stated conditions often fit
this pattern, e.g. *WHERE the interface is public-facing, the system SHALL meet
WCAG 2.1 AA contrast requirements.*

## Combining patterns

Real requirements may combine an optional/state precondition with an event
trigger. Keep the ordering **WHERE → WHILE → WHEN → (IF) → the system SHALL**:

> WHERE audit logging is enabled, WHEN a record is deleted, the system SHALL
> write an audit entry naming the actor and the deleted record.

Only combine when each clause is genuinely needed. Prefer the simplest single
pattern that captures the behavior.

## Quick reference

| Pattern | Keyword | Use for |
|---|---|---|
| Ubiquitous | (none) | Always-true invariants |
| Event-driven | WHEN | Reaction to a discrete event |
| State-driven | WHILE | Continuous behavior during a state |
| Unwanted-behavior | IF … THEN | Errors, failures, invalid input |
| Optional | WHERE | Behavior gated by an optional feature |
