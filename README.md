# feedback-board

A Canny-style customer-feedback / roadmap tool. A **Lane 2** project (per a private project-direction doc): a product-intuition rep built
via **grill → docs → issues → AFK**.

## What this is (and isn't)

The interesting part is **product judgment, not CRUD**. The hard calls are:

- **Dedup / merging** — when are two submissions the "same" request? Who decides, and
  how reversible is it?
- **The "graveyard" problem** — what happens to feedback that will never be built?
  Closing it honestly vs. leaving false hope.
- **Transparency vs. flexibility** — a public roadmap creates commitment; how much do
  you expose without boxing yourself in?

**Guardrail: keep it AI-free.** No AI-over-text (no auto-dedup, no summarization). The
product is the judgment calls; introducing AI here would (a) hide the judgment behind a
model and (b) drift toward the employer's no-go domain (AI-over-language). See the
overlap filter in the (private) project-direction doc.

## Stack

- **Runtime: Deno** — built-in permissions, no `postinstall` scripts, native TS. Chosen
  for the npm supply-chain concern flagged in the plan doc.
- **TypeScript** — Lane-2 / AFK language (best agent productivity).
- **Dependencies:** see [docs/approved-deps.md](docs/approved-deps.md). Agents must not
  add deps outside that policy without sign-off.

## Process & docs

This repo follows the grill → docs → issues workflow:

- [CONTEXT.md](CONTEXT.md) — domain language and the model (kept current as decisions land).
- [docs/prd/](docs/prd/) — product requirements, one per feature. Built via the product grill.
- [docs/adr/](docs/adr/) — architecture decision records.

## Status

Setup / pre-PRD. Next: product grill to establish the why and the cut-line, producing
the first PRD in `docs/prd/`.
