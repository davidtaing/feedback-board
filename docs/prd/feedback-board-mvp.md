# PRD: Feedback board MVP — a Canny-style request board, roadmap, and merge workflow

> **Status: grill in progress.** Branch 1 (Problem) resolved. Branches 2–6 (User, Why
> Now, Alternatives, Cut-line, Success) pending — see
> [docs/handoff-canny-grill.md](../handoff-canny-grill.md). Resume with `grill-why` in
> this repo.

## Problem Statement

This is a **learning project**, so the problem is what understanding is missing — and
there are two, honestly ordered:

1. **(Primary) Practice the grill → docs → issues → AFK delegation loop.** The durable
   skill being built is *front-loading judgment into docs precise enough that AFK agents
   can execute the build*, then leveraging that. The feedback board is a good vehicle
   because it is engineering-easy / product-hard: the CRUD is delegable, so the value
   lives in the design decisions, not the implementation — exactly the split the
   two-lane model is built around.

2. **(Secondary) Build product-management judgment under ambiguity.** The PM space is a
   standing interest, and a feedback board concentrates three calls with no correct
   answer, only a defensible one:
   - **Dedup / merge** — when are two requests "the same," who decides, and how
     reversible is being wrong? (Canny now does this with AI; we keep it manual on
     purpose — the manual decision *is* the lesson.)
   - **The graveyard** — how to close feedback that will never be built without lying to
     users.
   - **Transparency vs. flexibility** — a public roadmap is a promise; how much to commit.

CRUD clones (Dub, Tally) are product-easy and don't force these. The feedback board does,
while staying AI-free (no AI-over-text), which keeps it clear of the employer overlap
filter.

## Solution

_Pending — resolves during the grill (likely after the Cut-line branch). Will describe
the MVP shape end to end using CONTEXT.md terms._

## User Stories

_Pending — built during the User / Cut-line branches._

## Why Now (optional)

_Pending. Provisional: sequencing isn't urgency-driven — this is the next Lane-2 rep, and
the AFK pipeline is the thing being practiced. To confirm in the grill._

## Success Criteria (optional)

_Pending._

## Out of Scope

_Pending. Strong candidate already: **AI / Autopilot-style auto-dedup** — excluded by the
AI-free guardrail; the manual merge is the point._

## Implementation Decisions

_Owned by the technical session (`grill-with-prd`). Left empty._

## Testing Decisions

_Owned by the technical session. Left empty._
