# git-change-summary-skill Specification

## Purpose
Define the canonical requirements for producing stable, GitHub-ready summaries of Git changes.

## Requirements

### Requirement: Git summary output is GitHub comment ready
The skill SHALL produce output in GitHub-flavored Markdown that can be pasted directly into a GitHub PR comment without reformatting.

#### Scenario: Direct paste compatibility
- **WHEN** a user asks for a summary of Git changes for a PR comment
- **THEN** the skill returns GitHub-flavored Markdown with stable section headings and no editor-specific formatting assumptions

### Requirement: Skill references a canonical output template file
The skill SHALL reference a dedicated template file stored under the skill directory for rendering GitHub comment output.

#### Scenario: Template-file based output contract
- **WHEN** skill guidance is authored or updated
- **THEN** the GitHub comment layout is defined in a template file that is explicitly referenced by SKILL.md

### Requirement: Executive summary is concise factual narrative
The skill SHALL include an Executive Summary section written as narrative prose (2 to 5 sentences) grounded in observable Git evidence.

#### Scenario: Executive summary narrative and factuality
- **WHEN** the skill summarizes a change set
- **THEN** the Executive Summary is narrative prose with 2 to 5 sentences and contains no speculative intent

### Requirement: Reviewer summary highlights hotspots and risk signals
The skill SHALL include a Reviewer Summary that identifies hotspot files, change type, and risk signals derived from observable Git facts.

#### Scenario: Reviewer guidance with evidence-linked signals
- **WHEN** files with meaningful churn or critical configuration changes are present
- **THEN** the skill lists those files with factual risk signals and reviewer focus guidance for verification

### Requirement: Release notes include only user-facing changes
The skill SHALL provide a Release Notes section that includes only user-facing changes observable from Git content.

#### Scenario: No observable user-facing changes
- **WHEN** commits and diffs show internal-only changes
- **THEN** the skill states that no user-facing changes are identifiable from Git evidence alone

### Requirement: Output structure remains stable across repeated runs
Given the same Git input, the skill SHALL keep section order and output layout consistent.

#### Scenario: Repeatability on unchanged input
- **WHEN** the same repository state is summarized multiple times
- **THEN** the top-level section order and required subsection structure remain consistent

### Requirement: Output excludes VS Code and local workspace links
The skill SHALL not output VS Code-specific links, local workspace URIs, or editor line-anchor formats that are not portable to GitHub comments.

#### Scenario: Link portability compliance
- **WHEN** file references appear in the summary output
- **THEN** the output uses plain repository-relative paths and does not include `file://`, `vscode://`, or `#L` editor anchor patterns

## Evaluations

```json
[
  {
    "query": "Summarize my git changes for this PR comment.",
    "expected_behavior": [
      "Returns GitHub-flavored Markdown that can be pasted into a GitHub comment",
      "Includes an Executive Summary section written as a 2 to 5 sentence factual narrative",
      "Uses stable top-level section order across repeated runs",
      "Contains no VS Code links, local workspace URIs, or editor line-anchor patterns"
    ]
  },
  {
    "query": "Give me reviewer hotspots and likely regressions from this diff.",
    "expected_behavior": [
      "Provides a Reviewer Summary with hotspot file entries",
      "Each hotspot entry includes a factual risk signal from observable Git changes",
      "Reviewer focus guidance is specific to listed files"
    ]
  },
  {
    "query": "Write release notes from these commits, user-facing only.",
    "expected_behavior": [
      "Release Notes section includes only user-facing items supported by commit or diff evidence",
      "Internal-only refactors are excluded from user-facing notes",
      "If no user-facing change is observable, explicitly states that no user-facing changes were identified from Git evidence alone"
    ]
  }
]
```
