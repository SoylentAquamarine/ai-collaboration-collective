# Evaluation and Promotion Standard

This is the minimum bar for moving a protocol mechanism into `knowledge-base/state.md`'s Confirmed Findings (there called "Recommended Mechanisms"). This project's domain is uniquely prone to a specific failure mode: a recommendation that sounds reasonable and well-intentioned but was never actually measured against a real baseline. The standard here exists specifically to prevent that.

## Minimum bar for a Confirmed Finding

Before a PR adds an entry to `knowledge-base/state.md`'s Recommended Mechanisms, it should have:

- a real, cited baseline incident or pattern from `data/baseline-incident-catalog.md` (SQ-1) or this project's own operating history — not a hypothetical problem;
- a predeclared metric, defined in `data/metrics-framework.md` (SQ-3), stated **before** the trial began;
- an actual trial record: the mechanism was genuinely used for a defined period, within this project's own operation or by a sibling project's own choice through its own process;
- a measured before/after comparison against the predeclared metric, reported honestly — a null or negative result is a complete, valid, and equally reportable outcome;
- exact citations for any sibling-project data used (repository, file, commit or dated entry).

## Required experiment record

Before a protocol mechanism can be trialed, record:

1. **Target incident pattern** — the specific, cited friction pattern this mechanism addresses.
2. **Mechanism** — the exact, followable procedure being proposed (not a principle).
3. **Predicted effect** — stated in terms of a specific, predeclared metric.
4. **Alternatives considered** — at least one simpler or already-attempted-elsewhere mechanism, and why this one was chosen instead.
5. **Trial scope** — where/how long it will run, and what would count as the trial being complete enough to measure.

## Evidence required for promotion to "Recommended"

A mechanism can be promoted only when all of the following are present:

- the baseline metric value (before);
- the post-trial metric value (after), measured the same way;
- a stated judgment of whether the difference is large enough, and attributable enough to the mechanism itself (versus noise or an unrelated confound), to be meaningfully a result — argued explicitly, not just asserted;
- independent review by the other collaborator, including an attempt to recompute the metric from the same underlying data;
- a plainly written statement of what this result does **not** show — in particular, that a mechanism measured as effective within this project's own small-scale trial is not automatically proven effective at a different project's different scale or context.

## Automatic stop conditions

Do not promote a mechanism when any of these applies:

- no real baseline incident motivated it — it was proposed from general intuition about what "should" work;
- the metric was defined, or redefined, after seeing what result it would produce;
- the trial period or scope was chosen after seeing partial results, rather than predeclared;
- the comparison conflates the mechanism's effect with an unrelated change happening at the same time;
- sibling-project data is used without exact citation, or is characterized in a way that doesn't match what the cited source actually says;
- the writeup implies or recommends directly modifying a sibling project's own files rather than proposing through that project's own process.

## Current consequence

At launch, the repository has no baseline catalog, no metrics framework, and no trialed mechanisms — this is a genuine bootstrap state. The first substantive work is mining the sibling projects' own history for a real baseline (`config/sidequests.md`, SQ-1), which is itself infrastructure, not a finding.
