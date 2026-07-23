## ADDED Requirements

### Requirement: Risk-Based Test Design Guidance
The qa-engineer skill SHALL require risk-based prioritization before detailed scenario derivation so test depth is aligned with business and technical risk.

#### Scenario: Risk tier drives scope depth
- **WHEN** a user asks for a test plan or test strategy
- **THEN** the skill includes a risk-tiering step and explains how high-risk areas receive deeper coverage

### Requirement: Test Data Strategy Coverage
The qa-engineer skill SHALL include explicit test data planning guidance covering data setup, masking/privacy, reset/cleanup, and determinism.

#### Scenario: Test data planning is included
- **WHEN** the skill produces test cases or execution planning
- **THEN** it captures required test data sources, constraints, and lifecycle handling in the output

### Requirement: API and Backend QA Depth
The qa-engineer skill SHALL include backend-focused QA guidance for contract validation, idempotency, pagination/sorting behavior, retries, and timeout/error handling.

#### Scenario: Backend behavior is explicitly tested
- **WHEN** a feature depends on APIs or backend workflows
- **THEN** the skill includes API/backend test scenarios in addition to UI/state scenarios

### Requirement: Performance Testing Tier Strategy
The qa-engineer skill SHALL define performance testing tiers (smoke, baseline, load, stress, soak) and indicate when each tier is applicable.

#### Scenario: Appropriate performance tier is selected
- **WHEN** non-functional requirements include performance concerns
- **THEN** the skill recommends one or more performance tiers with clear pass/fail intent

### Requirement: Impact-Based Regression Selection
The qa-engineer skill SHALL guide regression scope selection using change impact and dependency blast radius rather than defaulting to full regression.

#### Scenario: Regression scope reflects change impact
- **WHEN** the user requests release readiness or regression coverage
- **THEN** the skill proposes a targeted regression set tied to changed areas and critical dependencies
