## Why

The `openspec/config.yaml` is currently empty beyond the schema declaration, so every artefact generated for this repo is guided only by OpenSpec's generic defaults. This repo is a skill-authoring workspace, and Claude's agent skills best practices prescribe an evaluation-first, observe-and-measure development cycle — but nothing in the config enforces or even encourages that pattern. As a result, proposals can be written without a baseline, tasks can be checked off without verifying behavior, and specs can be authored without evaluation scenarios.

## What Changes

- Add a `context` block to `config.yaml` establishing that this is a skill-authoring repo where evaluation-first development is the norm and conciseness is a first-class constraint
- Add `rules` for `proposal` requiring a **Baseline Measurement** section that defines what will be measured before implementation begins
- Add `rules` for `tasks` requiring every task that writes or modifies skill content to include three sub-steps: **Implement**, **Observe** (subagent query + expected signals), and **Measure** (pass/fail criteria with a failure branch back to Implement)
- Add `rules` for `specs` requiring at least three evaluation scenarios in the structured JSON format from the Claude best practices docs

## Capabilities

### New Capabilities

- `config-evaluation-rules`: The `context` and `rules` configuration in `config.yaml` that encodes evaluation-first principles and prescriptive observe-and-measure task structure for skill-authoring changes

### Modified Capabilities

<!-- none -->

## Impact

- `openspec/config.yaml` — sole file changed
- All future artefact generation for this repo will be shaped by the new context and rules
- No existing code, APIs, or runtime systems affected
