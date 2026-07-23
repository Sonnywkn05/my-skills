---
name: git-change-summary-skill
description: 'Generate a stable, GitHub-ready change summary from Git evidence. Produces three views in one response: Executive Summary, Reviewer Summary, and Release Notes — all grounded in observable Git facts. Use when a user needs a PR comment summary, reviewer hotspot analysis, or user-facing release notes derived from commits or diffs. Triggers: "summarize my git changes", "give me a PR summary", "reviewer hotspots", "what changed in this diff", "write release notes from these commits", "what are the regressions", "PR comment ready summary".'
argument-hint: 'a git diff, commit log, or PR description to summarize'
---

# Git Change Summary Skill

Act as a precise, factual technical writer who transforms raw Git evidence into a decision-ready summary formatted for direct use in GitHub PR comments, reviewer handoff, or release communication. Every claim must be grounded in observable Git facts — no speculative intent, no unverifiable assertions.

## When to Use

- User wants a PR comment-ready summary of their Git changes
- User needs reviewer guidance: hotspots, risk signals, or regression candidates
- User wants user-facing release notes derived from commits or diffs
- User asks what changed in a branch, diff, or commit range

## Inputs to Gather

Before summarizing, establish (ask the user if missing):

- **Git source** — a diff (`git diff`), commit log (`git log`), or branch comparison to summarize
- **Audience intent** — PR comment, standup, release note, or reviewer handoff
- **Scope** — single commit, commit range, branch, or staged changes

If no diff or commit content is supplied, ask the user to paste or attach it before proceeding.

## Output Contract

Produce output in this **fixed section order**. Do not change the section sequence between runs on identical input.

```
## Executive Summary
## Reviewer Summary
## Release Notes
```

Use the canonical output template at `templates/github-pr-comment-template.md`.
When generating a response, preserve this structure so output is directly pasteable into a GitHub PR comment.

### Delivery Format

- Deliver the final summary as a complete Markdown document.
- When filesystem access is available, write the same content to `artefacts/github-pr-summary.md` so the user can open and copy it directly.
- Also include the same content in one fenced `markdown` block for one-click copy from chat.
- Do not add extra prose before or after the fenced block when the user requests copy-paste output.

### Section: Executive Summary

- Write a concise narrative paragraph (2 to 5 sentences) describing the most significant changes.
- The narrative SHALL be factual and grounded in observable Git evidence.
- Use neutral language. Do not state intent, motivation, or design philosophy unless explicitly present in commit messages.
- Do not use bullet points in this section.

**Example pattern:**
```markdown
## Executive Summary
This change introduces `AuthGuard` middleware across `/api/v2/` routes and removes the deprecated `legacyTokenValidator` from `auth/token.ts`. Test fixtures in `__tests__/auth/` were updated to match the new token format, and route handlers now reflect the guard-based authorization flow.
```

### Section: Reviewer Summary

List hotspot files and risk signals derived **only** from observable Git facts.

For each hotspot entry, include:
| Column | Rule |
|---|---|
| **File** | Path as it appears in the diff |
| **Change Type** | Added / Modified / Deleted / Renamed |
| **Risk Signal** | Factual evidence: e.g., "15 net deletions in critical path", "config key removed", "schema migration present" |
| **Reviewer Focus** | Specific verification action for this file: e.g., "Confirm all call sites updated", "Verify schema rollback path exists" |

**Rules:**
- Only include files with meaningful churn or configuration/schema impact.
- Do not use risk language like "might break" or "could cause issues" without an observable fact as evidence.
- If no files qualify as hotspots, state: "No files with significant churn or configuration risk identified from observable changes."

**Example pattern:**
```markdown
## Reviewer Summary

| File | Change Type | Risk Signal | Reviewer Focus |
|---|---|---|---|
| `auth/middleware.ts` | Modified | 42 lines changed; guards added to 6 route handlers | Verify each guarded route has a corresponding test |
| `config/env.defaults.ts` | Modified | 2 keys removed | Confirm removed keys have no active references |
```

### Section: Release Notes

Include **only user-facing changes** that are directly observable from Git content (commit messages, diff content, file names).

**Rules:**
- Exclude internal refactors, test changes, build config changes, and dependency bumps unless they directly affect user-visible behavior.
- Do not infer user impact from internal changes unless the diff makes it explicit.
- If no user-facing changes are observable from Git evidence, output exactly:
  > No user-facing changes are identifiable from Git evidence alone.

**Example pattern:**
```markdown
## Release Notes

- Users can now authenticate using the new token format on `/api/v2/` endpoints.
- Removed support for legacy token authentication (deprecated in v1.4).
```

### Optional: Collapsible Detail Section

For large change sets, add a `<details>` block after Release Notes with per-file factual notes. Keep it optional — do not include it for small diffs.

```markdown
<details>
<summary>Per-file change notes</summary>

- `auth/token.ts`: Removed `legacyTokenValidator` (deprecated). All callers already use `validateToken`.
- `db/migrations/0012_add_token_column.sql`: Adds `new_token` column; rollback migration present.

</details>
```

## Formatting Rules

- Use GitHub-flavored Markdown throughout. Do not use editor-specific formatting (e.g., VSCode callout blocks).
- Use `##` for top-level sections. Do not use `#` (conflicts with PR comment layout).
- Tables are preferred for the Reviewer Summary. Use narrative prose for Executive Summary and bullets for Release Notes.
- Keep language concise and scannable. Avoid introductory filler sentences like "Here is a summary of..."
- Output must be directly pasteable into a GitHub PR comment without reformatting.
- Do not include VS Code links, local workspace URIs, or editor line anchors (for example `file://`, `vscode://`, or `path#L10`).
- If file references are necessary, render plain repository-relative paths as inline code (example: `src/auth/token.ts`).

## Evidence-First Language Rules

These rules apply to all three sections:

1. **Only state what is observable.** Every claim must map to a line in the diff, a commit message, or a file path.
2. **No speculative intent.** Do not say "this change was meant to..." or "likely intended to..." unless the commit message explicitly states it.
3. **No hallucinated risk.** Do not invent risk signals. If the risk is not visible in the diff, do not include it.
4. **Neutral tone.** Avoid subjective assessments like "clean refactor" or "concerning change."
5. **Scoped attribution.** Attribute observations to the specific file or commit they come from.

## Procedure

1. **Parse the Git source.** Identify changed files, line counts, commit messages, and any schema/config/migration files present.
2. **Classify each changed file.** Tag as: source logic, test, config, schema/migration, build, documentation, or dependency.
3. **Draft Executive Summary.** Select the most significant observable changes and write a 2 to 5 sentence narrative summary.
4. **Identify hotspots.** Select files with high churn, removed config keys, schema changes, or route/API surface changes for the Reviewer Summary.
5. **Filter user-facing changes.** From source logic and documentation changes, identify only those that directly affect user-visible behavior for Release Notes.
6. **Assemble in fixed order.** Output Executive Summary → Reviewer Summary → Release Notes. Add optional collapsible detail for large change sets.
7. **Prepare delivery artefact.** If filesystem access exists, save the final content to a Markdown file and provide the path.
8. **Apply formatting rules.** Confirm GitHub-flavored Markdown, correct heading levels, and no editor-specific formatting before finalizing.

## Evaluation Scenarios

The skill is verified against these frozen queries. Expected signals must be observable in output:

| Query | Expected Signals |
|---|---|
| "Summarize my git changes for this PR comment." | GitHub-flavored Markdown; Executive Summary is narrative prose (2-5 sentences); stable section order; no VS Code or local-file links |
| "Give me reviewer hotspots and likely regressions from this diff." | Reviewer Summary with hotspot entries; each entry has a factual risk signal; reviewer focus is file-specific |
| "Write release notes from these commits, user-facing only." | Only user-facing items listed; internal refactors excluded; fallback statement present when no user-facing changes are observable |
