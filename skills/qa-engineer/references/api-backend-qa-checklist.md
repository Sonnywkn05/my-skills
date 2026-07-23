# API and Backend QA Checklist

Use this reference for backend-integrated features and service-level validation.

## Contract and Schema

- Verify request and response schema adherence.
- Validate required/optional fields and type constraints.
- Confirm backward compatibility expectations if versioning applies.

## Behavioral Integrity

- Idempotency: repeated requests should not create unintended side effects.
- Pagination/sorting: ordering guarantees, boundary pages, empty pages.
- Filtering/query semantics: include/exclude correctness and invalid filter handling.

## Resilience Behavior

- Retry semantics: safe retries and duplicate handling.
- Timeout behavior: graceful failure and clear error responses.
- Error mapping: stable status codes and actionable error payloads.

## Data and Consistency

- Verify persistence side effects and state transitions.
- Check eventual consistency windows where applicable.
- Validate audit/logging behavior for critical mutations.

## Security Basics

- Authorization checks across roles and scopes.
- No data leakage in error payloads.
- Abuse controls where relevant (rate limit, lockout, replay protection).

## Quick Matrix

- Happy path: at least one success call per endpoint
- Negative path: invalid input, unauthorized, forbidden, not found
- Edge path: boundary values, duplicate requests, concurrency contention
