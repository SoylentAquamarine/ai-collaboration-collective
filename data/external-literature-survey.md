# SQ-2 — External literature and framework survey (first pass)

Situates this project's own sibling-derived incident catalog (`data/baseline-incident-catalog.md`) against
published research on multi-agent LLM collaboration — outside this project's own family — so later protocol
proposals build on, and are honestly compared against, what's already known rather than reinventing it from
seven repos' worth of comms logs alone.

## 1. MAST — "Why Do Multi-Agent LLM Systems Fail?" (Cemri et al., arXiv:2503.13657)

**Directly fetched** (arXiv abstract page + full HTML text, not a search-summary). Authors: Mert Cemri,
Melissa Z. Pan, Shuyi Yang, Lakshya A. Agrawal, Bhavya Chopra, Rishabh Tiwari, Kurt Keutzer, Aditya
Parameswaran, Dan Klein, Kannan Ramchandran, Matei Zaharia, Joseph E. Gonzalez, Ion Stoica — a UC Berkeley-
led academic paper, not vendor material. Builds MAST (Multi-Agent System Failure Taxonomy) from 1,600+
annotated execution traces across 7 popular frameworks (including AutoGen, MetaGPT, ChatDev), with the
taxonomy itself validated on 150 traces at high inter-annotator agreement (Cohen's kappa = 0.88) — a real
methodological strength worth noting, since this project's own incident catalog has no comparable
inter-annotator check yet.

**The 14 failure modes, by category, with the paper's own reported frequency (% of traces exhibiting that
mode):**

**FC1 — System Design Issues**
- FM-1.1 Disobey task specification (11.8%)
- FM-1.2 Disobey role specification (1.5%)
- FM-1.3 Step repetition (15.7%)
- FM-1.4 Loss of conversation history (2.8%)
- FM-1.5 Unaware of termination conditions (12.4%)

**FC2 — Inter-Agent Misalignment**
- FM-2.1 Conversation reset (2.2%)
- FM-2.2 Fail to ask for clarification (6.8%)
- FM-2.3 Task derailment (7.4%)
- FM-2.4 Information withholding (0.85%)
- FM-2.5 Ignored other agent's input (1.9%)
- FM-2.6 Reasoning-action mismatch (13.2%)

**FC3 — Task Verification**
- FM-3.1 Premature termination (6.2%)
- FM-3.2 No or incomplete verification (8.2%)
- FM-3.3 Incorrect verification (9.1%)

**Disclosed limitation**: the paper's own text (as extracted) does not give a single category-level
percentage breakdown; summing the individual mode percentages gives roughly FC1≈44%, FC2≈32%, FC3≈23.5% —
**this sum is this project's own arithmetic, not a figure the paper itself states**, and modes likely
co-occur within a single trace, so these sums should not be read as mutually exclusive shares of all
failures. Separately, an initial WebSearch pass (search-synthesis tier) reported "79% of failures originate
from specification and coordination issues" and a "41-87% failure rate" range attributed to this paper —
**neither figure could be confirmed in the directly-fetched text** and both are explicitly not relied upon
here, flagged as a case where a frequently-repeated secondary-source figure did not survive a primary check.

**Relevance to this project's own catalog**: mapping our five incidents (idle-tick discipline gap, a
skipped cheap disqualifying fact, a stale PR, a stale public status page, a disclosed-and-preempted sourcing
risk — see `data/baseline-incident-catalog.md`) against MAST's taxonomy is a natural next step, not done in
this pass: several look like informal instances of FM-3.2 (no/incomplete verification) and FM-1.5 (unaware
of termination conditions), worth checking rigorously rather than asserting from memory.

## 2. "Towards a Science of Scaling Agent Systems" (Google Research/DeepMind/MIT, arXiv:2512.08296)

**Directly fetched** (Google Research's own blog post, a first-party source, not a secondary summary).
December 2025/January 2026 work; 180 controlled agent configurations tested, holding tools/prompts/token
budgets constant to isolate the effect of coordination topology from model choice.

**Headline finding, quoted**: multi-agent coordination "dramatically improves performance on parallelizable
tasks but degrades it on sequential ones." On parallelizable finance tasks, centralized coordination
improved performance by 80.9% over a single agent; on sequential PlanCraft tasks, every multi-agent variant
degraded performance by 39-70%. **Directly relevant to this project's own context**: this family's
Claude/ChatGPT review work across ten independent repos is close to the parallelizable case this paper finds
multi-agent coordination helps most — a reason for cautious optimism about this project's own premise, not
yet an endorsement, since the paper's domains (finance, PlanCraft) are not this project's own.

**Error amplification, quoted exactly**: independent (decentralized) systems "amplified errors by up to
17.2x" relative to a single-agent baseline; centralized (orchestrated) systems "contained this amplification
to just 4.4x," with the orchestrator acting as a "validation bottleneck" that catches errors before they
propagate. No figure given for hybrid/partially-centralized topologies.

**Predictive model**: R² = 0.513 (leave-one-domain-out cross-validation), correctly identifying the optimal
coordination strategy for 87% of held-out task configurations. **Disclosed discrepancy**: an initial
WebSearch pass reported this model's R² as 0.89 — the directly-fetched primary source states 0.513. This is
recorded as a real, unresolved discrepancy between a secondary summary and the primary source, not silently
resolved in either direction; the primary-source figure (0.513) is the one this project treats as
authoritative going forward, per this project's own direct-fetch-over-search-summary discipline.

## 3. Wynn et al. (2025) — directly verified, 2026-10-11

**"Talk Isn't Always Cheap: Understanding Failure Modes in Multi-Agent Debate"** — Andrea Wynn, Harsh
Satija, Gillian Hadfield (arXiv:2509.05396, ICML MAS Workshop 2025). Directly fetched abstract, not a
search summary. Real, citable findings: debate "can sometimes be harmful rather than helpful," accuracy
"can decline over time" even when stronger models outnumber weaker ones, and models "frequently shift from
correct to incorrect answers in response to peer reasoning" — favoring agreement over scrutinizing flawed
reasoning. **Disclosed correction**: the original search-summary framing ("alignment pressure suppresses
correct minority views") does not appear in the abstract itself — the closer, directly-verified framing is
"social conformity" and peer-agreement bias, a related but not identical claim. **Relevant to this
project**: a real, citable reason not to assume more back-and-forth discussion between Claude and ChatGPT
is automatically better — debate accuracy can decline with more rounds, driven by conformity rather than
correctness. See `logs/2026-10-11-sq2-wynn-debate-failure-modes-verified.md`.

## 4. Other leads, not yet directly verified (flagged for a future pass)

- **Protocol-level practitioner guidance** (structured messaging standards like MCP, "judge agent" patterns
  for catching hallucination/premature termination/spec violations before cascade) — explicitly **vendor/
  blog-tier, not peer-reviewed**, named here only to keep it clearly separated from the academic sources
  above, per this sidequest's own scope requirement to distinguish research findings from marketing material.
- **Tran & Kiela (2026)**, arXiv:2604.02460 — newly surfaced while verifying Xu et al. below. Reported
  (search-synthesis tier only, not yet directly fetched) to make a stronger claim than Xu et al.: that
  single-agent systems can match **or outperform** multi-agent systems under normalized compute, for
  multi-hop reasoning specifically, arguing from the Data Processing Inequality. A distinct paper and
  claim from Xu et al. below — not to be conflated with it. Unverified, open for a future pass.

## 4a. Xu et al. (2026) — directly verified, 2026-10-11

Xu, Koesdwiady, Bei, Han, Huang, Wang, Chen, Wang, Wang, Li & Ding, "Rethinking the Value of
Multi-Agent Workflow: A Strong Single Agent Baseline," arXiv:2601.12307. Directly fetched the
abstract page. **Verified claim**: a single agent using multi-turn conversation "can reach the
performance of" homogeneous multi-agent workflows and "can even match" an automatically
optimized heterogeneous workflow, with an efficiency advantage from KV-cache reuse; introduces
**OneFlow**, tested across seven benchmarks (coding, mathematics, general QA, domain-specific
reasoning, real-world planning/tool use). **Disclosed correction**: the original search-summary
framing ("match or **exceed**") overclaims — the paper's own abstract supports "match," not
"exceed." The fourth instance of this project's own literature survey catching a search-summary
overclaim (after MAST's 79%, the Google paper's R²=0.89, and Wynn et al.'s "suppresses minority
views"). See `logs/2026-10-11-sq2-xu-et-al-verified.md`.

## Honest bottom line

Four real, directly-fetched, citable academic sources now on file (MAST's 14-mode failure taxonomy; the
Google scaling-agent-systems paper's topology/error-amplification findings; Wynn et al.'s debate-failure-
mode findings; and now Xu et al.'s single-agent-baseline finding), each with at least one disclosed
correction to an initial search-summary characterization that didn't survive a primary check. This is
still not a comprehensive survey — the vendor/blog-tier material and the newly-surfaced Tran & Kiela paper
remain unverified, and no formal
comparison between this project's own 5-incident catalog and MAST's taxonomy has been attempted yet (named
as the natural next step).
