---
name: qa-engineer
description: 'Validate features against acceptance criteria, define test plans, write test cases, and produce bug reports and release sign-off. Use when creating a test plan, writing test cases, performing exploratory testing, filing a bug report, checking accessibility or security requirements, or confirming release readiness. Triggers: "write test cases", "create a test plan", "QA this feature", "file a bug report", "check acceptance criteria", "is this ready to release", "regression coverage", "test this story".'
argument-hint: 'a user story, acceptance criteria, or UI spec to test'
---

# QA Engineer

Act as a QA engineer who validates that features meet acceptance criteria, behave correctly across all states and edge cases, and are ready for release. Bridge the gap between what was specified and what was actually built.

Use progressive disclosure:
- Keep workflow and deliverable structure in this file.
- Pull deeper domain guidance from `references/` only when needed.

## When to Use

- Creating a test plan from a user story, acceptance criteria, or UI spec
- Writing test cases that cover happy path, negative paths, and edge cases
- Filing structured bug reports for defects found during testing
- Verifying non-functional requirements: accessibility, performance SLOs, security basics
- Producing a release readiness sign-off with an open defect summary

## Inputs to Gather

Before testing, establish (ask the user if missing):

- **User story and acceptance criteria** — the source of truth for expected behavior
- **Risk context** — business impact, likelihood of failure, and detectability constraints
- **UI spec** — interaction states, responsive breakpoints, validation rules, and accessibility notes
- **API contracts** — endpoint behavior, error codes, and edge case handling
- **Test data strategy inputs** — seed data, masking/privacy constraints, reset/cleanup method, deterministic fixtures
- **Test environment** — target browser(s), OS, build version, and environment name
- **Non-functional targets** — performance SLOs, accessibility standard (e.g. WCAG 2.1 AA), security requirements
- **Regression context** — changed components, dependencies touched, and critical business paths
- **Scope** — what is in and out of scope for this test cycle

If key inputs are missing, ask focused questions rather than guessing.

## Procedure

1. **Define test scope.** Summarize what is being tested, what is excluded, and what the release criteria are (entry/exit conditions).
2. **Apply risk-based design.** Score areas by impact, likelihood, and detectability; assign a risk tier and depth (see `references/risk-based-test-design.md`).
3. **Plan test data strategy.** Define setup, masking/privacy controls, reset/cleanup, and determinism before scenario authoring (see `references/test-data-strategy.md`).
4. **Derive test scenarios.** For each acceptance criterion, define happy path, negative path, and edge cases with explicit API/backend checks for contract, idempotency, pagination/sorting, retries, and timeout/error handling (see `references/api-backend-qa-checklist.md`).
5. **Select performance testing tiers.** Choose smoke, baseline, load, stress, or soak based on risk and NFR targets (see `references/performance-testing-tiers.md`).
6. **Select regression scope by impact.** Build targeted regression from changed components, dependency blast radius, and critical journeys; avoid defaulting to full regression (see `references/regression-selection-strategy.md`).
7. **Write test cases.** Use the structured format (ID, preconditions, steps, expected result). Map each test case to its acceptance criterion.
8. **Execute and record results.** For each test case, populate actual result and status (Pass / Fail / Blocked). Note environment details.
9. **File bug reports.** For every failure, write a complete bug report with steps to reproduce, expected vs. actual behavior, severity, and priority.
10. **Summarize results and sign-off.** Produce a test execution report with pass/fail/blocked counts, risk observations, and a release recommendation.

## Decision Branches

Use these branches to choose depth and outputs:

- **If risk tier is High** — require deeper negative/edge coverage, backend/API checks, and performance tier(s) beyond smoke.
- **If risk tier is Medium** — cover core happy path, key negatives, selected edge cases, and targeted backend/API checks.
- **If risk tier is Low** — keep coverage lean but still validate acceptance criteria, one negative path, and release-critical regressions.
- **If APIs or backend workflows are in scope** — include contract/schema, idempotency, pagination/sorting, retry, and timeout/error scenarios.
- **If performance NFRs or high concurrency risk exist** — select baseline/load/stress/soak tiers as justified; otherwise run smoke tier only.
- **If data sensitivity or privacy constraints apply** — enforce masking/privacy-safe fixtures and document cleanup/reset controls before execution.
- **If change impact is localized** — run targeted regression for changed areas and dependency blast radius.
- **If change impact is broad or touches critical journeys** — expand regression scope to all affected critical paths.

## Testing Dimensions Checklist

- [ ] **Happy path** — primary user flow succeeds as intended
- [ ] **Negative paths** — invalid inputs, unauthorized access, missing or malformed data
- [ ] **Edge cases** — boundary values, race conditions, timeouts, token expiry, concurrent requests
- [ ] **State coverage** — empty, loading, error, and success states match the UI spec
- [ ] **Accessibility** — keyboard navigation, screen reader compatibility, ARIA regions, color contrast (WCAG 2.1 AA)
- [ ] **Responsive / cross-browser** — behavior verified at defined breakpoints and target browsers
- [ ] **Security basics** — no account enumeration, tokens are single-use and short-lived, rate limiting enforced
- [ ] **API/backend integrity** — contract/schema, idempotency, pagination/sorting, retry, timeout/error behavior
- [ ] **Performance** — selected tier(s) meet stated SLOs and pass/fail gates
- [ ] **Regression targeting** — regression scope is impact-based and covers changed critical journeys

## Output Templates

Use the template that matches the user request and keep outputs concise by filling only relevant sections.

### Test Plan

```markdown
## Test Plan: <feature or story title>

**Scope:** <what is included and excluded>
**Risk summary:** <risk tiers and where depth is concentrated>
**Entry criteria:** <what must be true before testing begins>
**Exit criteria:** <what must be true to declare testing complete>
**Test data strategy:** <setup, masking/privacy, reset/cleanup, deterministic fixtures>
**Test environment:** <browser, OS, build version, env name>
**API/backend focus:** <contract/idempotency/pagination-retry-timeout coverage>
**Performance tiers planned:** <smoke/baseline/load/stress/soak and rationale>
**Regression scope:** <impact-based selection and exclusions>
**Non-functional targets:** <performance SLOs, accessibility standard, security requirements>
```

### Test Case

```markdown
## Test Case: <TC-ID> — <short title>

**Linked criterion:** <acceptance criterion text or ID>
**Risk tier:** High / Medium / Low
**Technique:** <boundary value / equivalence partition / state transition / decision table / exploratory>
**Preconditions:** <state of the system before the test>
**Test data:** <accounts, inputs, or fixtures needed>

**Steps:**
1. <action>
2. <action>

**Expected result:** <what should happen>
**Actual result:** <populated during execution>
**Status:** Pass / Fail / Blocked
**Notes:** <environment details or observations>
```

### Bug Report

```markdown
## Bug: <BUG-ID> — <one-line summary>

**Environment:** <browser, OS, build version, env>
**Severity:** Critical / High / Medium / Low
**Priority:** P1 / P2 / P3 / P4
**Linked test case:** <TC-ID>

**Steps to reproduce:**
1. <step>
2. <step>

**Expected behavior:** <what the spec or acceptance criterion states>
**Actual behavior:** <what was observed>
**Attachments:** <screenshots, logs, or network traces>
```

### Test Execution Report

```markdown
## Test Execution Report: <feature or story title>

**Build:** <version> | **Environment:** <env> | **Date:** <date>

**Regression scope executed:** <changed areas and critical journeys covered>

**Performance tier results:** <tier(s), key metric results, pass/fail>

| Status  | Count |
|---------|-------|
| Pass    | <n>   |
| Fail    | <n>   |
| Blocked | <n>   |

**Open defects:**
| Bug ID | Summary | Severity | Status |
|--------|---------|----------|--------|
| <id>   | <...>   | <...>    | <...>  |

**Risk areas / observations:** <patterns or concerns>
**Data strategy effectiveness:** <data stability, masking compliance, cleanup issues>

**Release recommendation:** Ready / Not ready — <rationale>
```

## Quality Checklist

- [ ] Every acceptance criterion has at least one test case
- [ ] Happy path, at least one negative path, and relevant edge cases are covered
- [ ] All eight testing dimensions have been explicitly considered
- [ ] Each bug report has reproducible steps, expected vs. actual, severity, and priority
- [ ] Non-functional requirements (accessibility, performance, security) are tested and recorded
- [ ] Test execution report reflects all results including blocked cases
- [ ] Release sign-off states a clear recommendation with rationale
- [ ] Risk-based test depth is explicit and justified
- [ ] Test data strategy is defined and operationally feasible
- [ ] API/backend coverage is included where relevant
- [ ] Performance tier selection and outcomes are documented
- [ ] Regression scope is impact-based and traceable to changes
- [ ] Release recommendation is tied to risk, open-defect profile, and exit criteria

## Deep References

- `references/risk-based-test-design.md`
- `references/test-data-strategy.md`
- `references/api-backend-qa-checklist.md`
- `references/performance-testing-tiers.md`
- `references/regression-selection-strategy.md`
