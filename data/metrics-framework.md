# Metrics framework

SQ-3's deliverable: operationalized metrics for measuring collaboration quality across this
project family, defined **before** any protocol experiment (SQ-4) runs, so metrics aren't
picked after the fact to favor a preferred outcome. Every metric below is grounded in a
specific incident already catalogued in `data/baseline-incident-catalog.md` — none is invented
in the abstract and retrofitted to an incident afterward. See
`logs/2026-10-12-sq3-metrics-framework-first-draft.md` for the drafting process.

**Standing caveat on all of these**: SQ-1's own baseline catalog is a first pass over 3 of 9
sibling repos, not yet exhaustive. These six metrics are grounded in what that partial catalog
has surfaced so far; a fuller SQ-1 pass could surface incident types none of these capture,
and this framework should be revisited when it does.

## 1. Idle-tick blind-spot rate

**Grounded in:** Incident 1 (a shelved decision sat idle for 8 consecutive no-op ticks before a
meeting caught it).

**Definition:** the number of consecutive "no new activity" comms entries that elapse before a
shelved, already-scoped backlog item is re-surfaced (either by an explicit sweep or by a
meeting's own review).

**Computation:** scan a project's `comms/FromClaudeToChatGPT.md` (or equivalent) for
consecutive entries matching a no-op pattern (e.g. "still quiet," "no new activity"); separately
scan `comms/meetings/*.md` action-item tables for items marked "deferred" or "shelved" with a
timestamp; compute the tick-count gap between an item's deferral and its next mention. Fully
mechanical once a project consistently tags deferred items as such — not yet true of every
sibling repo, a real precondition for this metric to be computed project-wide.

## 2. Routine-track PR time-to-merge

**Grounded in:** Incident 3 (a routine-track PR sat open past its own stated review window).

**Definition:** elapsed time between a PR being marked ready for routine-track merge and its
actual merge, compared against the project's own stated window (where one exists).

**Computation:** fully mechanical — `gh pr view <PR> --json createdAt,mergedAt,reviews` or
equivalent git/GitHub API timestamps. No semantic judgment required. The only project-specific
step is reading each project's own stated window from its process docs.

## 3. Public-artifact staleness lag

**Grounded in:** Incident 4 (a public status page omitted an already-made internal correction).

**Definition:** elapsed time between an internal knowledge-base commit recording a fact and the
corresponding public-site commit reflecting the same fact.

**Computation:** partially mechanical. Commit timestamps themselves are trivial to extract; the
real difficulty, disclosed rather than glossed over, is matching which public-site commit
actually corresponds to which internal fact — that step currently needs a human/AI judgment
call (reading both diffs and deciding they're about the same underlying claim), not a pattern
match. This metric is usable but not fully automatable as written.

## 4. Efficiency-check finding rate

**Grounded in:** SQ-3's own original scope text, which named this as a candidate directly.

**Definition:** count of distinct findings logged under a meeting's own "Efficiency check"
agenda section, per meeting.

**Computation:** fully mechanical — a bullet-point count under a consistently-headed section in
`comms/meetings/*.md` files. The main caveat is cross-project consistency: Claude's and
ChatGPT's own meeting-writeup formats differ (see the baseline catalog's "Secondary
observation" — narrative vs. terse-bullet style), so a raw bullet count may not be a like-for-
like comparison across the two parties without further normalization, named here as a known
limitation, not solved by this metric alone.

## 5. Cross-repo scheduling-liveness gap

**Grounded in:** Incidents 6 and 7 (synchronized, family-wide stop-and-resume bursts in
ChatGPT's own scheduling, found only by this project's own direct git-timestamp investigation).

**Definition:** the time gap between activity bursts in a party's own fallback-branch naming
convention (e.g. `chatgpt/review-<timestamp>`) across all sibling repos simultaneously, and
whether those gaps are synchronized (same timestamp across every repo) or staggered
(independent per-repo).

**Computation:** fully mechanical — exactly the method Incidents 6 and 7 already used by hand
(`git log` across all sibling repos' remote branches, extracting and comparing timestamps).
This metric generalizes that one-off investigation into a repeatable check, rather than
requiring a fresh manual investigation each time the question comes up.

## 6. Cheap-check-skip flag count

**Grounded in:** Incident 2 (expensive research began before a cheap, already-available
disqualifying fact was checked).

**Definition:** count of explicit post-hoc admissions, in a meeting's "Efficiency check"
section, of the form "we should have checked X before starting Y."

**Computation:** mechanical in the narrow sense of pattern-matching such admissions once
written down — but disclosed as a **structural undercount**: this only counts cases that were
noticed and admitted after the fact. A case where the cheap check was skipped and nobody ever
caught it leaves no record to count. This metric measures "admitted near-misses," not the true
rate of the underlying failure mode — a floor, not an estimate.

## Metrics explicitly rejected as not reliably computable

- **Duplicated-work-incident count** — named as a candidate in SQ-3's own original scope text,
  but rejected here: distinguishing genuine duplication from legitimate independent parallel
  exploration requires a semantic judgment call per instance, not a pattern match, and no
  consistent operational definition of "duplicate" currently exists across this project family.
- **Error-propagation incidents caught vs. missed** — the "missed" half is structurally
  uncountable by definition (an uncaught error leaves no record), so any reported rate would
  silently only reflect the "caught" half, misrepresenting itself as more complete than it is.
- **Reporting-style correlation** (terse vs. narrative meeting style vs. missed action items) —
  a real, interesting question raised by the baseline catalog's own secondary observation, but
  not yet an operational metric: it needs a much larger sample and a way to isolate writing
  style from every other difference between the two parties' processes, neither of which this
  project currently has.
