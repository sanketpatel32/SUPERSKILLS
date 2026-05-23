# Graphify

Use Graphify when the user wants a project map, codebase relationship graph, architecture overview, corpus graph, or asks for `/graphify`.

## Trigger Phrases

- `/graphify`
- `graphify this`
- `make a graph of this repo`
- `map this codebase`
- `show file relationships`
- `explain the architecture as a graph`

## Default Behavior

If no path is provided, use the current directory.

Decision rule:
- build/update graph when the user asks to graph, map, or analyze a corpus
- query existing graph when `graphify-out/graph.json` exists and the user asks about architecture or relationships
- do normal source inspection when no graph exists and graph generation was not requested

Before running, state:
- target path
- whether this is a full build, update, query, path lookup, or explanation
- expected output directory

Primary output directory:

```text
graphify-out/
```

Expected outputs may include:
- `graphify-out/GRAPH_REPORT.md`
- `graphify-out/graph.json`
- `graphify-out/graph.html`

If `graphify-out/graph.json` already exists and the user asks a codebase or architecture question, query the existing graph before broad source scanning:

```powershell
graphify query "question"
graphify path "Concept A" "Concept B"
graphify explain "Concept"
```

Use `graphify-out/GRAPH_REPORT.md` for broad architecture review or when query/path/explain does not provide enough context.

## Safety Rules

- Do not run on huge folders silently. If the corpus is large, summarize size and ask for a narrower path.
- Do not print sensitive skipped file names.
- Do not invent graph edges. Use uncertain/ambiguous labels when needed.
- If Graphify needs installation, network, or dependency changes, ask first.
- After running, verify the output files exist before summarizing results.
- Dirty `graphify-out/` files may be expected after graph updates. Do not treat them as unrelated code changes.
- In multi-repo workspaces, run Graphify inside the actual repo or service folder, not blindly from the workspace parent.
- After code changes in a repo with an existing graph, update the graph if the user wants graph freshness or the local project rules require it.

## Common Commands

```powershell
/graphify .
/graphify . --update
/graphify . --mode deep
/graphify query "What is the auth flow?"
/graphify path "Frontend" "Database"
/graphify explain "AuthModule"
```

## Report Format

After Graphify work, report:
- command or query used
- files produced or graph queried
- most important finding
- any skipped scope or missing evidence
