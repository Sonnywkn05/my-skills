# config-evaluation-rules Specification

## Purpose
Define the configuration rules in `openspec/config.yaml` that enforce evaluation-first development and the observe-and-measure task structure for skill-authoring changes.

## Requirements

### Requirement: Config provides evaluation-first project context
The `openspec/config.yaml` SHALL include a `context` block that identifies this as a skill-authoring repository, establishes that evaluation-first development is the norm, and states that conciseness is a first-class constraint for all generated artefacts.

#### Scenario: Proposal generation reflects evaluation-first framing
- **WHEN** an AI agent generates a proposal artefact for this repo
- **THEN** the generated proposal treats evaluation and observable outcomes as a primary concern, not an afterthought

#### Scenario: Context discourages over-documentation
- **WHEN** an AI agent generates any artefact for this repo
- **THEN** the output avoids adding explanations, rationale, or content the agent already knows, defaulting to minimal necessary content

#### Scenario: Context is present and non-empty
- **WHEN** `openspec/config.yaml` is read
- **THEN** it contains a populated `context` field describing the repo's purpose and governing principles

### Requirement: Proposal rules require a baseline measurement section
The `openspec/config.yaml` `rules.proposal` SHALL require every proposal to include a **Baseline Measurement** section that declares what the agent does today (without the skill or change) before any implementation begins.

#### Scenario: Baseline declared before implementation
- **WHEN** an AI agent generates a proposal artefact
- **THEN** the proposal includes a Baseline Measurement section describing current observed behavior and the gap being addressed

#### Scenario: Baseline is specific, not generic
- **WHEN** the Baseline Measurement section is present
- **THEN** it names specific queries or scenarios where the current behavior falls short, not vague statements like "the agent doesn't do this yet"

#### Scenario: Missing baseline is a rule violation
- **WHEN** a proposal artefact is generated without a Baseline Measurement section
- **THEN** the artefact does not satisfy the `rules.proposal` constraint

### Requirement: Spec rules require structured evaluation scenarios
The `openspec/config.yaml` `rules.specs` SHALL require every spec to include at least three evaluation scenarios in the structured JSON format: `{ "query": "...", "expected_behavior": ["...", "..."] }`.

#### Scenario: Evaluation scenarios are present in every spec
- **WHEN** an AI agent generates a spec artefact
- **THEN** the spec includes an Evaluations section with a minimum of three JSON scenario objects

#### Scenario: Scenarios use the required format
- **WHEN** evaluation scenarios are written in a spec
- **THEN** each scenario object contains a `query` string and an `expected_behavior` array of observable, checkable strings

#### Scenario: Expected behaviors are concrete and observable
- **WHEN** the `expected_behavior` array is populated
- **THEN** each entry describes a specific action or output that can be verified by observation (e.g., "Assigns a risk tier before writing test cases"), not abstract qualities (e.g., "Works correctly")

### Requirement: Task rules require observe-and-measure sub-steps on skill content tasks
The `openspec/config.yaml` `rules.tasks` SHALL require that every task which writes or modifies skill content (SKILL.md or any file in a skill directory) includes three explicit sub-steps: **Implement**, **Observe**, and **Measure**.

#### Scenario: Implement sub-step describes the content change
- **WHEN** a task modifies skill content
- **THEN** the Implement sub-step specifies exactly what file is changed and what content is added or modified

#### Scenario: Observe sub-step uses a fresh subagent
- **WHEN** the Implement sub-step is complete
- **THEN** the Observe sub-step instructs the executor to spawn a fresh subagent (with no context from the current change), provide the updated skill content, and run a specific test query derived from the spec's evaluation scenarios

#### Scenario: Observe sub-step names expected signals
- **WHEN** the Observe sub-step is defined
- **THEN** it lists the specific observable signals to watch for in the subagent's response (e.g., "Did it assign a risk tier before writing test cases?")

#### Scenario: Measure sub-step defines pass and fail
- **WHEN** the Observe sub-step has been executed
- **THEN** the Measure sub-step provides explicit pass criteria, explicit fail criteria, and a failure branch instruction (e.g., "If fail: return to Implement, note what signal was missing")

#### Scenario: Failure branch prevents premature task completion
- **WHEN** the Measure sub-step evaluates the observation as a fail
- **THEN** the task is not marked complete and the executor returns to the Implement sub-step with a specific note about the gap
