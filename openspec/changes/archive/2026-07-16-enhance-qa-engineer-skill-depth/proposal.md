## Why

The current qa-engineer skill provides strong structure and templates, but it lacks deeper QA domain guidance needed for consistently high-quality planning and coverage decisions. Enhancing domain depth now will improve output quality and make the skill more useful for complex testing scenarios.

## What Changes

- Add core guidance for risk-based test design so scope and depth are prioritized by risk.
- Add explicit test data strategy guidance (data setup, masking, reset/cleanup, and determinism).
- Expand API/backend QA guidance to include contract, idempotency, pagination, retry, and timeout coverage.
- Add performance testing tiers with practical usage and pass/fail framing.
- Add regression selection strategy based on impact and dependency blast radius.
- Introduce progressive disclosure by separating heavy guidance into reference documents while keeping execution flow concise in the skill.

## Capabilities

### New Capabilities
- `qa-engineer-skill-depth`: Defines deeper QA domain guidance and reference structure for the qa-engineer skill.

### Modified Capabilities
- None.

## Impact

- Affected files: `skills/qa-engineer/SKILL.md` and new supporting reference files under `skills/qa-engineer/`.
- No runtime code or API contract changes; impact is on skill behavior and output quality.
- Improves consistency for QA planning, scenario derivation, and release-readiness recommendations.
