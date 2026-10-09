# Knowledge Base — Current State

Last updated: 2026-10-09 (bootstrap)

This file is the shared, evolving understanding of the group. It only
changes via pull request. Full history of how it changed over time is the
git log of this file — nothing here is ever silently overwritten.

## Confirmed Findings (Recommended Mechanisms)

_(none yet — SQ-1's baseline catalog is infrastructure, not a finding or a recommended mechanism, per
`methods/falsification-standard.md`. No mechanism has been proposed, trialed, or measured yet.)_

## Baseline (infrastructure, not a finding)

Six real, citable collaboration-friction incidents — five mined from three sibling repos' own meeting
history, plus one (Incident 6) this project's own direct investigation found by checking
`chatgpt/review-*` branch timestamps across all seven mature repos: a synchronized, family-wide stop in
ChatGPT's own activity at 2026-09-29 15:05 UTC, consistent with its own scheduling mechanism dying the
same way `CronCreate` does on Claude's side — not a detection failure on Claude's part. See
`data/baseline-incident-catalog.md`. This is the raw material SQ-4's first protocol experiment (durable
local scheduling, see Mechanisms section above) was designed against.

## Mechanisms Proposed / Trialed, Not Yet Confirmed

**Durable, no-cloud local scheduling (Windows Task Scheduler + CLI `-p`/`--dangerously-skip-permissions`)**
— proposed 2026-10-10, directly responding to a user request. Designed and partially verified (the
invocation mechanism itself tested working up to an authentication boundary); not yet trialed, since it's
blocked on a one-time interactive step (`claude setup-token`) only the user can complete, and deliberately
not auto-created as a standing task without the user's explicit go-ahead given it would run unattended
with all permission checks disabled. See `data/protocol-experiments/durable-local-scheduling.md`.

## Trialed, Not Confirmed Effective

_(none yet. A mechanism that completes a trial without a measured
positive effect belongs here, disclosed with its actual result, not
silently dropped — see `methods/falsification-standard.md`.)_

## Open Questions

- What real, already-disclosed collaboration-friction patterns exist in
  the sibling projects' own comms and meeting history? See SQ-1 —
  **partially answered (2026-10-09)**: five found across 3 of 9 repos, see
  `data/baseline-incident-catalog.md`; six repos still unchecked.
- What metrics can actually be computed mechanically and reproducibly
  from a project's own comms/meeting files, versus sounding appealing but
  requiring unreliable subjective judgment? See SQ-3.
- What does published research on multi-agent AI collaboration already
  establish that this project should build on rather than rediscover?
  See SQ-2.
