# Handoff — feedback-board product grill

The `grill-why` session for the feedback-board MVP is **complete** — all 6 why-branches are
resolved and written into `docs/prd/feedback-board-mvp.md`. Everything needed to pick up the
next phase is in the repo; no prior context window required.

## Next phase — the *how*

Start a fresh session in `/home/davidtaing/feedback-board` and invoke **`grill-with-prd`**,
pointed at `docs/prd/feedback-board-mvp.md`. It owns the **Implementation Decisions** and
**Testing Decisions** sections (left empty on purpose) plus any ADRs and the data model.
Then **`to-issues`** to slice the PRD for AFK agents. Read first:

- `docs/prd/feedback-board-mvp.md` — the resolved PRD (why sections settled).
- `CONTEXT.md` — domain glossary, now sharpened; carries the **deferred data-shape questions**
  the technical grill must answer (unmerge vote/comment ownership, simulated identities,
  where the resolution note lives).
- `docs/canny-feature-reference.md` — concrete Canny feature set (what we cloned / cut).
- `README.md` — product framing, AI-free guardrail, Deno stack.

Project constraint: **no git worktrees** for now — work directly on branches in this repo.

## What the why-grill resolved (all 6 branches DONE)

- **Problem.** Two problems, ordered: (1, primary) practice the grill→docs→issues→**AFK**
  delegation loop; (2, secondary) build PM judgment under ambiguity.
- **User.** Builder is the primary user; **single admission test** — does a feature teach the
  AFK loop or one of the three judgment calls (merge / graveyard / roadmap-commitment)? A thin
  simulated persona is the *instrument* that gives those calls stakes, not a customer to please.
- **Why Now.** No urgency — sequencing: the **first Lane-2 rep where docs must carry contested
  product judgment**, not just CRUD spec.
- **Alternatives.** Feedback board beats Sentry-lite (its dedup is *mechanical*; ours is
  *irreducibly subjective*) and complements the builder's separate CI-as-a-service mechanical
  rep. Null hypothesis loses only because the Why-Now progression holds.
- **Cut-line.** IN: one public board, requests, voting, thin public comments, statuses + a
  "Won't do" graveyard with a required resolution note, public roadmap, merge + **unmerge**.
  Two contested calls settled: notifications **deferred** (graveyard = status taxonomy + public
  copy); comments **IN-thin** (they carry users' words, which is what makes merge consequential).
- **Success.** = shipping the MVP to the cut-line; the loop is being *shaped*, not graded.
  Post-MVP features are each a new grill, not scope-creep. Kill triggers: cut-line won't hold,
  or drift toward AI-over-text.

## Decisions already locked (don't relitigate)

- **AI-free.** No Autopilot / auto-dedup / summarization. Manual merge/unmerge is the
  product. (Strong Out-of-Scope candidate already noted in the PRD.)
- **Stack: Deno + TypeScript**, supply-chain stance per `docs/approved-deps.md`.
- **Lane 2 / AFK build** once docs + issues are ready.
