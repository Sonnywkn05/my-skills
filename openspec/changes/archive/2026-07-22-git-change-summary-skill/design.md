## Context

This repository defines agent skills and reference guidance rather than product runtime code. The proposed capability adds a new skill that transforms Git changes into a decision-ready narrative formatted for direct GitHub PR comment use.

Current baseline behavior is inconsistent in structure and may include generic or weakly grounded risk statements. The design must improve output consistency, factual grounding, and readability while preserving concise token use.

## Goals / Non-Goals

**Goals:**
- Define a stable, GitHub-ready output contract with three views: executive, reviewer, and release notes.
- Provide a canonical template file that the skill references for consistent rendering.
- Enforce neutral, factual summaries based only on observable Git evidence.
- Keep output visually appealing and highly scannable in GitHub comments.
- Define evaluation scenarios that verify factuality, consistency, and reviewer usefulness.

**Non-Goals:**
- Implementing Git parsing tooling or runtime automation in this change.
- Covering every possible repository workflow or branch-comparison strategy.
- Producing management dashboards or metrics beyond summary content itself.

## Decisions

### Decision: Use a fixed output layout optimized for GitHub comments
- Choice: Standardize section order and formatting for predictable copy-paste results, and store the structure in a dedicated template file referenced by the skill.
- Rationale: Stable structure improves reviewer trust and avoids formatting drift.
- Alternatives considered:
  - Free-form narrative output: rejected due to instability and lower scanability.
  - Multiple templates selected dynamically: rejected to keep behavior predictable.

### Decision: Enforce evidence-first language
- Choice: Allow only claims grounded in observable Git facts.
- Rationale: Prevents speculative intent statements and reduces hallucinated risk claims.
- Alternatives considered:
  - Confidence-scored inference: rejected because strictness requires observable facts only.
  - Hybrid factual and inferred summaries: rejected due to trust and consistency concerns.

### Decision: Provide multi-audience value in one response
- Choice: Include Executive Summary, Reviewer Summary, and Release Notes in one output.
- Rationale: Supports standup, review, and release communication without rerunning prompts.
- Alternatives considered:
  - Single audience output per run: rejected due to additional user iteration cost.

### Decision: Emphasize visual clarity with minimal ornamentation
- Choice: Use concise headings, compact tables, and optional collapsible details.
- Rationale: Improves readability in GitHub while preserving factual density.
- Alternatives considered:
  - Plain bullet-only output: rejected due to weak hotspot readability.
  - Highly decorated markdown: rejected to avoid noise.

### Decision: Make Executive Summary narrative, not bullets
- Choice: Require a short narrative paragraph (2 to 5 sentences) for Executive Summary.
- Rationale: A compact narrative improves readability for stakeholder updates while remaining factual.
- Alternatives considered:
  - Bullet-only executive summary: rejected due to fragmented flow for standup and PR narrative context.

### Decision: Ban editor-specific and local file links
- Choice: Forbid VS Code links, local workspace URIs, and editor line anchors in output.
- Rationale: These links are not portable in GitHub comments and break copy-paste compatibility.
- Alternatives considered:
  - Preserve editor-native links for convenience: rejected because GitHub comment portability is required.

## Risks / Trade-offs

- Risk: Strict factuality can understate probable intent when diffs are ambiguous. -> Mitigation: Keep reviewer guidance focused on observable risk signals and verification actions.
- Risk: Fixed format may feel rigid for tiny changes. -> Mitigation: Keep optional rows and optional detail sections while preserving required top-level order.
- Risk: Overly concise summaries may miss context for large change sets. -> Mitigation: Include optional per-file factual notes in collapsible details.
- Risk: Narrative executive summary may become too verbose. -> Mitigation: Constrain to 2 to 5 sentences and require direct evidence grounding.

## Migration Plan

1. Add a new skill directory and SKILL.md guidance for git-change-summary-skill.
2. Add a reusable GitHub comment template file and reference it from SKILL.md.
3. Include required output contract and evaluation scenarios in the skill content.
4. Validate behavior using frozen scenario queries on fresh agent runs.
5. Iterate only if measured signals fail, then re-run the same scenarios.

Rollback strategy:
- Revert the newly added skill directory and related OpenSpec artefacts if evaluation fails to show measurable improvement.

## Open Questions

- Should the initial version include a compact mode for very small diffs, or should that be deferred to a follow-up change?
- Should large PR handling (for example, grouping hotspots by subsystem) be included now or postponed?
