# Approved dependencies policy

Per the project-direction doc: agents will happily `deno add` / `npm install` anything.
This file is the allowlist. **Adding a dependency not listed here requires explicit
sign-off** (open an issue or ask before adding).

## Rules

1. **Prefer the Deno standard library and Web platform APIs** before reaching for a dep.
2. **No packages with `postinstall`/lifecycle scripts.** (Deno doesn't run them by
   default — keep it that way; don't enable `--allow-scripts` broadly.)
3. **Pin versions.** No floating ranges.
4. **Justify each dep** in the PR that introduces it: what it does, why std lib won't,
   and a glance at its maintenance / transitive footprint.
5. **No AI / LLM / ASR / speech / NLP packages** — out of scope by product guardrail and
   the overlap filter.

## Approved list

| Dependency | Purpose | Added in |
|------------|---------|----------|
| _(none yet)_ | | |

## Rejected / parked

| Dependency | Reason |
|------------|--------|
| _(none yet)_ | |
