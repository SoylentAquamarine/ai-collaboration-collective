# SQ-3 — first draft of the metrics framework

## Precommitment self-review (written before drafting)

**Known:** SQ-3 ("Metrics framework") has sat "not started," explicitly gated only on "SQ-1
being underway" — not on SQ-1's completion. SQ-1's baseline-incident-catalog.md already has 7
real, cited incidents from 3 of 9 sibling repos (a first pass, not exhaustive, but genuinely
"underway"). The Initial Priority note itself says "SQ-3 should follow shortly after SQ-1
produces real examples of what's measurable" — that precondition is already met.

**Not done yet:** no metrics have been defined; SQ-3's own deliverable
(`data/metrics-framework.md`) doesn't exist.

**Design and why it's non-circular:** derive every candidate metric from a specific, already-
catalogued incident (not invented in the abstract then retrofitted to an incident), define its
exact computation procedure before any metric is actually computed on real data, and — per
SQ-3's own explicit scope requirement — name which appealing-sounding metrics are **not**
reliably computable from available data, rather than only listing the ones that work.

**Honesty precommitment:** if a metric cannot be made mechanical and reproducible, say so
plainly in the framework itself rather than omitting it and leaving a future reader to
rediscover the same limitation.

## The six computable metrics (full definitions in `data/metrics-framework.md`)

1. **Idle-tick blind-spot rate** (Incident 1) — ticks elapsed before a shelved decision is
   re-surfaced.
2. **Routine-track PR time-to-merge** (Incident 3) — fully mechanical, computable from git/PR
   timestamps alone.
3. **Public-artifact staleness lag** (Incident 4) — partially mechanical; matching "the same
   fact" across an internal commit and a public-site commit needs a judgment call, disclosed as
   a limitation, not hidden.
4. **Efficiency-check finding rate** (SQ-3's own named candidate) — a direct bullet count under
   each meeting's "Efficiency check" header; fully mechanical.
5. **Cross-repo scheduling-liveness gap** (Incidents 6/7) — burst/silence timing from git log
   timestamps across sibling repos; the exact method Incidents 6/7 themselves already used,
   now generalized into a repeatable metric rather than a one-off investigation.
6. **Cheap-check-skip flag count** (Incident 2) — a weaker, disclosed-as-partial metric: counts
   explicit post-hoc "we should have checked X first" admissions in Efficiency-check sections,
   which under-counts real instances that were never caught or admitted.

## Three metrics explicitly flagged as NOT reliably computable (per SQ-3's own scope requirement)

- **Duplicated-work-incident count** (named as a candidate in SQ-3's own original scope text):
  requires a semantic judgment about whether two pieces of work were genuinely duplicative vs.
  legitimately independent parallel exploration — not mechanically extractable from comms text
  pattern-matching alone.
- **Error-propagation incidents caught vs. missed**: the "missed" half is structurally
  undercounted by definition — an error that was never caught leaves no record to count, except
  via a later retrospective discovery (itself rare and non-systematic). Reporting only the
  "caught" half as if it were the full rate would misrepresent what's actually known.
- **Reporting-style correlation** (the baseline catalog's own "Secondary observation" — does
  terse vs. narrative meeting-writeup style correlate with missed action items): a real,
  interesting question, but not yet an operational metric — it would need a much larger sample
  and a way to isolate style from the many other differences between the two parties' own
  processes, neither of which exists yet.

## Outcome

SQ-3's own deliverable file now exists for the first time, derived entirely from SQ-1's already-
catalogued incidents rather than invented independently of them. This is a first draft, not a
final framework — explicitly open to revision once SQ-1's catalog expands beyond its current 3-
of-9-repos coverage, which could surface incident types none of the six current metrics capture.

## Decision

SQ-4 (the first protocol experiment) can now draw on both SQ-1's catalog and this framework, as
its own scope requires — not yet attempted, a distinct future step.
