## 1. Implement config.yaml

- [x] 1.1 Add `context` block to `openspec/config.yaml` describing this as a skill-authoring repo, establishing evaluation-first development as the norm, and stating conciseness as a first-class constraint
- [x] 1.2 Add `rules.proposal` constraint requiring a **Baseline Measurement** section that declares what Claude does today (without the skill or change) before any implementation begins, with specific queries or scenarios where current behavior falls short
- [x] 1.3 Add `rules.specs` constraint requiring at least three evaluation scenarios per spec in the structured JSON format: `{ "query": "...", "expected_behavior": ["...", "..."] }` with observable, checkable expected behavior strings
- [x] 1.4 Add `rules.tasks` constraint requiring every task that writes or modifies skill content to include three explicit sub-steps: **Implement** (what file/content changes), **Observe** (fresh subagent + specific test query + expected signals), and **Measure** (pass criteria, fail criteria, failure branch back to Implement)

## 2. Observe — proposal rule

- [x] 2.1 **Implement**: confirm `config.yaml` is valid YAML (no syntax errors)
- [x] 2.2 **Observe**: spawn a fresh subagent with no context from this change; provide it the updated `config.yaml` rules and ask it to generate a proposal for a hypothetical skill change ("add coverage for happy-path user journeys to the qa-engineer skill"); capture the generated proposal
- [x] 2.3 **Measure**:
  - Pass: generated proposal includes a **Baseline Measurement** section naming specific queries where current behavior falls short
  - Fail: proposal is missing the section or the section is generic/vague → return to task 1.2, tighten the `rules.proposal` wording, repeat from 2.2

## 3. Observe — specs rule

- [x] 3.1 **Observe**: using the same hypothetical change, ask a fresh subagent to generate a spec given the updated `rules.specs`; capture the generated spec
- [x] 3.2 **Measure**:
  - Pass: spec contains ≥3 evaluation scenario JSON objects, each with a `query` string and an `expected_behavior` array of observable strings
  - Fail: scenarios are missing, fewer than three, use wrong format, or expected behaviors are abstract → return to task 1.3, sharpen the `rules.specs` wording, repeat from 3.1

## 4. Observe — tasks rule

- [x] 4.1 **Observe**: ask a fresh subagent to generate tasks for the same hypothetical change given the updated `rules.tasks`; capture the generated tasks
- [x] 4.2 **Measure**:
  - Pass: every task that modifies skill content has a clearly labelled Implement sub-step, an Observe sub-step naming the test query and expected signals, and a Measure sub-step with explicit pass/fail criteria and a failure branch
  - Fail: tasks are flat checkboxes with no sub-steps, or sub-steps are present but the Observe step does not specify a fresh subagent → return to task 1.4, add more explicit language about the fresh-subagent requirement, repeat from 4.1
