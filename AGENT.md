# AGENT.md

Use/read skills only when needed.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

## Skills

**Use skills when needed.**

Pick the matching skill, read it, then follow it:
- [Graphify](./agent-tools/graphify.md) - project graphs, codebase maps, architecture relationships, and knowledge graph queries.
- [Caveman](./agent-tools/caveman.md) - compressed communication mode for lower-token, high-signal responses.
- [Python](./agent-tools/python.md) - Python repo workflow, `uv` commands, linting, tests, and runtime verification.
- [JavaScript/TypeScript](./agent-tools/javascript-typescript.md) - JS/TS repo workflow, `bun` or `npm` scripts, Biome, linting, tests, and runtime verification.
- [GitHub Commit](./agent-tools/github-commit.md) - detailed, descriptive commit messages based on actual staged changes and verification evidence.
- [Code Review](./agent-tools/code-review.md) - review diffs for bugs, regressions, security risks, missing tests, and maintainability issues.
- [Skill Adder](./agent-tools/skill-adder.md) - add new linked tool rules after researching best practices and distilling only the useful parts.
- [Minimal UI/UX](./agent-tools/minimal-ui-ux.md) - clean, accessible, low-risk interfaces that prioritize usability over decoration.
- [Debugging](./agent-tools/debugging.md) - reproduce, isolate, fix minimally, and verify bugs using real evidence.
- [Documentation](./agent-tools/documentation.md) - create clean READMEs, diagrams, runbooks, changelogs, and other markdown docs.
- [Research](./agent-tools/research.md) - investigate questions with source quality checks, cross-verification, and clear citations.

When using skills:
- Prefer local linked rules over assumptions.
- Do not install, delete, commit, push, or mutate external state unless asked or approved.
- If a tool creates files, name and verify the outputs.

---
