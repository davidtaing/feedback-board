# Canny feature reference

Research notes on what Canny.io actually does, so we know what we're cloning. Built from
public sources only (Canny's own marketing + help center). _Reference, not commitment —
the cut-line is decided in the grill, not here._

## Core surface

- **Feedback boards** — public or private boards where users post feature requests / bug
  reports / ideas. Multiple boards, each with privacy settings (public / private / limited).
- **Voting** — one vote per user per post; vote totals surface demand. Admins can "vote on
  behalf" of a customer.
- **Comments** — public discussion on a post; internal (team-only) comments; pinned comments.
- **Statuses** — posts move through lifecycle states: Under Review → Planned → In Progress →
  Complete (and Closed / won't-do — the "graveyard"). Voters are emailed on status change.
- **Roadmap** — public or private view organizing posts by status; posts move along it as
  status changes. The transparency/commitment surface.
- **Changelog** — published product updates; embeddable widget; release scheduling.

## The judgment-heavy bits (our actual product)

- **Merge / unmerge** — combine duplicate posts into one; votes and comments roll up into the
  surviving post; the merged post shows in comments. Unmerge reverses it. Bulk merge exists.
- **The graveyard** — closing feedback that won't be built, honestly, without leaving false
  hope. (Canny handles via Closed status + notification.)
- **Transparency vs. flexibility** — how much the public roadmap commits you to.

## Organization / filtering

- Tags & categories, labels (by product area), user segmentation (e.g. paying customers),
  voter segmentation, MRR-impact sorting, prioritization scoring.

## Admin / integrations

- Moderation controls, user identification (link feedback to accounts), integrations with
  external tools, custom branding.

## AI (Autopilot) — DELIBERATELY EXCLUDED

Canny's modern dedup is **AI-powered ("Autopilot")**: it auto-detects similar posts and can
merge a new post into an existing one as a vote + internal comment. **We strip this on
purpose** — the manual merge/unmerge *is* the judgment call we're here to practice, and
AI-over-text drifts into the employer no-go domain (see the overlap filter in the private
project-direction doc).
Our clone keeps the human merge decision and the unmerge safety net; it does not predict.

## Sources

- [Canny — Features](https://canny.io/features)
- [Merging and unmerging posts](https://help.canny.io/en/articles/5776649-merging-and-unmerging-posts)
- [Managing posts](https://help.canny.io/en/articles/3827592-managing-posts)
- [Autopilot (formerly Inbox)](https://help.canny.io/en/articles/8202451-autopilot-formerly-inbox)
- [Public roadmap](https://help.canny.io/en/articles/3828148-public-roadmap)
- [Canny 101](https://help.canny.io/en/articles/3816826-canny-101)
