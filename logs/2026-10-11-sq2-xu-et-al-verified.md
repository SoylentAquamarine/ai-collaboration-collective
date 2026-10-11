# SQ-2 — Xu et al. (2026) verified: "match," not "exceed," and a distinct second paper found

## Precommitment self-review (written before fetching)

**Known:** the original literature-survey pass flagged "Xu et al. (2026)" as a search-synthesis-
tier-only lead, reporting that simpler single-agent baselines "often match or exceed multi-agent
workflows at lower cost." This was explicitly named as the next verification target in both the
survey file and this project's own comms, left unverified through the Wynn et al. pass.

**Not done yet:** the actual paper has never been identified by exact title/authors or directly
fetched.

**Design and why it's non-circular:** search for the specific paper, then directly fetch its
abstract page to check the exact claim against the search-summary's wording — this project's own
established pattern (MAST, Google scaling paper, Wynn et al. all had a search-summary claim that
didn't survive a direct check). Treat "match" and "exceed" as different claims requiring
separate verification, not synonyms.

**Honesty precommitment:** report the paper's actual claim exactly, including if it's narrower
than the original search-summary suggested.

## Findings

**Identified**: Xu, Koesdwiady, Bei, Han, Huang, Wang, Chen, Wang, Wang, Li & Ding, "Rethinking
the Value of Multi-Agent Workflow: A Strong Single Agent Baseline," arXiv:2601.12307 (January
2026). Directly fetched the abstract page.

**The exact claim, verified**: a single agent, using multi-turn conversation, "can reach the
performance of homogeneous [multi-agent] workflows" and "can even match" an automatically
optimized heterogeneous workflow — with an efficiency advantage from KV-cache reuse. The paper
introduces **OneFlow**, a method that automatically tailors workflows for single-agent
execution, reducing inference cost versus existing automatic multi-agent design frameworks
without sacrificing accuracy. Tested across seven benchmarks (coding, mathematics, general QA,
domain-specific reasoning, real-world planning/tool use).

**Disclosed correction**: the original search-summary's "match or **exceed**" framing overclaims
— this paper's own abstract supports "match" / "reach the performance of," not "exceed." This is
the same pattern this project's literature survey has now caught four times running (MAST's
79%, the Google paper's R²=0.89, Wynn et al.'s "suppresses minority views," and now this) —
search-summary synthesis has a consistent tendency to round a hedged "comparable to" claim up to
a stronger one.

**A distinct second paper found, not to be confused with Xu et al.**: Tran & Kiela, arXiv:2604.02460
(April 2026) makes the stronger claim the original search-summary may have actually been
describing — that single-agent systems can match **or outperform** multi-agent systems under
normalized compute, for multi-hop reasoning tasks specifically, arguing from the Data Processing
Inequality (multi-agent decomposition introduces communication bottlenecks and potential
information loss). This is a separate paper, a separate claim, and a separate argument — not
independently verified here this cycle (not directly fetched), named only so it isn't conflated
with Xu et al.'s narrower "match" finding.

## Outcome vs. the original lead

The core relevance to this project survives: a credible academic source does find single-agent
baselines can be competitive with multi-agent workflows on cost/efficiency grounds, a real
counterweight to any future proposal that just adding more agents helps. But the claim is
narrower than originally reported ("match," not "match or exceed"), and the stronger "exceed"
framing, if still worth pursuing, belongs to a different, not-yet-verified paper (Tran & Kiela)
that should not be cited under Xu et al.'s name.

## Decision

All four literature leads named in the original 2026-10-10 survey pass are now directly
verified (MAST, the Google scaling paper, Wynn et al., and now Xu et al.), each with at least
one disclosed correction to its original search-summary framing. The vendor/blog-tier material
and the newly-surfaced Tran & Kiela paper remain unverified — open for a future pass.
