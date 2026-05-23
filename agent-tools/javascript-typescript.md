# JavaScript/TypeScript

Use this rule automatically when the repo is a JavaScript or TypeScript project.

## Detect JS/TS Repos

Treat the workspace as JS/TS when you see any of:
- `package.json`
- `bun.lock`
- `bun.lockb`
- `package-lock.json`
- `pnpm-lock.yaml`
- `yarn.lock`
- `tsconfig.json`
- `biome.json`
- `biome.jsonc`
- `.js`, `.jsx`, `.ts`, or `.tsx` source files

In multi-repo workspaces, inspect the nearest app/service directory first. Do not assume the workspace root has the real scripts.

## Package Manager Preference

Prefer the package manager shown by the lockfile:
- `bun.lock` or `bun.lockb` -> use `bun`
- `package-lock.json` -> use `npm`
- `pnpm-lock.yaml` -> use `pnpm`
- `yarn.lock` -> use `yarn`

If multiple lockfiles exist, prefer the manager that matches `packageManager` or the script bodies. For example, if scripts use `bun` or `bunx`, use Bun even when `package-lock.json` is also present.

If no lockfile exists, inspect `package.json` and README before choosing. If unclear, prefer `npm` for compatibility.

## Default Command Style

Use package scripts first:

```powershell
npm run dev
npm run lint
npm run test
npm run build
```

When the repo uses Bun:

```powershell
bun run dev
bun run lint
bun run test
bun run build
```

Common scripts to look for:
- `dev`
- `prod`
- `start`
- `build`
- `lint`
- `lint:fix`
- `format`
- `format:check`
- `typecheck`
- `test`
- `test:run`
- `test:coverage`
- `preview`
- `doctor`

Do not call tools directly (`biome`, `tsc`, `vite`, `next`, `jest`, `vitest`) unless:
- the package script is missing
- the repo documents the direct command
- the user specifically asks for it

## Biome

If `biome.json` or `biome.jsonc` exists, assume Biome is the preferred formatter/linter unless package scripts say otherwise.

Prefer:

```powershell
npm run lint
```

or:

```powershell
bun run lint
```

For fixable lint/format work, prefer existing scripts such as:

```powershell
npm run lint:fix
npm run format
bun run lint:fix
bun run format
```

Only use direct Biome commands after checking scripts:

```powershell
npm exec biome check .
bunx biome check .
```

Do not run formatting writes automatically unless the user asked for formatting or the fix requires it.

## Before Editing

Check the project shape first:
- package manager
- framework
- available scripts
- lint/format tools
- test runner
- TypeScript config
- app entrypoints

Prefer reading:
- `package.json`
- lockfile name only unless dependency details matter
- `biome.json` or `biome.jsonc`
- `tsconfig.json`
- README

If repo docs mention commands that do not match the current manifests, trust the current manifests and call out the mismatch.

## Verification

For code changes, verify with the smallest relevant command first:
- targeted test for bug fixes
- `npm run lint` or `bun run lint` for lint-sensitive edits
- `npm run typecheck` or `bun run typecheck` when TypeScript interfaces changed
- `npm run test` or `bun run test` when behavior may be affected
- `npm run build` or `bun run build` for framework, routing, or type-sensitive changes

If a script does not exist, report that clearly and fall back to the closest documented command.

## Dependency Rules

- Do not add dependencies unless necessary.
- Use the repo's package manager.
- Prefer `npm install <package>` or `bun add <package>` for runtime dependencies.
- Prefer `npm install -D <package>` or `bun add -d <package>` for development dependencies.
- Do not edit lockfiles manually.
- After dependency changes, run the relevant verification command.

## Runtime Rules

When the user asks to run the app, prefer the repo script:

```powershell
npm run dev
```

or:

```powershell
bun run dev
```

For production-like runs, prefer:

```powershell
npm run build
npm run start
```

or:

```powershell
bun run build
bun run start
```

## Style Rules

- Preserve existing component and module patterns.
- Keep TypeScript types explicit where the repo already does.
- Avoid broad refactors while fixing bugs.
- Prefer existing utilities, hooks, and design-system components.
- Do not introduce new state management, routing, styling, or build tools without approval.
