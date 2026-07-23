# Regression Selection Strategy

Use this reference to select regression scope by impact instead of defaulting to full regression.

## Inputs

- Changed files/components/services
- Dependency map and integration points
- Business-critical user journeys
- Defect history or historically fragile areas

## Scope Selection Flow

1. Identify directly changed areas.
2. Map immediate upstream/downstream dependencies.
3. Mark critical journeys touched by change or dependency effects.
4. Add historically fragile paths that overlap impacted areas.
5. Define exclusions explicitly with rationale.

## Scope Levels

- **Narrow scope**
  - Isolated low-risk change
  - Directly touched components + one key journey

- **Targeted scope**
  - Moderate change with integration effects
  - Changed components + dependency-linked journeys + key negative paths

- **Broad targeted scope**
  - High-risk or high-impact change
  - Full impacted blast radius across critical journeys and shared services

## Exit Criteria Guidance

- All in-scope critical journeys pass
- No unresolved high-severity defects in impacted paths
- Known limitations documented with risk acceptance if release proceeds

## Example

Change: payment retry policy update

Regression set should include:
- Checkout success and failure flows
- Retry exhaustion and timeout behavior
- Order state reconciliation
- Notification and audit side effects
- Related account-history and refund paths if shared services changed
