<!-- Copy this full Markdown document into a GitHub PR description or PR comment. -->

## PR Change Summary

{{optional_context_line}}

## Executive Summary

{{narrative_summary_2_to_5_sentences}}

## Reviewer Summary

| Hotspot File | Change Type | Observable Risk Signal | Reviewer Focus |
|---|---|---|---|
| {{path_1}} | {{Added|Modified|Deleted|Renamed}} | {{factual signal from git evidence}} | {{specific verification action}} |
| {{path_2_optional}} | {{...}} | {{...}} | {{...}} |

Likely regression areas:
- {{area_1}}
- {{area_2_optional}}

## Release Notes

- {{user_facing_change_1}}
- {{user_facing_change_2_optional}}

If no user-facing change is observable from git evidence, output exactly:
No user-facing changes are identifiable from Git evidence alone.

<details>
<summary>Per-file factual notes (optional for large diffs)</summary>

| File | What changed (factual) | Notes |
|---|---|---|
| {{path_a}} | {{added/modified/deleted with factual note}} | {{optional}} |
| {{path_b_optional}} | {{...}} | {{...}} |

</details>

### Constraints

- GitHub-flavored Markdown only
- No VS Code links, local workspace URIs, or editor line anchors
- Use plain repository-relative file paths when needed
- Keep tone neutral and factual
- Keep Executive Summary as narrative prose (2 to 5 sentences), not bullets