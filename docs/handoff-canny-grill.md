# Handoff — feedback-board product grill

Picking up the `grill-why` session for the feedback-board MVP in a fresh Claude session
in this repo. Everything you need is in the repo; no prior context window required.

## How to resume

Start a session in `/home/davidtaing/feedback-board` and invoke **`grill-why`**. Point it
at `docs/prd/feedback-board-mvp.md`. Read first:

- `docs/prd/feedback-board-mvp.md` — the PRD being built; Problem branch is done.
- `docs/canny-feature-reference.md` — concrete Canny feature set (what we're cloning).
- `CONTEXT.md` — domain glossary (still stubbed; sharpen as branches resolve).
- `README.md` — product framing, AI-free guardrail, Deno stack.

## Where the grill stands

The why-tree has 6 branches. Resolved so far:

- **[DONE] Problem.** Two problems, ordered: **(1, primary)** practice the
  grill→docs→issues→**AFK** delegation loop; **(2, secondary)** build product-management
  judgment under ambiguity (dedup/merge, the graveyard, transparency-vs-flexibility).
  Written into the PRD's Problem Statement.

Still open:

- **User** — confirm the builder-as-user framing; name precisely what each branch teaches.
- **Why Now** — provisional: not urgency, just the next Lane-2 rep. Confirm or sharpen.
- **Alternatives** — null hypothesis + the other backlog clones (Dub, Tally, Sentry-lite).
  Sentry-lite is the real rival ("grouping/dedup as the product insight") — settle why
  the feedback board wins, or don't.
- **Cut-line** — THE big one. Canny is large (boards, voting, statuses, roadmap,
  changelog, merge/unmerge, tags, segmentation, MRR sorting, integrations). The MVP must
  stop somewhere defensible. Likely core: a board + posts + voting + statuses + a roadmap
  view + manual merge/unmerge. Likely cut: changelog, segmentation, MRR, integrations,
  multi-board. Decide and justify the line.
- **Success** — what outcome would make us kill or revisit it.

## Decisions already locked (don't relitigate)

- **AI-free.** No Autopilot / auto-dedup / summarization. Manual merge/unmerge is the
  product. (Strong Out-of-Scope candidate already noted in the PRD.)
- **Stack: Deno + TypeScript**, supply-chain stance per `docs/approved-deps.md`.
- **Lane 2 / AFK build** once docs + issues are ready.

## After the grill

When the why branches resolve, hand off to a fresh **`grill-with-prd`** session for the
*how* (domain model, ADRs, implementation sections), then **`to-issues`** to slice it for
AFK agents.
