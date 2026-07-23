# Performance Testing Tiers

Use this reference to choose the right level of performance validation for scope and risk.

## Tier Definitions

- **Smoke**
  - Goal: quick confidence that major regressions are absent
  - Typical scope: 1-3 key endpoints or flows
  - Typical gate: no catastrophic latency/error regressions vs recent baseline

- **Baseline**
  - Goal: characterize normal-load behavior against SLOs
  - Typical scope: critical workflows and dependencies
  - Typical gate: meets defined p95/p99 latency and error-rate targets

- **Load**
  - Goal: verify behavior at expected peak traffic
  - Typical scope: sustained expected peak profile
  - Typical gate: stable throughput, acceptable latency, no significant error spikes

- **Stress**
  - Goal: identify breaking points and degradation mode
  - Typical scope: traffic beyond expected peak
  - Typical gate: graceful degradation and clear failure boundaries

- **Soak**
  - Goal: validate long-run stability and resource behavior
  - Typical scope: extended duration at normal/high load
  - Typical gate: no memory/resource leak trends or progressive latency drift

## Tier Selection Heuristics

- High-risk or high-impact changes: baseline + load, optionally stress
- Medium-risk changes: smoke or baseline based on NFR criticality
- Low-risk isolated changes: smoke when performance-sensitive paths are touched

## Reporting Minimums

- Workload profile and duration
- Key metrics (latency percentiles, error rate, throughput)
- Pass/fail outcome vs declared gate
- Observed bottlenecks and next actions
