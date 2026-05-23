# GitHub Commit

Use this rule when the user asks to create a commit, write a commit message, review staged changes for a commit, or prepare GitHub-friendly commit text.

## Core Preference

Commit messages should be descriptive and detailed.

Default to a structured, high-signal message:

```text
type(scope): concise imperative summary

Explain what changed in concrete terms.

Explain why the change was needed, including the bug, product behavior,
cleanup goal, or operational reason.

Verification:
- command or check that passed
- command or check that could not run, with reason

Refs: #123
```

The subject should summarize the commit. The body should preserve the context future maintainers need.

## Before Writing a Message

Inspect the actual change set first:
- `git status --short`
- `git diff --staged`
- `git diff` if the user wants a message for unstaged work
- relevant test/lint output if available

Do not invent motivation, issue numbers, tests, or behavior changes. If evidence is missing, omit it or say it was not run.

If unrelated changes are present, separate them mentally and do not describe files outside the requested/staged change set.
If nothing is staged and the user asked for a commit, ask whether to stage the relevant files or commit all current changes.
If the user only asked for a message, do not stage or commit.

## Commit Creation Rules

- Do not create a commit unless the user explicitly asks to commit.
- Do not stage unrelated files.
- Do not amend a commit unless the user explicitly asks to amend.
- Do not push unless the user explicitly asks to push.
- Prefer non-interactive commands.
- For multi-line messages, prefer writing the message to a temporary file and using `git commit -F <file>` instead of stacking many `-m` flags.
- Run `git status --short` after committing and report any remaining uncommitted files.

## Subject Line

Use:
- imperative mood: `add`, `fix`, `remove`, `document`, `refactor`
- no trailing period
- concise but specific
- lower-case Conventional Commit type when useful

Preferred format:

```text
type(scope): summary
```

Good examples:

```text
fix(auth): preserve refresh token rotation errors
feat(workflows): add tenant assignment fallback
docs(readme): document uv startup flow
refactor(api): isolate workflow status mapping
test(menu): cover retry exhaustion state
```

Avoid:

```text
update files
fix bug
changes
wip
stuff
```

## Types

Use these Conventional Commit-style types by default:
- `feat` - user-facing feature or capability
- `fix` - bug fix
- `docs` - documentation only
- `test` - tests only or test infrastructure
- `refactor` - code structure change without intended behavior change
- `perf` - performance improvement
- `style` - formatting or non-behavioral code style
- `build` - build system or dependency changes
- `ci` - CI/CD workflow changes
- `chore` - maintenance with no product/runtime behavior change
- `revert` - revert a prior commit

If one commit spans multiple types, choose the type that best represents the user-visible or operational reason. If the changes are truly unrelated, recommend splitting the commit.

## Body Style

Use the body to explain what and why, not a line-by-line diff.

Prefer this structure for non-trivial commits:

```text
What changed:
- describe the concrete code/doc/config changes
- mention important files or modules when useful

Why:
- explain the failure mode, requirement, cleanup reason, or product impact
- mention tradeoffs or intentionally preserved behavior

Verification:
- exact command that passed
- exact command that failed or was skipped, with reason
```

For small commits, a shorter body is fine:

```text
docs(agent): add GitHub commit message rules

Add a dedicated commit-writing rule that prefers detailed bodies,
verification notes, and Conventional Commit-style subjects.
```

## Breaking Changes and Footers

If behavior, API, config, schema, migration, or deployment compatibility breaks, mark it clearly:

```text
feat(api)!: require tenant id for workflow creation

What changed:
- require tenant id in workflow creation requests
- reject requests without explicit tenant ownership

Why:
- prevents private workflows from being created without ownership

BREAKING CHANGE: workflow creation callers must now send tenant id.
```

Use footers when relevant:
- `Refs: #123`
- `Closes: #123`
- `Reviewed-by: Name`
- `Co-authored-by: Name <email@example.com>`

Only include footers that are true and requested or evidenced.

## Detail Level

Prefer detailed bodies when:
- the change affects runtime behavior
- the change fixes a bug
- the change touches config, deployment, auth, data, billing, or workflows
- the change required non-obvious tradeoffs
- verification matters for future debugging

Keep the message shorter when:
- the commit is docs-only and obvious
- the commit is formatting-only
- the diff is tiny and self-explanatory

Even then, avoid vague subjects.

## Verification Wording

Good:

```text
Verification:
- uv run test
- npm run lint
- not run: Docker build, Docker Desktop unavailable
```

Bad:

```text
Tests passed
```

If no verification was run:

```text
Verification:
- not run: message-only change
```

## Final Checklist

Before finalizing a commit message:
- subject matches the actual diff
- body explains what changed and why
- verification is exact
- unrelated files are not described
- breaking changes are explicit
- no secrets, credentials, or private tokens are included
- message does not claim tests ran unless there is evidence
