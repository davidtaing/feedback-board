# PRD: Feedback board MVP — a Canny-style request board, roadmap, and merge workflow

> **Status: why-grill complete.** All 6 branches (Problem, User, Why Now, Alternatives,
> Cut-line, Success) resolved. The *why* sections below are settled. Next: a fresh
> `grill-with-prd` session for the *how* (Implementation + Testing Decisions, ADRs, domain
> model), then `to-issues` to slice for AFK agents.

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

A single **public board** holds **requests**. Customers (simulated identities — no real auth)
post a request directly to the board; there is no submission inbox or triage queue (that is
Canny's Autopilot territory, cut with AI). Each request can be **voted** on — one vote per
identity per request — and the vote count is the visible demand signal. Customers can leave
flat, public **comments** on a request; comments exist specifically because they carry a
user's words and intent, which is what makes the merge call consequential.

Each request carries a **status** along a lifecycle (Under Review → Planned → In Progress →
Complete) plus a **graveyard** state (Won't do) that requires a public **resolution note** —
the structured, honest "no" that closes feedback without leaving false hope. A single public
**roadmap** view organizes requests by status; moving a request's status is the one act that
moves the public commitment.

Admins **merge** duplicate requests into a surviving request: the duplicate's votes sum into
the survivor, its comments roll up under the survivor, and the duplicate redirects to it — so
scattered near-duplicates become one true demand signal. **Unmerge** reverses a merge, the
safety net for the (irreducibly subjective) call of "are these the same?" Merge/unmerge is the
product; everything else exists to give it, the graveyard, and the roadmap real stakes.

## User Stories

**Who this is for.** The primary user is the **builder** — this is a learning project, and
the users are the skill reps named in the Problem Statement. There is a **single admission
test** for every feature: *does it teach the AFK loop, or one of the three PM judgment calls
(merge, the graveyard, roadmap-as-commitment)?* If not, it is cut, no matter how "real" a
product would normally include it.

A **thin simulated persona** — a SaaS team running a public board, plus end-customers who
post and vote — exists *only as the instrument* that gives those judgment calls stakes: the
graveyard only hurts if a customer voted and waited; the roadmap is only a promise if someone
reads it; a merge is only a judgment call if two believable people filed near-duplicates.
The persona is not a customer to please. When "a real product would have X" but X teaches
none of the four, the builder wins and X is cut. Honing product sense is *inside* this lens
(it is the secondary problem), not a second admission path.

### Posting, voting, commenting

1. As a customer, I want to post a request to the public board, so that the team and other
   users can see what I'm asking for.
2. As a customer, I want to vote on a request (one vote per identity), so that demand shows up
   as a count the team can rank by.
3. As a customer, I want to leave a public comment on a request, so that I can add the context
   and intent behind it.

### Statuses and the graveyard

4. As an admin, I want to move a request along a status lifecycle (Under Review → Planned → In
   Progress → Complete), so that the board reflects where each request stands.
5. As an admin, I want to close a request into a graveyard state with a required public
   resolution note, so that I can say "no" honestly instead of leaving it to rot.
6. As a customer, I want to read a closed request's resolution note, so that I understand why
   it won't be built rather than assume I was ignored.

### Merge and unmerge

7. As an admin, I want to merge a duplicate request into a surviving request, so that scattered
   votes and comments consolidate into one true demand signal.
8. As an admin, when I merge, I want the duplicate's votes summed into the survivor and its
   comments rolled up under it, so that no signal is lost in the consolidation.
9. As a customer, I want a merged-away request to redirect me to its survivor, so that I can
   still find where the discussion went.
10. As an admin, I want to unmerge a request I previously merged, so that I can reverse a wrong
    "these are the same" call and restore the original requests.

### Roadmap

11. As a customer, I want a public roadmap that organizes requests by status, so that I can see
    what's planned, in progress, and shipped.
12. As an admin, I want a request's place on the roadmap to follow its status, so that updating
    one status is the single act that moves the public commitment.

## Why Now (optional)

No external urgency — the reason is **sequencing within the Lane-2 progression**, written
plainly rather than dressed as a deadline. Prior Lane-2 reps (CRUD clones like Dub, Tally)
exercised the *pipeline mechanics* — grill → docs → issues → AFK — but the docs were easy
because the product calls were easy. The feedback board is the **first rep where the docs
have to carry contested product judgment** (merge reversibility, the graveyard,
roadmap-as-commitment) precisely enough for an AFK agent to build from. It's the rung where
the hard half of the loop — *judgment*-into-docs, not just CRUD-spec-into-docs — first gets
stressed. That progression is the "now."

## Success Criteria (optional)

**Success for this milestone = shipping the MVP to the cut-line** (the Solution + stories 1–12,
nothing past the Out-of-Scope line). This is a *learning rep*: the grill → docs → issues → AFK
loop is being *shaped*, not graded — so the bar is reaching a working MVP, not proving the
process ran flawlessly. How much intervention the AFK build needed is useful data for the next
rep, not a failure condition. Getting reps in is the meta-goal.

**Deliberately open:** whether to continue past the MVP is a *future* decision, not part of this
one. Adding features later is fine — but each is a **new grill / new PRD**, not scope-creep into
this build.

**Kill / revisit triggers:**

- **The cut-line won't hold during the build** — if "just one more feature" keeps pulling at
  *this* MVP, stop and re-grill the cut-line rather than quietly moving the line.
- **Drift toward AI-over-text** (auto-dedup, summarization) — kill on sight; locked guardrail.

## Alternatives Considered

- **Do nothing.** Nothing breaks externally — no user is waiting. The cost is forfeiting the
  first *judgment-heavy* doc rep (see Why Now), so "do nothing" loses only because the
  progression claim holds. The two are linked.
- **Sentry-lite (error-grouping clone) — the real rival.** Same product-insight *shape*
  (grouping/dedup), and arguably a sharper dedup problem. Rejected on two legs:
  1. **Mechanical vs. subjective dedup.** Sentry groups by stack-trace fingerprint — largely
     *computable* (same fingerprint = same bug), so the judgment trivializes or begs to be
     automated, colliding with the AI-free guardrail. Feedback-dedup is *irreducibly
     subjective* — there is no ground truth for "same request," so the human merge call
     cannot be automated away without changing what the product is. That subjectivity is the
     lesson (the secondary problem by name).
  2. **Portfolio complementarity.** The builder is already getting a heavy *mechanical* rep
     from a separate CI-as-a-service project. A second mechanical-grouping clone duplicates
     that rep. The feedback board is engineering-light / judgment-heavy — it covers the rep
     the CI project does not, and is the lighter build wanted now. Deliberate coverage, not
     laziness.
- **Other CRUD clones (Dub, Tally).** Product-easy — they exercise pipeline mechanics but not
  the judgment-into-docs muscle. Already covered by prior Lane-2 reps (see Why Now).

## Out of Scope

- **AI / Autopilot-style auto-dedup, summarization** — excluded by the AI-free guardrail; the
  manual merge is the point, and AI-over-text is the employer no-go domain.
- **Notifications (in-app feed or email) on status change** — *deferred, not rejected.* The
  graveyard judgment lives in the status taxonomy + public copy (see Solution), which is fully
  exercised without a delivery channel; a feed is CRUD plumbing that adds per-user
  infrastructure a solo MVP doesn't need. Plain CRUD, not the AI no-go domain — safe to revisit
  later (or build for real at work).
- **Multiple boards / private or limited-visibility boards** — one public board exercises all
  three judgment calls; more boards add infra, not judgment, and private boards contradict the
  roadmap-as-public-commitment lesson.
- **Submission inbox / triage queue** — posts land directly on the board; a pre-board triage
  queue is Canny's Autopilot territory and reintroduces the AI-shaped step we cut.
- **Bulk merge** — single merge already teaches the call; bulk is a scale convenience.
- **Internal (team-only) and pinned comments** — comments are in only to carry users' words for
  the merge lesson; internal/pinned are admin-workflow nuance that teaches nothing here.
- **Tags / categories / labels** — organization, not judgment.
- **Segmentation, MRR-impact sorting, prioritization scoring** — a *different* judgment axis
  (prioritization), and they need billing/customer data the simulated persona doesn't have.
- **Changelog** — a downstream publishing surface; teaches none of the three calls.
- **Real authentication / account linking, vote-on-behalf** — the persona is simulated; seeded
  identities suffice. Real auth is infra, not judgment.
- **Integrations and custom branding** — pure product realism; no judgment content.

## Implementation Decisions

_Owned by the technical session (`grill-with-prd`). ADR-worthy calls link out to `docs/adr/`._

### Merge / unmerge data shape

Non-destructive **redirect pointer**: a request carries a nullable `merged_into` to its
survivor. Merge sets that one field — votes/comments are never relocated. Survivor's vote count
(`COUNT(DISTINCT identity)`) and comment list are aggregated at read time across the survivor
and its duplicates; the duplicate redirects, so post-merge activity lands natively on the
survivor. Unmerge clears the pointer; the duplicate returns with exactly what it had at merge
time. Merges are **depth-1** (a duplicate can't be a survivor and vice-versa) — no chains, no
recursive queries. Full rationale and trade-offs: [ADR-0002](../adr/0002-merge-by-redirect-pointer.md).

### Persistence & data access

Postgres via docker-compose; runtime is **Node + pnpm** ([ADR-0004](../adr/0004-switch-runtime-to-node.md),
reversing the original Deno choice — React/Node is the AFK-reliable stack; supply-chain posture
reconstructed in a committed `.npmrc`: `ignore-scripts` + `minimumReleaseAge` + pins + allowlist).
`pg` driver behind Kysely's `PostgresDialect`; **Kysely** for type-safe queries (no ORM);
**Kysely's migrator** for migrations; **`kysely-codegen`** (dev-only) generates the `Database`
type from the migrated schema. Workflow rule: **migrate, then regenerate types.** Data-stack
detail: [ADR-0003](../adr/0003-postgres-kysely-data-stack.md).

### Simulated identities

No real auth. A seeded **`identity`** table (`id`, `display_name`, optional `org`, `role`) is
populated by a seed migration for deterministic demos/tests. `role` is `customer` (posts,
votes, comments) or `admin` (status moves, graveyard, merge/unmerge); admin controls render
only when an admin identity is selected. The current identity lives in a cookie, changed via a
switcher ("choosing a hat"). One-vote-per-identity is a `(request_id, identity_id)` unique
constraint — enforced by the DB, not app code.

## Testing Decisions

_Owned by the technical session. Left empty._
