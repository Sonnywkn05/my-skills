## Context

The qa-engineer skill currently provides process guidance, testing dimensions, and output templates in a single file. It is effective for basic QA outputs, but it does not consistently guide depth decisions for high-risk areas or complex backend and performance testing. The change introduces deeper QA domain guidance while keeping the core skill concise through progressive disclosure.

## Goals / Non-Goals

**Goals:**
- Add domain-level QA guidance for risk-based test design, test data strategy, API/backend depth, performance tiers, and regression selection.
- Keep `skills/qa-engineer/SKILL.md` readable and execution-focused.
- Move heavier lookup material into reference files that can be consulted when needed.
- Preserve existing output templates while improving the decision quality behind them.

**Non-Goals:**
- Implement application runtime code changes.
- Introduce project-specific tooling automation for test execution.
- Redefine all existing QA terminology across other skills.

## Decisions

1. Keep execution flow in the core skill and externalize deep guidance.
   - Rationale: core instructions should stay short and trigger-friendly; heavy guidance is better as references.
   - Alternative considered: keep all guidance inline in `SKILL.md`. Rejected due to cognitive and token overhead.

2. Add explicit risk-tiering before scenario derivation.
   - Rationale: this ensures test depth is proportional to business and technical risk.
   - Alternative considered: rely on general "edge case" language. Rejected because depth decisions remain inconsistent.

3. Treat test data as a first-class planning concern.
   - Rationale: deterministic and privacy-safe data is required for repeatable QA outcomes.
   - Alternative considered: leave data handling implicit in test cases. Rejected because it produces flaky and incomplete plans.

4. Define backend/API and performance expectations as structured checklists.
   - Rationale: improves completeness for non-UI behavior and allows consistent pass/fail evaluation.
   - Alternative considered: single broad non-functional bullet list. Rejected due to ambiguity.

5. Use impact-based regression selection.
   - Rationale: balances speed and risk by focusing regression on changed components and dependency blast radius.
   - Alternative considered: full regression by default. Rejected as inefficient for routine changes.

## Risks / Trade-offs

- [Risk] Added guidance increases skill complexity for simple tasks. -> Mitigation: keep concise defaults in core and defer detailed material to references.
- [Risk] Reference documents may drift from core guidance over time. -> Mitigation: include periodic consistency review in maintenance tasks.
- [Risk] Teams may apply risk scoring inconsistently. -> Mitigation: define clear scoring bands and examples in references.
- [Risk] Performance tier guidance may be interpreted as mandatory in all contexts. -> Mitigation: define invocation criteria for each tier.

## Migration Plan

1. Update `skills/qa-engineer/SKILL.md` to incorporate core guidance hooks for the five depth areas.
2. Add reference documents under `skills/qa-engineer/references/` for detailed frameworks and checklists.
3. Ensure output templates reference relevant deep guidance when appropriate.
4. Validate the skill by running representative prompts for test plans, test cases, bug reports, and release sign-off.
5. Iterate wording for clarity and brevity based on prompt outcomes.

## Open Questions

- Should severity/priority calibration be included now or in a follow-up enhancement?
- Should accessibility depth be promoted to a sixth foundational area in this change?
- What level of org-specific policy should be encoded versus kept generic?
