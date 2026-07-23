## Executive Summary
This change set adds a new OpenSpec change package for `git-change-summary-skill` and introduces a new skill directory with a canonical GitHub PR comment template. In `openspec/changes/git-change-summary-skill/`, the change artefacts include a proposal, design, tasks, and capability spec with evidence-first rules, fixed section order, and evaluation scenarios. The current working tree reflects both staged additions and follow-up edits to four of those OpenSpec documents, resulting in net churn concentrated in documentation and skill-definition files. Two untracked files under `skills/git-change-summary-skill/` add the runnable skill instructions (`SKILL.md`) and the reusable template (`templates/github-pr-comment-template.md`).

## Reviewer Summary

| File | Change Type | Risk Signal | Reviewer Focus |
|---|---|---|---|
| `openspec/changes/git-change-summary-skill/design.md` | Added + Modified | 87 additions and 4 deletions across staged and unstaged diffs | Confirm final design decisions still align with the spec requirements and task checklist |
| `openspec/changes/git-change-summary-skill/specs/git-change-summary-skill/spec.md` | Added + Modified | 88 additions and 6 deletions in capability requirements and evaluation signals | Verify requirement wording matches evaluation scenarios and does not conflict with output contract |
| `openspec/changes/git-change-summary-skill/tasks.md` | Added + Modified | 58 additions and 6 deletions; task status includes checked items plus remaining feedback-remediation tasks | Confirm incomplete tasks (`4.1` to `4.3`) map to actual file changes in the new skill artefacts |
| `skills/git-change-summary-skill/SKILL.md` | Added | New 116-line skill definition introduces output contract, evidence rules, and delivery requirements | Validate section order, narrative constraints, and no-link portability rules against expected PR output |
| `skills/git-change-summary-skill/templates/github-pr-comment-template.md` | Added | New 31-line canonical template defines headings, table structure, and fallback text | Confirm template and `SKILL.md` are consistent on headings, Executive Summary format, and fallback statements |

## Release Notes

- Added a new `git-change-summary-skill` that formats Git evidence into PR-ready Markdown with fixed sections: Executive Summary, Reviewer Summary, and Release Notes.
- Added a reusable GitHub PR comment template at `skills/git-change-summary-skill/templates/github-pr-comment-template.md` for consistent summary structure.

<details>
<summary>Per-file factual notes</summary>

- `openspec/changes/git-change-summary-skill/.openspec.yaml`: Added change metadata scaffold.
- `openspec/changes/git-change-summary-skill/proposal.md`: Added baseline gaps, scope, and impact statements; later updated with small follow-up edits.
- `openspec/changes/git-change-summary-skill/design.md`: Added goals, decisions, trade-offs, migration plan, and follow-up revisions.
- `openspec/changes/git-change-summary-skill/specs/git-change-summary-skill/spec.md`: Added requirements and evaluation scenarios; later edited requirement wording and expected behavior details.
- `openspec/changes/git-change-summary-skill/tasks.md`: Added implementation/evaluation checklist and additional remediation tasks.
- `skills/git-change-summary-skill/SKILL.md`: Added skill frontmatter, output contract, evidence-first rules, and procedure.
- `skills/git-change-summary-skill/templates/github-pr-comment-template.md`: Added canonical PR-comment template with table and fallback text.

</details>
