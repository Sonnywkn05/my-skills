# happy-path-journey-decomposition Specification

## Purpose
Define how the qa-engineer skill decomposes happy-path user journeys into structured, checkable elements before deriving test cases.

## Requirements

### Requirement: Happy-path journey decomposition as a pre-authoring step
The qa-engineer skill SHALL require a structured journey decomposition before writing test cases for any user-facing feature. The decomposition MUST produce: an entry point, a primary success path as an ordered step list, per-step intermediate checkpoints (state or data assertions valid at each step boundary), at least two alternative success variants, and identified multi-actor or system boundaries where control transfers between components, services, or roles.

#### Scenario: Decomposition precedes test case authoring
- **WHEN** a user asks the qa-engineer skill to write test cases for a feature or user story
- **THEN** the skill outputs a journey decomposition section before any test case table or scenario list, containing entry point, primary success path steps, and per-step checkpoints

#### Scenario: Alternative success variants are surfaced
- **WHEN** the journey decomposition is produced
- **THEN** it includes at least two named alternative success variants (e.g., "existing user vs. new user", "single item vs. bulk") that differ from the primary path in a testable way

#### Scenario: System and actor boundaries are identified
- **WHEN** the feature involves more than one service, role, or external system
- **THEN** the decomposition explicitly marks the step at which control crosses each boundary and names the boundary (e.g., "→ Payment Gateway", "→ Email Service")

### Requirement: Per-step intermediate checkpoints are concrete state assertions
Each step in the primary success path SHALL have an associated intermediate checkpoint. A checkpoint MUST describe a specific, observable system state or data condition that is true after that step completes and before the next step begins — not a description of what the step does.

#### Scenario: Checkpoints describe post-step state, not actions
- **WHEN** the primary success path lists a step such as "User submits order form"
- **THEN** the checkpoint for that step states the resulting state (e.g., "Order record exists in DB with status=PENDING; confirmation email enqueued") rather than restating the action

#### Scenario: Checkpoints are scoped to the step boundary
- **WHEN** a step involves multiple sub-actions
- **THEN** the checkpoint reflects only the state observable at the step's exit point, not intermediate internal states

### Requirement: Decomposition drives test case derivation
Test cases written after a journey decomposition SHALL trace back to decomposition elements. Each test case MUST be tagged with the decomposition element it exercises: primary path step, checkpoint, alternative variant, or system boundary.

#### Scenario: Test cases reference decomposition elements
- **WHEN** the skill produces test cases following a journey decomposition
- **THEN** each test case includes a tag or label identifying which decomposition element (step number, variant name, or boundary name) it covers

#### Scenario: Uncovered decomposition elements are flagged
- **WHEN** a decomposition element has no corresponding test case
- **THEN** the skill explicitly lists the uncovered element as a coverage gap rather than silently omitting it

## Evaluations

```json
{
  "query": "Write test cases for a checkout feature where a logged-in user adds items to a cart, enters shipping and payment details, and places an order.",
  "expected_behavior": [
    "Outputs a journey decomposition section before any test cases, listing entry point, ordered primary success path steps, and a per-step checkpoint for each step",
    "Includes at least two alternative success variants (e.g., 'guest checkout vs. logged-in', 'single item vs. multi-item cart')",
    "Marks at least one system boundary in the decomposition (e.g., '→ Payment Gateway' between payment submission and order confirmation)",
    "Each test case is tagged with the decomposition element it exercises (step number, variant name, or boundary name)"
  ]
}
```

```json
{
  "query": "Generate a test plan for a password-reset flow: user requests reset, receives email, clicks link, sets new password, and logs in with the new password.",
  "expected_behavior": [
    "Produces an ordered primary success path of at least five steps matching the described flow before listing test scenarios",
    "Each step in the primary path has an intermediate checkpoint describing observable state at that step's exit (e.g., 'Reset token written to DB with expiry=+1h; email enqueued')",
    "Identifies the email delivery step as a system boundary and names the external actor (e.g., '→ Email Service')",
    "Lists alternative success variants such as 'token near-expiry' or 'user with multiple active sessions'"
  ]
}
```

```json
{
  "query": "I need test cases for a multi-step onboarding wizard where an admin invites a user, the user accepts, completes a profile, and is granted role-based access.",
  "expected_behavior": [
    "Decomposes the journey into at least four primary path steps aligned to the described sequence before writing test cases",
    "Identifies the actor boundary where control transfers from admin to invited user and labels it explicitly",
    "Produces test cases that each carry a tag mapping them to a primary path step, checkpoint, alternative variant, or boundary",
    "Lists any decomposition element with no corresponding test case as an explicit coverage gap"
  ]
}
```