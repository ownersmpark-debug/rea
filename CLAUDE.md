# Claude Code

@AGENTS.md

The guidelines above are shared with every coding agent and are authoritative.
This file only adds notes specific to Claude Code.

## Claude Code setup

- Project skills in `.claude/skills/` are links to `.agents/skills/`. Edit the
  skill under `.agents/skills/`; never copy it into `.claude/`.
- `.claude/settings.json` holds shared permissions and a hook that runs
  `oxfmt` on files Claude edits. Personal overrides belong in
  `.claude/settings.local.json`, which is ignored.
- Run `npm ci` before the first check so `oxfmt`, `oxlint`, `turbo`, and
  `vitest` resolve from `node_modules/`.

## Working loop

1. Read the owning module and its tests before editing.
2. Make the change, then run the narrowest relevant check:
   `npm run test:local -- PATH...` for source tests, or
   `npm run test:focused -- PATH...` when built artifacts are needed.
3. Run `npm run check:fast` before committing; the pre-push hook runs it too.
4. Run `npm run docs:check` when contracts, catalogs, or docs change.

Do not edit generated outputs (`dist/`, `skills/`,
`docs/public/product-catalog.json`, `docs/verification/managed-conformance-*.json`).
Change their sources and regenerate.
