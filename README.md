# js-cross-framework-tooling

Shared release, changelog, README, and CI templates for **cross-framework** JS component monorepos (framework-agnostic core + Vue / React / future adapters).

Used by:

- [js-pointing-bubble](https://github.com/MurzNN/js-pointing-bubble)
- [js-pointing-cursor](https://github.com/MurzNN/js-pointing-cursor)

## What this repo provides

| Path | Purpose |
|------|---------|
| [`presets/release-it.synced-adapters.json`](presets/release-it.synced-adapters.json) | [release-it](https://github.com/release-it/release-it) recipe: synced vue+react bumps, CHANGELOG, GitHub Release, no local npm publish |
| [`scripts/readme-packages.mjs`](scripts/readme-packages.mjs) | Split root `README.md` into per-package READMEs via `<!-- pkg:* -->` markers |
| [`scripts/prepend-changelog.mjs`](scripts/prepend-changelog.mjs) | Prepend a Keep-a-Changelog-style section from commit subjects (release-it hook) |
| [`scripts/github-release.mjs`](scripts/github-release.mjs) | Idempotent `gh release create` from `CHANGELOG.md` (CI fallback) |
| [`templates/workflows/`](templates/workflows/) | Copy-into-repo CI + OIDC publish workflows (compose official Actions) |
| [`docs/ADOPT.md`](docs/ADOPT.md) | Adoption checklist |

## Design notes

- **Release tooling:** reuse [release-it](https://github.com/release-it/release-it) + [`@release-it/bumper`](https://github.com/release-it/bumper) — do not reinvent bump/tag/GH Release.
- **npm publish:** stays in each consumer’s `publish.yml` via [Trusted Publishing (OIDC)](https://docs.npmjs.com/trusted-publishers/). Do **not** call publish through a cross-repo `workflow_call` — npm binds trust to the workflow filename in the package repo.
- **Workflows:** templates to copy, not reusable `workflow_call` workflows. They only compose `pnpm/action-setup`, `actions/setup-node`, Pages actions, etc.

## Quick start

See [docs/ADOPT.md](docs/ADOPT.md).

## License

MIT
