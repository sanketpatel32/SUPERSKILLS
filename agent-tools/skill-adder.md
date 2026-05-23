# Skill Adder

Use this rule when the user asks to add a new skill, tool rule, agent rule, workflow file, or linked markdown instruction under `agent-tools/`.

## Required Outcome

Every new skill request must produce exactly two changes unless the user asks otherwise:
- add one link in the `AGENT.md` `Skills` section
- create one focused file at `agent-tools/<skill-name>.md`

Keep `AGENT.md` lean. Put detailed instructions in the linked file.
Never create a skill file without also adding it to `Skills`.

## Workflow

1. Name the skill.
   - Use lowercase kebab-case.
   - Keep it short and specific.
   - Example: `code-review.md`, `github-commit.md`, `python.md`.

2. Research before writing.
   - Inspect existing local `agent-tools/` files for style and overlap.
   - Search local repo examples when the skill relates to the user's projects.
   - Use web research when public best practices, tool docs, or current behavior matter.
   - Prefer official docs, widely used specs, and high-quality examples.
   - Do not copy long text. Extract the best operational rules.

3. Distill the research.
   - Keep only instructions that change agent behavior.
   - Remove generic advice, marketing claims, and obvious filler.
   - Prefer checklists and decision rules over essays.
   - Write for a literal agent that may follow steps mechanically.

4. Write the skill file.
   - Start with a clear one-sentence purpose.
   - Add trigger conditions.
   - Add exact workflow steps.
   - Add safety rules.
   - Add expected output format if the skill produces responses.
   - Keep it concise.

5. Update `AGENT.md`.
   - Always add one bullet under `## Skills`.
   - Place the new bullet with the other linked rules.
   - Do this by default for every new skill.
   - Use this format:

```md
- [Skill Name](./agent-tools/skill-name.md) - short practical description.
```

6. Verify.
   - Read back `AGENT.md`.
   - Read back the new skill file.
   - Confirm the link path is correct.
   - Confirm the new skill appears in the `Skills` list.

## Quality Bar

A good skill file:
- tells the agent exactly when to use it
- gives concrete steps in the right order
- says what not to do
- is short enough to be read every time it triggers
- preserves user preferences from this repo
- avoids bloating `AGENT.md`

A bad skill file:
- duplicates the main agent philosophy
- adds generic best practices without workflow impact
- assumes the agent will infer missing steps
- buries the important rule in long prose
- creates extra files without need

## Research Standard

Before adding a skill, gather enough evidence to avoid making up a workflow.

Use this order:
- local existing rules
- local real repos or examples
- official documentation
- reputable public examples
- community examples only as inspiration, not authority

If sources disagree, prefer the rule that is safest, easiest to verify, and closest to the user's actual workflow.

## Final Response

Report:
- skill file created
- `AGENT.md` `Skills` link added
- sources or local examples used
- any assumptions
