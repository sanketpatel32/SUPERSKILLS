# Code Review

Use this rule when the user asks for a review, PR review, diff review, pre-commit review, or second opinion on code quality.

## Review Goal

Find issues that could matter after merge:
- correctness bugs
- regressions
- security or privacy risks
- broken edge cases
- data loss or migration risk
- missing tests for changed behavior
- maintainability problems that create real future cost

Do not spend review budget on style nits, formatting, or issues already handled by lint/typecheck unless they hide a real bug.

## Inputs To Inspect

Start from real evidence:
- `git status --short`
- `git diff --staged` for staged review
- `git diff` for unstaged review
- base-branch diff for PR review when available
- nearby tests, schemas, types, routes, and callers
- repo-specific tool rules such as Python or JavaScript/TypeScript when relevant

If the review target is unclear, state what was reviewed.
If no diff is available, ask for the PR, branch, staged diff, or file list before giving findings.

## Review Method

1. Understand the intended behavior from the task, diff, tests, and surrounding code.
2. Trace changed code through callers, data flow, error paths, and persistence.
3. Check security boundaries: auth, tenant scope, secrets, logs, user input, file/network access.
4. Check edge cases: empty data, retries, partial failures, concurrency, timeouts, invalid input.
5. Check tests: whether changed behavior has focused coverage and whether existing tests still prove the right thing.
6. Verify findings against code before reporting. Do not guess.

Before reporting a finding, confirm:
- exact changed line or nearby caller exists
- failure mode is plausible from code, not preference
- suggested fix is smaller than the problem it solves

## Severity

Use these labels:
- `Blocking` - likely production bug, security issue, data loss, migration break, or severe regression.
- `Major` - real bug or missing coverage that should be fixed before merge.
- `Minor` - low-risk issue worth fixing if nearby.
- `Nit` - optional cleanup; keep these rare.

Prefer fewer, stronger findings over many weak comments.

## Output Format

Findings first, ordered by severity:

```text
Findings
- Blocking: path/to/file.ts:42 - Problem. Why it matters. Suggested fix.
- Major: path/to/file.py:88 - Problem. Why it matters. Suggested fix.

Open Questions
- Any assumption that affects review confidence.

Verification Gaps
- Tests or commands not run, or coverage missing.
```

If there are no findings, say that explicitly and list residual risk:

```text
No findings.

Residual risk:
- Not run: integration tests.
- Review only covered staged diff.
```

## Rules

- Do not rewrite code during a review unless the user asks for fixes.
- Do not approve or reject a PR; report evidence.
- Do not report speculative issues without a concrete code path.
- Do not duplicate CI noise unless it changes behavior.
- Cite exact files and lines when possible.
- Mention pre-existing issues separately from issues introduced by the diff.
- For large diffs, focus on high-risk paths first and say what was not reviewed deeply.
- If a finding is only a preference, omit it.
