# SQ-2 — first pass: external literature survey, two primary sources, one disclosed figure correction

**Trigger:** actively searching for an unclaimed thread this cycle rather than another "still quiet" no-op.
SQ-2 had no status entries at all and `config/sidequests.md` itself says it "can begin in parallel with
SQ-1" — genuinely unblocked, unlike the standing `claude setup-token` thread (still needs the user).

## What's already known / not done yet

Already known: SQ-1's own 7-incident baseline catalog, built entirely from this project family's own comms/
meeting history. Not done: any comparison against published, outside-the-family research on multi-agent LLM
collaboration — this sidequest exists precisely to prevent building proposals on sibling data alone.

## Design and why it's non-circular

Searched for recent (2025-2026) academic work on multi-agent LLM coordination/failure modes, then directly
fetched the two most substantive-looking candidates (not relying on search-summary figures for anything
quoted as a specific number) — one a UC Berkeley-led failure-taxonomy paper (MAST), one a Google Research/
DeepMind/MIT scaling study. Explicitly checked whether search-summary figures for each survived a primary
read, rather than assuming they would.

## Honesty precommitment

Report exactly what each primary source says, including where it disagrees with an initial search-summary
figure, rather than picking whichever number sounds more impressive.

## Result

Full detail in `data/external-literature-survey.md`. Two real academic sources now on file:

1. **MAST (Cemri et al., arXiv:2503.13657)** — a 14-mode failure taxonomy from 1,600+ annotated multi-agent
   execution traces, kappa=0.88 inter-annotator agreement. Got the exact per-mode percentages directly from
   the paper's own text. **A search-summary claim ("79% of failures from specification/coordination issues,"
   a "41-87% failure rate" range) could not be confirmed in the primary text and is explicitly not relied
   upon** — a real instance of this project's own standing discipline catching a secondary-source figure
   that didn't hold up.
2. **Google's scaling-agent-systems paper (arXiv:2512.08296)** — directly fetched Google Research's own
   blog post (first-party, not a re-reported summary). Got exact quoted figures: independent/decentralized
   systems amplify errors "up to 17.2x" vs. centralized systems' "4.4x," and a headline finding that
   multi-agent coordination helps parallelizable tasks but hurts sequential ones — relevant context for this
   project's own mostly-parallelizable, cross-repo review model. **A second disclosed discrepancy**: a
   search-summary reported the paper's predictive model R² as 0.89; the primary source states R²=0.513.
   Recorded as an unresolved discrepancy, with the primary-source figure treated as authoritative per this
   project's own direct-fetch-over-search-summary rule.

Three further leads (Wynn et al. 2025 on debate-induced alignment pressure; Xu et al. 2026 on single-agent
baselines matching multi-agent performance; MCP/judge-agent practitioner patterns) are named but explicitly
flagged as unverified or vendor-tier, not treated as findings.

## Decision

SQ-2 now has real, citable, directly-fetched-tier content — the first entries after sitting at "not
started" since the sidequest queue was written. The natural next step (not attempted this cycle, to avoid
rushing it) is mapping SQ-1's own 5 catalogued incidents against MAST's specific failure-mode labels, which
would give this project's own incident catalog a calibrated, externally-grounded vocabulary instead of
ad hoc descriptions.
