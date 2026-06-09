# 4. Switch runtime from Deno to Node + pnpm

Date: 2026-06-09

## Status

Accepted — supersedes the **runtime** decision in [ADR-0003](0003-postgres-kysely-data-stack.md).
(The rest of ADR-0003 — Postgres, Kysely, the migrator, kysely-codegen, raw-SQL-as-escape-hatch
— still stands; only the Deno/`npm:`-compat parts are replaced.)

## Context

ADR-0003 kept the runtime on Deno (a why-grill decision) primarily for its supply-chain
posture: Deno does not execute `postinstall`/lifecycle scripts by default. But the project's
*primary* purpose is the grill → docs → issues → **AFK** loop — the UI/CRUD layer is explicitly
the delegable half. That reframes the selection criterion: the runtime should optimize for
**agent reliability**, not for fewest defaults-on protections.

Two facts then push off Deno:

- **React/Node is the deepest-trained stack.** AFK agents produce it with the fewest mistakes,
  and the maintainer has a React background (so agent output is reviewable). On Deno, "React"
  meant Preact/Fresh or a community Vite path — lower agent familiarity and real compat friction
  (e.g. running `kysely-codegen`). On Node those frictions vanish and *real* React is first-class.
- **The supply-chain concern is mitigable on Node** to a posture substantially equivalent to
  Deno's, without giving up the ecosystem.

## Decision

Runtime is **Node + pnpm**. The supply-chain protection that justified Deno is reconstructed
explicitly and **committed in `.npmrc`** so it is inherited, not remembered:

- `ignore-scripts=true` — disables `postinstall`/lifecycle script execution. This is the direct
  replacement for Deno's core default.
- `minimumReleaseAge` (~7–14 days) — refuses freshly-published versions, defeating the dominant
  npm attack (hijacked-maintainer / poisoned-release caught and yanked before adoption).
- Pinned exact versions + lockfile + `--frozen-lockfile`, plus the existing `approved-deps`
  allowlist (small, vetted surface).

## Consequences

- The protections are now **opt-in config rather than runtime defaults** — an agent could forget
  them. Mitigated by committing `.npmrc` so the posture ships with the repo.
- Acceptable residual risk for this project: a public learning board with simulated identities,
  no real secrets or PII.
- Node removes the Deno-compat friction ADR-0003 worked around — `kysely-codegen` and Vite are
  Node-native, so no `npm:` specifiers and no node/npx workaround needed.
- App shape (the open node 7) simplifies: Fresh/Preact drops out; the live options are a **React
  SPA + Node API** or a **React meta-framework** (Next / Remix-React-Router). Sub-choice still open.
