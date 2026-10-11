# SQ-2 — Tran & Kiela (2026) verified: a budget-conditional claim, not an unconditional one

## Precommitment self-review (written before fetching)

**Known:** last cycle's Xu et al. verification surfaced a second, distinct paper (Tran & Kiela,
arXiv:2604.02460) reported at search-synthesis tier only, making a stronger claim than Xu et al.
— that single-agent systems can "match or outperform" multi-agent systems, argued from the Data
Processing Inequality, for multi-hop reasoning specifically. Named as the one remaining
unverified lead from the external-literature survey.

**Not done yet:** the paper had not been directly fetched; its exact claim, scope, and any
conditions attached to it were unknown beyond the original search-summary characterization.

**Design and why it's non-circular:** directly fetch the abstract page and check the exact
wording against the original "match or outperform" framing — this project's own established
pattern (every one of the four prior literature leads had at least one search-summary overclaim
caught on direct verification).

**Honesty precommitment:** report the claim's actual conditions and scope exactly, including if
it's narrower or more conditional than the original framing suggested.

## Findings

**Identified and directly fetched**: Dat Tran and Douwe Kiela, arXiv:2604.02460. The claim is
**conditional, not unconditional**: single-agent systems (SAS) "consistently match or
outperform MAS on multi-hop reasoning tasks when reasoning tokens are held constant" — i.e.
under a fixed compute/token budget with good context utilization, not as a general claim about
single-agent vs. multi-agent systems in all circumstances. The paper itself predicts multi-agent
systems become competitive again when a single agent's context use degrades or when more
compute is spent overall.

**A methodologically relevant finding for this project specifically**: the paper argues many
reported multi-agent performance gains in prior work are better explained by **unaccounted
computation and context-budget effects** than by anything about multi-agent architecture itself
— it identifies specific "budget-control artifacts" in API-based setups (notably Gemini 2.5) and
in standard benchmarks that can inflate apparent multi-agent gains. Tested across three model
families (Qwen3, DeepSeek-R1-Distill-Llama, Gemini 2.5) under matched budgets.

**Grounded in the Data Processing Inequality**: a fixed reasoning-token budget with perfect
context use lets a single agent process information more efficiently than a multi-agent
decomposition, per the paper's own theoretical framing (the abstract doesn't give the full
formal derivation; not independently re-derived here).

## Outcome vs. the original lead

The original search-summary's "match or outperform" framing is directionally accurate but
drops the paper's own central qualifier — the claim holds specifically **when reasoning-token
budgets are held constant**, not as an unconditional architecture comparison. This is a
materially different, narrower claim than "single agents beat multi-agent systems," and it is
distinct from (not a stronger version of) Xu et al.'s own "match" finding — Tran & Kiela's
contribution is specifically the *budget-accounting* argument, not just an empirical result.

**A real caution worth carrying forward for this project's own SQ-4 work**: if this family of
projects ever designs a protocol experiment claiming a multi-agent coordination benefit, this
paper's own named "budget-control artifact" critique is a concrete, citable reason to check
whether an observed gain is actually attributable to the coordination mechanism itself, or to
an unaccounted difference in effective compute/context budget between the compared conditions.

## Decision

All literature leads surfaced across this project's external-literature-survey work are now
directly verified (MAST, the Google scaling paper, Wynn et al., Xu et al., and now Tran &
Kiela), each with at least one disclosed correction or important qualifier found on direct
reading. No further unverified leads remain on file from the original survey pass.
