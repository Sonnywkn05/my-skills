## 1. Skill Scaffold and Core Content

- [x] 1.1 Create the new skill scaffold and metadata
  - Implement: Create skills/git-change-summary-skill/SKILL.md with frontmatter name, description, and argument hint aligned to the new capability.
  - Observe: Spawn a fresh subagent with no change context and ask, "When should I use the git-change-summary-skill?" Expected signals: correct trigger intent, scope includes PR-comment-ready summaries, no mention of unsupported scope features.
  - Measure: Pass if all expected signals are present and no unsupported claims appear. Fail if scope is ambiguous or overbroad. If fail: revise SKILL.md metadata and rerun Observe.

- [x] 1.2 Author the required GitHub-ready output contract in SKILL.md
  - Implement: Add required section order and formatting rules: Executive Summary (3 to 6 bullets), Reviewer Summary (hotspots and risk signals), Release Notes (user-facing only), plus optional collapsible factual detail section.
  - Observe: Spawn a fresh subagent with no change context and run the query, "Summarize my git changes for this PR comment." Expected signals: GitHub-flavored markdown, stable section order, and 3 to 6 executive bullets.
  - Measure: Pass if all expected signals are present and output is directly pasteable to GitHub comments. Fail if section order drifts, bullet count is out of range, or formatting is editor-specific. If fail: refine contract wording and rerun Observe.

## 2. Reviewer and Release-Note Behavior

- [x] 2.1 Add reviewer hotspot and risk-signal guidance
  - Implement: Add explicit instructions for hotspot reporting using only observable Git facts, including change type, risk signal, and reviewer focus guidance.
  - Observe: Spawn a fresh subagent with no change context and run the query, "Give me reviewer hotspots and likely regressions from this diff." Expected signals: hotspot entries are present, risk signals are factual and evidence-linked, reviewer focus guidance is file-specific.
  - Measure: Pass if all expected signals are present with no speculative intent statements. Fail if risk language is generic or unsupported by observable facts. If fail: tighten evidence-first rules and rerun Observe.

- [x] 2.2 Add strict user-facing release-note rules
  - Implement: Add instructions that release notes include only user-facing changes and require an explicit fallback statement when none are observable from Git evidence.
  - Observe: Spawn a fresh subagent with no change context and run the query, "Write release notes from these commits, user-facing only." Expected signals: only user-facing items are listed; internal refactors are excluded; fallback statement appears when applicable.
  - Measure: Pass if all expected signals are present and no internal-only changes are mislabeled as user-facing. Fail if internal changes leak into release notes or fallback is missing. If fail: revise constraints and rerun Observe.

## 3. Evaluation and Completion

- [x] 3.1 Run frozen evaluation scenarios end to end
  - Implement: Execute all three spec evaluation queries using a fresh subagent instance and capture outputs for pass/fail scoring.
  - Observe: For each query, verify expected_behavior signals from openspec/changes/git-change-summary-skill/specs/git-change-summary-skill/spec.md are directly observable.
  - Measure: Pass if every required signal across all three scenarios is present and no regression appears in output stability. Fail if any expected signal is missing. If fail: return to the relevant Implement task, revise content, and rerun Observe.

- [x] 3.2 Final quality sweep and handoff
  - Implement: Verify SKILL.md language is concise, neutral-factual, and aligned with proposal, design, and spec requirements.
  - Observe: Run one additional fresh-subagent check with the query, "Summarize my git changes for this PR comment," and compare section structure against the defined contract.
  - Measure: Pass if structure, strictness, and readability remain consistent. Fail if drift appears. If fail: revise SKILL.md and rerun Observe before marking complete.

## 4. Feedback Remediation

- [ ] 4.1 Add and reference canonical GitHub comment template file
  - Implement: Create skills/git-change-summary-skill/templates/github-pr-comment-template.md and update skills/git-change-summary-skill/SKILL.md to reference it as the canonical output structure.
  - Observe: Spawn a fresh subagent with no change context and ask, "Use the git-change-summary-skill format to summarize this diff for a PR comment." Expected signals: output structure matches template sections and remains GitHub-comment-ready.
  - Measure: Pass if section order and structure align with the template file and are directly pasteable into GitHub comments. Fail if structure drifts or template is not followed. If fail: revise SKILL.md/template mapping and rerun Observe.

- [ ] 4.2 Enforce narrative Executive Summary format
  - Implement: Update SKILL.md rules to require a 2 to 5 sentence factual narrative Executive Summary and remove bullet-only guidance.
  - Observe: Spawn a fresh subagent with no change context and run the query, "Summarize my git changes for this PR comment." Expected signals: Executive Summary is narrative prose, sentence count within bounds, factual language only.
  - Measure: Pass if the Executive Summary is narrative and evidence-grounded. Fail if bullets are used or speculative intent appears. If fail: tighten section rules and rerun Observe.

- [ ] 4.3 Block VS Code and local-file link formats
  - Implement: Add explicit prohibition of VS Code links, local workspace URIs, and editor line anchors; require plain repository-relative paths when needed.
  - Observe: Spawn a fresh subagent with no change context and run the query, "Give me a PR-ready summary with file references." Expected signals: no `file://`, no `vscode://`, no `#L` line-anchor patterns, and file references are plain repo paths.
  - Measure: Pass if all references are GitHub-comment-compatible and portable. Fail if any editor/local link format appears. If fail: strengthen constraints and rerun Observe.
