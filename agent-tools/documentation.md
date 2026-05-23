# Documentation

Use this rule when the user asks to create or improve README files, architecture docs, setup guides, runbooks, API docs, changelogs, diagrams, onboarding docs, or any markdown documentation.

## Default Style

Documentation should be minimal, clean, scannable, and useful.

Use:
- short sections
- direct language
- accurate commands
- small icons only when they improve scanning
- tables only when they reduce complexity
- Mermaid diagrams for flows and architecture

Avoid:
- long marketing copy
- fake certainty
- decorative clutter
- huge emoji/icon walls
- undocumented commands
- diagrams that look nice but do not explain flow

## First Step

Before writing docs, inspect the real project:
- existing README/docs
- package scripts or `pyproject.toml` scripts
- env examples
- app entrypoints
- Docker/deploy files
- existing architecture or diagrams

Never document setup, test, lint, deploy, or run commands without checking the repo first.

## README

For a README, prefer this structure:

```md
# Project Name

> One-line description.

## Overview
What this does and who it is for.

## Features
- ...

## Tech Stack
- ...

## Getting Started
Commands that were verified against the repo.

## Environment
Required variables, using placeholders only.

## Scripts
Common commands and what they do.

## Architecture
Short explanation plus Mermaid diagram if useful.

## Troubleshooting
Known local issues and fixes.
```

Use icons sparingly, for example `Overview`, `Setup`, `Architecture`, `Troubleshooting`. Do not put icons on every bullet.

## Architecture Diagrams

Use Mermaid by default because it works well in markdown.

Choose diagram type by intent:
- `flowchart TD` for system architecture and request flow
- `sequenceDiagram` for user/API/service interactions over time
- `erDiagram` for database relationships
- `stateDiagram-v2` for lifecycle/status transitions
- `graph LR` for simple dependency maps

Rules:
- keep diagrams small enough to understand
- label edges with the action or data
- group services with `subgraph` when it helps
- do not invent services, databases, queues, or protocols
- verify names against code/config before drawing

## Runbooks

For operational docs, include:
- purpose
- prerequisites
- exact commands
- expected output or health check
- rollback or recovery steps
- common failure modes

Keep runbooks action-oriented. A tired operator should be able to follow them.

## API Docs

For API docs, include:
- endpoint and method
- auth requirement
- request body or query params
- response shape
- errors
- example request

Verify against route/schema/controller code before documenting.

## Changelog

For changelogs, group by version and category:
- Added
- Changed
- Fixed
- Removed
- Security

Keep entries user-facing. Do not dump commit logs.

## Generic Docs

If the doc type is not listed:
1. identify the audience
2. identify the task the doc helps them complete
3. put the shortest useful path first
4. add details only after the quick path
5. verify claims against files or commands

## Verification

Before finishing:
- check links and paths
- check commands exist
- run a command if the user expects executable setup docs
- make Mermaid syntax simple and likely to render
- ensure no secrets are included

If verification was not possible, state exactly what was not verified.
