---
name: vue-nuxt-frontend
description: 'Build front-end features with Vue 3 and Nuxt using sound software engineering practices, typed contracts, testable layering, and accessible form workflows. Use when creating or reviewing Vue/Nuxt components, composables, server routes, or client-side state and validation logic. Triggers: "vue component", "nuxt route", "composable", "typed contract", "form validation", "vitest", "vue test utils".'
argument-hint: 'feature goal, component/composable scope, API contract, or validation flow'
---

# Vue Nuxt Frontend

Build front-end features with Vue 3 and Nuxt using sound software engineering practices.

This skill is context-agnostic and cloud-agnostic. Cloud integrations are optional and must stay behind adapters.

## When To Use

Use this skill when the task involves any of the following:

- Creating or refactoring Vue 3 single-file components.
- Extracting UI logic into composables.
- Adding Nuxt server routes or client-side data fetching.
- Modeling API request and response contracts in TypeScript.
- Building forms with validation, loading, and error states.
- Writing Vitest or Vue Test Utils tests for components and services.

## Fallback Policy

Follow this order of precedence when implementing Vue/Nuxt work:

1. Prefer existing Vue skills. If Vue-specific skills are available, defer to them first: vue-best-practices, vue-testing-best-practices, vue-router-best-practices, vue-pinia-best-practices, and vue-debug-guides.
2. Fall back to general Vue 3 best practices. If no Vue skills are available, use Composition API, script setup, typed props and emits, and single-responsibility components.
3. Cloud provider default. If cloud integration is needed and no provider is specified, propose AWS and ask user permission before using AWS-specific services.
4. Keep core logic portable. Components, composables, and services remain vendor-neutral.

## Core Engineering Practices

- Composition API first. Use script setup with TypeScript and keep components thin.
- Single responsibility per layer. Separate presentation, orchestration, transport, domain logic, and integration.
- Typed contracts. Prefer explicit types and discriminated unions such as ok, not_found, and error.
- Thin transport handlers. In Nuxt routes, parse input, delegate to services, and shape responses only.
- State placement. Use composables for local orchestration and move to Pinia only for cross-view state.
- Dependency injection for testability. Inject gateways, validators, and clients to allow fakes in tests.
- Forms as state machines. Represent loading, valid, invalid, blocked, submitting, success, and failure explicitly.
- Accessibility by default. Use labels, disabled states, aria-invalid, aria-describedby, and role alert for errors.
- Fail visibly and recover gracefully. Show actionable errors and block risky actions until required data is loaded.

## Recommended Structure

- app/components for thin presentational Vue SFCs
- app/composables for orchestration state
- server/api for transport-only route handlers
- server/services for pure domain logic
- server/validators for input rules
- server/contracts for shared TypeScript types
- server/gateways for integration interfaces
- server/adapters for concrete vendor integrations
- server/config for policy constants

## Procedure

1. Clarify the feature request and identify whether work belongs in a component, composable, route, service, validator, or adapter.
2. Define typed contracts for request, response, and error result shapes before implementation.
3. Implement presentation as a thin component and orchestration in a composable.
4. Keep route handlers transport-only and delegate business rules to services.
5. Add validation and model form transitions as explicit states.
6. Add accessibility attributes and stable error message ids.
7. Write tests at the correct layer:
- Component tests for UI behavior and validation messaging.
- Service tests for domain branches using fakes.
- Adapter tests for mapping between vendor SDKs and gateway types.
8. Run quality checks: vue-tsc, project tests, and project formatter.
9. If cloud integration is required, define gateway interfaces first, then implement vendor adapters only after provider confirmation.

## Architecture Shape

User to component to composable to route or fetch to service to validator and gateway to adapter.

The UI never calls vendor SDKs directly.

## Guardrails

- Never call vendor SDKs from components, composables, or services.
- Never assume a cloud provider; ask before defaulting to AWS.
- Keep components presentational and composables orchestration-focused.
- Keep service logic independently testable from UI and transport.
- Surface actionable failure messages to users.
- Maintain accessibility attributes on interactive and error elements.
