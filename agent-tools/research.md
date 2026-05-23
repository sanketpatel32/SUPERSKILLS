# Research

Use this rule when the user asks to research, compare, investigate, verify, find best practices, choose a tool, evaluate options, or answer with current/external information.

## Goal

Produce answers grounded in evidence, not memory or vibes.

Good research:
- defines the question
- uses the right source types
- cross-checks important claims
- separates facts from inference
- cites sources
- says when evidence is weak or missing

## Workflow

1. Clarify the research target if vague.
   - What decision will this answer support?
   - Is the user asking for current facts, best practices, examples, or a recommendation?

2. Choose source types.
   - Official docs for product/tool/API behavior.
   - Specs and standards for protocols and formats.
   - Primary sources for announcements, releases, pricing, policies, laws, and company facts.
   - Reputable secondary sources for analysis and comparisons.
   - Community posts only for lived experience, bugs, workarounds, or inspiration.

3. Search broadly, then narrow.
   - Start with multiple source candidates.
   - Prefer recent sources for fast-changing topics.
   - Prefer original sources over summaries.
   - Avoid SEO articles unless they cite primary evidence.

4. Verify.
   - Cross-check high-impact claims with at least two reliable sources when possible.
   - Check publication dates and version numbers.
   - Identify conflicts between sources.
   - If sources disagree, say which source is more authoritative and why.

5. Answer.
   - Start with the conclusion.
   - Give the supporting evidence.
   - Include links.
   - State assumptions and uncertainty.
   - Recommend next steps only when useful.

## Source Quality

Prefer:
- official documentation
- standards bodies
- source repositories and changelogs
- vendor release notes
- academic papers for research claims
- government or legal primary sources for rules and regulations

Use cautiously:
- blogs
- Medium/Substack posts
- Reddit/HN/forum threads
- AI-generated summaries
- outdated docs
- vendor comparison pages that attack competitors

Do not use Wikipedia as final authority. It can be a starting point for finding better sources.

## Current Information

Browse the web when information may have changed:
- prices
- releases
- APIs and SDKs
- laws and regulations
- company leadership
- product recommendations
- security vulnerabilities
- cloud/provider limits
- docs and framework behavior

Do not answer from old memory when the user asks for latest/current information.

## Output Format

For short research:

```text
Conclusion: ...

Evidence:
- ...
- ...

Sources:
- ...
```

For comparisons:

```text
Recommendation: ...

Options:
| Option | Best for | Tradeoff |
|---|---|---|

Why:
- ...

Sources:
- ...
```

For uncertain results:

```text
Best current answer: ...

Confidence: low/medium/high

Why confidence is limited:
- ...

What would improve confidence:
- ...
```

## Rules

- Do not over-cite obvious claims.
- Do cite non-obvious, current, or high-impact claims.
- Do not quote long passages.
- Do not hide uncertainty.
- Do not present inference as fact.
- Do not recommend paid tools/products without checking current pricing and maintenance signals.
