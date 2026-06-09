# Handoff — feedback-board technical grill (the *how*)

The `grill-with-prd` session for the feedback-board MVP is **in progress, ~60% done**. The two
architecturally heavy, hard-to-reverse calls (merge model, data stack) are settled and recorded;
what remains is more contained. Everything decided is already written to the repo — no prior
context window required to resume.

**Branch:** `grill/feedback-board-mvp-how` (off clean `main`; PR not yet opened).
**Repo is now public.** Outbound links to the private `side-projects` doc were scrubbed (PR #3).

## How to resume

Start a fresh session, invoke **`grill-with-prd`** on `docs/prd/feedback-board-mvp.md`, and pick
up at **node 5** below. Read first: the PRD (Implementation Decisions section), `CONTEXT.md`,
and ADR-0002 / ADR-0003.

## Locked this session (with docs)

1. **Merge/unmerge data shape** — non-destructive `merged_into` redirect pointer; counts/comments
   aggregated at read time; unmerge = clear the pointer; **depth-1** (no chains). Post-merge
   activity belongs to the survivor and stays there on unmerge. → [ADR-0002](adr/0002-merge-by-redirect-pointer.md),
   PRD Implementation Decisions, CONTEXT (Merge/Survivor/Unmerge).
2. **Persistence stack** — Postgres via docker-compose; runtime stays **Deno** with `npm:` deps
   (no `postinstall` → supply-chain stance holds); `npm:pg` + **Kysely** (queries + migrator) +
   **`kysely-codegen`** (dev-only, run via node/npx) for types. Rule: migrate → regenerate types.
   → [ADR-0003](adr/0003-postgres-kysely-data-stack.md), `approved-deps.md` (3 rows added).
3. **Simulated identities** — seeded `identity` table (`role`: customer | admin), current
   selection in a cookie via a switcher ("choosing a hat", not auth); `(request_id, identity_id)`
   unique constraint. Prior art (Canny SSO: signed JWT, HS256, vouched-for stable user id) confirms
   the cut — auth is a separable layer; same data shape. → PRD Implementation Decisions, CONTEXT (Identity).
4. **Vote semantics** — fell out of #1 and #3: dedup via `COUNT(DISTINCT identity)` across the
   merged set; one-per-identity via the unique constraint. No separate decision needed.

## Remaining (nodes 5–8)

5. **Resolution note placement (graveyard "Won't do").** *Merge needs no separate metadata record*
   — the pointer carries it (ADR-0002) — so the only note to place is the graveyard one. Question:
   field on the request, on a status-transition record, or its own record. **Tightly coupled to
   node 6 — settle 6 first.**
6. **Status lifecycle.** Strict state machine (explicit allowed transitions) vs. free transitions.
   *Leaning:* an explicit transition set, and likely a status-change/transition record (gives
   history + a natural home for the resolution note + drives the roadmap). Confirm against
   simplicity.
7. **App shape.** Server-rendered vs. API+SPA. *Leaning:* server-rendered for an engineering-light,
   AFK-delegable build — but the rendering approach (plain `Deno.serve` + JSX/templates vs. a
   framework like Fresh) is a real sub-decision with a dep implication. The biggest remaining call.
8. **Testing decisions.** Integration tests against an **ephemeral Postgres** (consequence of
   ADR-0003 — no in-process file). Decide the ephemeral-DB strategy (compose service / fresh
   schema per run) and how much to test the merge/unmerge aggregation directly.

## After the grill

`to-issues` to slice for AFK agents. Issue #1 is the **walking-skeleton substrate** (project boots,
docker-compose Postgres connects, one request renders) — setup is delegated, not built in the grill.
