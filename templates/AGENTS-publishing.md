## Publishing

- npm Trusted Publishing (OIDC): `.github/workflows/publish.yml` on `v*` tags
- Publishes `vue-…` + `react-…` adapters only (not core)
- Trusted Publisher workflow filename on npmjs.com must match: `publish.yml`
- Release: `pnpm release` (patch) / `pnpm release minor|major|x.y.z` — [release-it](https://github.com/release-it/release-it) bumps both adapters, regenerates package READMEs, prepends `CHANGELOG.md`, commits, tags `vX.Y.Z`, pushes, creates a GitHub Release
- `CHANGELOG.md` is generated on release from commit subjects since the previous `v*` tag — do not edit it by hand for routine work; write clear commit messages instead
- `pnpm readme:packages` — regenerate `packages/{vue,react}/README.md` only
- Root `README.md` markers: visible `<!-- pkg:all|omit -->` regions; hidden package-only `<!-- pkg:vue|react|core … -->` comment blocks (body must not contain `-->`)
- Shared templates/scripts: https://github.com/MurzNN/js-cross-framework-tooling
