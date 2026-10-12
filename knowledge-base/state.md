# Knowledge Base — Current State

Last updated: 2026-10-09 (bootstrap)

This file is the shared, evolving understanding of the group. It only
changes via pull request. Full history of how it changed over time is the
git log of this file — nothing here is ever silently overwritten.

## Confirmed Findings (Recommended Mechanisms)

_(none yet — SQ-1's baseline catalog is infrastructure, not a finding or a recommended mechanism, per
`methods/falsification-standard.md`. No mechanism has been proposed, trialed, or measured yet.)_

## Baseline (infrastructure, not a finding)

Seven real, citable collaboration-friction incidents — five mined from three sibling repos' own meeting
history, plus two (Incidents 6-7) this project's own direct investigation found by checking
`chatgpt/review-*` branch timestamps across all seven mature repos: a synchronized, family-wide stop in
ChatGPT's own activity at 2026-09-29 15:05 UTC, consistent with its own scheduling mechanism dying the
same way `CronCreate` does on Claude's side — not a detection failure on Claude's part — followed by a
second synchronized resumption replicating the same pattern. See `data/baseline-incident-catalog.md`. This
is the raw material SQ-4's first protocol experiment (durable local scheduling, see Mechanisms section
above) was designed against. **Update (2026-10-12)**: SQ-3's metrics framework now exists too — six
metrics, each grounded in a specific incident above, with exact computation procedures (several fully
mechanical). Three appealing-sounding metrics explicitly rejected as not reliably computable (duplicated-
work count, error-propagation caught-vs-missed — structurally uncountable on the "missed" side — and a
reporting-style correlation). See `data/metrics-framework.md` and
`logs/2026-10-12-sq3-metrics-framework-first-draft.md`. **Update (2026-10-12, same day)**: SQ-1's
second mining pass checks 5 more sibling repos. `atari-2600-collective` and `earth-anomalies-
collective` have no meetings yet (disclosed null result). `linear-a-collective` yields a genuinely
new **Incident 8** — the first in this catalog with an actual measured before/after effect (a
named process fix, then a measured result two cycles later). 8 of 9 sibling repos now checked at
least once. See `logs/2026-10-12-sq1-second-pass-five-more-repos.md`.

**Update (2026-10-10) — mapped against MAST's failure taxonomy (SQ-2), a real negative result**: only
Incident 1 has even a loose MAST analog (FM-3.2, no/incomplete verification); the other six don't map
cleanly. MAST's taxonomy is built from fully-autonomous, continuously-running multi-agent frameworks —
structurally different from this family's own async, git-mediated, session-scoped, human-supervised model.
Five of our own incidents (2-7) describe failure types — cross-session scheduling death above all — that
have no equivalent in a framework that assumes the agents are always actively running. See
`logs/2026-10-10-sq2-mapping-baseline-incidents-against-mast.md`. Practical consequence: SQ-3's metrics
framework should not adopt MAST's 14 modes wholesale; borrow FM-3.2 directly, build the rest from this
project's own incident types.

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
  See SQ-2. **Partially answered (2026-10-10)**: two directly-fetched academic sources now on file — MAST
  (Cemri et al., arXiv:2503.13657), a 14-mode multi-agent failure taxonomy from 1,600+ annotated traces; and
  Google Research's scaling-agent-systems study (arXiv:2512.08296), finding independent/decentralized
  coordination amplifies errors up to 17.2x vs. 4.4x for centralized coordination, and that multi-agent
  coordination helps parallelizable tasks but hurts sequential ones. See
  `data/external-literature-survey.md`. Two search-summary figures explicitly did not survive a
  primary-source check and are not relied upon. **Update (2026-10-11)**: a third source verified — Wynn et
  al. (arXiv:2509.05396) on multi-agent debate failure modes (accuracy can decline over rounds, driven by
  social conformity, not correctness) — with a disclosed correction to its original search-summary framing.
  Relevant to any future protocol experiment involving extended back-and-forth with ChatGPT.
  **Update (2026-10-11)**: Xu et al. (2026, arXiv:2601.12307) now directly verified too — a single agent
  can **match** (not "exceed," correcting the original search-summary) multi-agent workflows across seven
  benchmarks. Fourth consecutive overclaim this survey has caught and corrected. A separate, stronger-
  claiming paper (Tran & Kiela 2026, arXiv:2604.02460) surfaced in the process and is now the one
  unverified lead, queued for a future pass — not to be conflated with Xu et al.'s narrower finding. See
  `logs/2026-10-11-sq2-xu-et-al-verified.md`. **Update (2026-10-12)**: Tran & Kiela now verified too — the
  claim is conditional (holds when reasoning-token budgets are held constant), not unconditional; the
  paper's real contribution is identifying "budget-control artifacts" that can make reported multi-agent
  gains look architectural when they're really unaccounted compute/context-budget effects — a concrete
  caution for this project's own future protocol-experiment design. All five original survey leads are
  now directly verified. See `logs/2026-10-12-sq2-tran-kiela-verified.md`.
