# Test Data Strategy

Use this reference when planning test execution and case reliability.

## Data Lifecycle

1. **Setup**
- Define fixtures, account states, and dependencies required per scenario.
- Prefer deterministic seed scripts over ad hoc manual data creation.

2. **Use**
- Keep test data scoped and traceable to each test case.
- Avoid shared mutable test records across parallel tests unless explicitly controlled.

3. **Reset/Cleanup**
- Define cleanup action per dataset (rollback, delete, archive, or environment reset).
- Ensure reruns can start from a known baseline state.

## Privacy and Safety

- Never use production personal data in test environments.
- Mask or synthesize sensitive fields (email, phone, IDs, payment data).
- Store only the minimum data needed for test intent.

## Determinism Rules

- Use fixed timestamps or clock controls when time-sensitive behavior is tested.
- Use stable identifiers for repeatability in assertions.
- Isolate randomization behind seeded generators when random values are needed.

## Data Strategy Checklist

- [ ] Required datasets are defined for each scenario
- [ ] Sensitive fields are masked or synthetic
- [ ] Data setup is repeatable
- [ ] Cleanup/reset steps are explicit
- [ ] Parallel execution contention is addressed

## Example Pattern

For order-cancellation testing:
- Seed customer account, product catalog, and unpaid order in setup.
- Use synthetic customer profile fields.
- Execute cancellation flow and validate status transitions.
- Cleanup by deleting seeded order and restoring inventory counters.
