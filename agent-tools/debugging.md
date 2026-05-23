# Debugging

Use this rule when the user reports a bug, failing command, crash, broken UI, bad runtime behavior, flaky test, or asks why something is not working.

## Core Loop

Follow this order:

1. Ask where the failure happens if the user did not say: page, command, endpoint, feature, environment, or user flow.
2. Ask for evidence if none was provided: screenshot, logs, error text, failing command, request/response, or reproduction steps.
3. Start by reading available logs or captured runtime output.
4. Reproduce or observe the failure when possible.
5. Capture the exact error, log, request, screenshot, or failing test.
6. Identify the smallest affected path.
7. Isolate the layer causing the failure.
8. Make the smallest safe fix.
9. Verify the failure is gone.
10. Add or update a regression test when practical.

Do not guess from symptoms when logs, tests, network traces, or runtime output are available.
Never assume the root cause without evidence.

## First Checks

Before editing, inspect:
- current git status
- exact command or user flow that fails
- terminal output, browser console, backend logs, network response, or test failure
- relevant config/env values without printing secrets
- nearby code and callers
- repo-specific rules such as Python, JavaScript/TypeScript, or Minimal UI/UX

If the issue is runtime-facing, prefer real runtime evidence over static code reading.
If logs exist, read them first. If logs are missing, ask the user for logs or reproduce the issue to generate them.

Evidence request template:

```text
Where does it fail?
- page/command/endpoint/feature:

What evidence do you have?
- screenshot/log/error text/request-response/repro steps:
```

## Isolation Rules

Narrow the bug by boundary:
- UI -> browser console, route, component state, request payload
- API -> route, schema, auth, service, persistence, response shape
- database -> query, migration, indexes, data shape, constraints
- async/job -> queue state, retries, idempotency, timeouts
- config/deploy -> env, ports, hostnames, secrets, Docker/service status
- tests -> fixture, setup/teardown, mocks, shared state, order dependence

Change one hypothesis at a time. If a hypothesis fails, say what it ruled out.
Keep a clear line between evidence and hypothesis.

## Fix Rules

- Patch the root cause, not just the visible symptom.
- Keep the change surgical.
- Do not refactor unrelated code while debugging.
- Do not hide errors unless the product intentionally needs graceful fallback.
- Preserve existing user flow unless the user approves behavior changes.
- If the bug is caused by bad input or bad state, handle that exact case and document the assumption.

## Verification

Prefer the smallest reliable check:
- rerun the failing command
- rerun the failing test
- add a focused regression test and make it pass
- verify the UI flow in a browser when the bug is visual or interactive
- run lint/typecheck/build only when the touched area needs it

If broad tests fail for unrelated existing issues, report the blocker and run focused validation for the touched path.

## When Root Cause Is Not Found

If the available evidence does not prove the cause, say so plainly.

Use this wording:

```text
I failed to identify the root cause from the available evidence.

What I checked:
- ...

What I ruled out:
- ...

What I need next:
- screenshot/log/error text/reproduction steps/etc.
```

Do not keep patching random code when the cause is unknown.
Ask the user for more evidence, a clue, or permission to gather more runtime data.
Stop after two failed root-cause hypotheses unless a new evidence source is available.

## Flaky Bugs

For intermittent failures:
- run the failing test/flow multiple times when cheap
- look for time, concurrency, shared state, retries, random data, external services, and cleanup leaks
- do not mark fixed after one lucky pass unless the root cause is clear

## Output Style

When reporting debugging work, include:
- root cause
- changed files or area
- verification run
- any remaining risk

Format:

```text
Root cause: ...
Fix: ...
Verification:
- ...
Remaining risk:
- ...
```

If not fixed yet, say the current best hypothesis and next concrete check.
