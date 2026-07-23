## Why

Teams need fast, reliable summaries of Git changes that can be pasted directly into GitHub PR comments for standups, reviewer handoff, and release-note drafting. Current behavior is inconsistent in structure and often includes either too much raw diff detail or ungrounded inference, which reduces reviewer trust.

## Baseline Measurement

Current model behavior without this skill was measured with these scenarios:
- Query: "Summarize my git changes for this PR comment." Observed gap: output structure varies run to run and is not consistently GitHub-comment-ready.
- Query: "Give me reviewer hotspots and likely regressions from this diff." Observed gap: risk signals are sometimes generic and not clearly tied to observable Git evidence.
- Query: "Write release notes from these commits, user-facing only." Observed gap: output may include internal refactors or assumptions not directly supported by commit content.

## What Changes

- Add a new skill that converts raw Git changes into a decision-ready narrative using a stable, GitHub-formatted output.
- Add a canonical template file under the skill directory so the response layout is reusable and referenced directly by the skill instructions.
- Standardize three output views in one response: executive summary, reviewer summary, and user-facing release-note summary.
- Enforce neutral, factual language based only on observable Git evidence.
- Add explicit formatting rules to keep the output visually appealing and easy to scan in GitHub comments.
- Require the executive summary to be narrative prose rather than bullet points.
- Explicitly prohibit VS Code links, local workspace URIs, and editor line anchors in generated output.
- Include scenario-based evaluation guidance to verify consistency, factuality, and reviewer usefulness.

## Capabilities

### New Capabilities
- `git-change-summary-skill`: Generates a stable, GitHub-ready change summary with executive, reviewer, and user-facing release-note sections grounded in observable Git facts.

### Modified Capabilities
- None.

## Impact

- Adds a new skill directory and guidance file for Git change summarization.
- Introduces new OpenSpec capability documentation under this change.
- No application runtime or API changes; impact is limited to agent behavior and skill authoring assets.
