# Approved dependencies policy

Per the project-direction doc: agents will happily `npm install` anything. This file is the
allowlist. **Adding a dependency not listed here requires explicit sign-off** (open an issue
or ask before adding).

## Rules

1. **Prefer the Node standard library and Web platform APIs** before reaching for a dep.
2. **Supply-chain controls are committed in `.npmrc`** (see [ADR-0004](adr/0004-switch-runtime-to-node.md)):
   `ignore-scripts=true` (no `postinstall`/lifecycle execution) + `minimumReleaseAge` (no
   freshly-published versions). Do not weaken these per-install.
3. **Pin versions.** No floating ranges; commit the lockfile and install with `--frozen-lockfile`.
4. **Justify each dep** in the PR that introduces it: what it does, why std lib won't,
   and a glance at its maintenance / transitive footprint.
5. **No AI / LLM / ASR / speech / NLP packages** — out of scope by product guardrail and
   the overlap filter.

## Approved list

| Dependency | Purpose | Added in |
|------------|---------|----------|
| `pg` (pinned) | Postgres driver backing Kysely's `PostgresDialect`. Std lib has no Postgres client; Kysely's first-class support targets node-postgres. | ADR-0003 |
| `kysely` (pinned) | Type-safe query builder + migrator. Replaces both an ORM and hand-written SQL strings; gives AFK agents compile-time column safety. | ADR-0003 |
| `kysely-codegen` (pinned, **dev-only**) | Generates the Kysely `Database` type from the migrated schema so query types can't drift. Not a runtime dependency. | ADR-0003 |

## Rejected / parked

| Dependency | Reason |
|------------|--------|
| _(none yet)_ | |
