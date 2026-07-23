# Risk-Based Test Design

Use this reference when a request needs explicit scope prioritization and depth allocation.

## Scoring Model

Score each feature area on a 1-3 scale:

- **Impact**
  - 1: Minor inconvenience, no data loss, no compliance concern
  - 2: User workflow disruption, recoverable financial/operational effect
  - 3: Revenue loss, security/compliance risk, major trust or service impact

- **Likelihood**
  - 1: Stable area with low change complexity
  - 2: Moderate change, mixed dependency complexity
  - 3: New logic, high churn, or fragile dependency graph

- **Detectability**
  - 1: Failure obvious and quickly detectable by users/monitoring
  - 2: Failure detectable with moderate effort
  - 3: Failure subtle, delayed, or hard to detect without deep checks

Risk score = Impact x Likelihood x Detectability

## Risk Tiers and Required Depth

- **High risk (12-27)**
  - Deep negative and edge coverage
  - API/backend and data integrity checks required
  - Performance tier at least baseline; add load/stress as needed
  - Regression scope includes full blast radius for critical paths

- **Medium risk (6-11)**
  - Balanced happy/negative/edge coverage
  - Selective API/backend checks
  - Performance smoke or baseline based on NFR needs
  - Targeted regression on directly impacted journeys

- **Low risk (1-5)**
  - Focused happy path plus key negative path
  - Minimal API/backend checks unless integration is touched
  - Performance smoke checks only when relevant
  - Narrow regression on touched components

## Example

Feature: password reset token validation

- Impact = 3 (auth and account access)
- Likelihood = 2 (moderate logic update)
- Detectability = 3 (subtle security failures)
- Score = 18 -> High risk

Expected test depth:
- Deep token lifecycle and replay tests
- Timeout/expiry, retry, and abuse checks
- Baseline + load checks on verification endpoint
- Regression includes login, reset, and account recovery journeys
