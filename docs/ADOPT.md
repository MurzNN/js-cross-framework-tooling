# Adopt js-cross-framework-tooling

Checklist for a cross-framework component monorepo (`packages/core` + `packages/vue` + `packages/react`).

## 1. Copy scripts

From this repo into the consumer:

```text
scripts/readme-packages.mjs
scripts/prepend-changelog.mjs
scripts/github-release.mjs
```

## 2. Config files

1. Copy [`templates/readme-packages.config.mjs.example`](../templates/readme-packages.config.mjs.example) → `readme-packages.config.mjs` and fill in names/URLs.
2. Copy [`presets/release-it.synced-adapters.json`](../presets/release-it.synced-adapters.json) → `.release-it.json` (adjust only if your adapter dirs differ).
3. Add a root `CHANGELOG.md` intro (or let `prepend-changelog.mjs` create one on first release).

## 3. package.json

```json
{
  "scripts": {
    "readme:packages": "node scripts/readme-packages.mjs",
    "release": "release-it"
  },
  "devDependencies": {
    "@release-it/bumper": "^7.0.5",
    "release-it": "^19.0.0"
  }
}
```

Pin versions to whatever is current when you adopt; run `pnpm install`.

Version source of truth for bumps is `packages/vue/package.json` (via `@release-it/bumper` `in`). Bumper also writes `packages/react/package.json` and the root `package.json`. The npm plugin is disabled (`"npm": false`) so it does not fight bumper with `npm version` / “Version not changed”.

## 4. Workflows

Copy [`templates/workflows/ci.yml`](../templates/workflows/ci.yml) and [`templates/workflows/publish.yml`](../templates/workflows/publish.yml) into `.github/workflows/`.

In `publish.yml`, replace `vue-COMPONENT` / `react-COMPONENT` with your package names.

Configure npm Trusted Publishers for each published package with workflow filename **`publish.yml`**.

## 5. AGENTS.md

Paste [`templates/AGENTS-publishing.md`](../templates/AGENTS-publishing.md) into your agent guide (adjust package names).

## 6. Verify

```bash
pnpm readme:packages --dry-run   # if you add a dry-run passthrough
pnpm release --dry-run
```

`pnpm release` (without dry-run) will commit, tag, push, and trigger `publish.yml`.

## Updating from this repo

Re-copy scripts/presets/templates when tooling improves. There is no cross-repo `workflow_call` for publish (OIDC Trusted Publishing requires the workflow file to live in the package repo).
