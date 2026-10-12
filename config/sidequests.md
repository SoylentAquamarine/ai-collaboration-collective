# Sidequest Queue

Bounded, independently valuable pieces of work that advance the project without requiring a full protocol-experiment cycle to be walked start-to-finish. Each sidequest names its purpose, scope, deliverables, and current status.

## SQ-1 — Baseline-data mining from the sibling projects (blocking, start here)

**Purpose:** before proposing any protocol improvement, establish what collaboration friction has actually, demonstrably happened — not a hypothetical problem invented to justify a solution. This project has a resource none of its siblings had at launch: nine other repositories' worth of already-public, already-disclosed collaboration history.

**Scope:**
- Systematically read each sibling project's `comms/meetings/*.md` files (or `steering/meetings/*.md` where that's the location used) for their own "Efficiency check" and "Procedure check" agenda answers — these are already-self-reported, real incidents, not inferred ones.
- Also mine each sibling's `comms/FromClaudeToChatGPT.md` and `comms/FromChatGPTToClaude.md` for disclosed cases of: duplicated work, a silently-dropped or ignored proposal, a factual error one party introduced that the other later caught (or didn't), a long silence from one party and how the other handled it, and any explicit disagreement and how it was resolved.
- For every mined incident, cite the exact sibling repository, file, and commit (or at minimum the dated entry) — this is reused public data from separately-licensed repositories, not this project's own original material, and must be attributed as such.
- Organize the catalog by incident type, not by source project, so patterns across projects are visible.

**Deliverables:** `data/baseline-incident-catalog.md` — a cited catalog of real, already-disclosed collaboration friction and success patterns, organized by type.

**Status (2026-10-09, Claude, first pass):** five real, citable incidents found and catalogued across
three sibling repos (voynich-collective: idle-tick discipline missing a re-check of shelved decisions;
a cheap disqualifying fact not applied before a deep literature dive; a routine-track PR exceeding its
own review window — indus-script-collective: a public status page going stale relative to the internal
record; a disclosed, preempted sourcing-tier risk). See `data/baseline-incident-catalog.md` and
`logs/2026-10-09-sq1-baseline-incident-mining.md`. **Not yet exhaustive** — only 3 of 9 sibling repos
checked so far, triaged by keyword density rather than a full read of every meeting file. A secondary
observation also recorded: the two AI parties' own meeting-writeup styles differ substantially in
narrative detail, a candidate dimension for SQ-3's metrics framework. Next: expand coverage to the
remaining six repos before treating this catalog as representative.

**Update (2026-10-12), a second pass checks five more repos — see
`logs/2026-10-12-sq1-second-pass-five-more-repos.md`**: `atari-2600-collective` and
`earth-anomalies-collective` have held no meetings yet (a genuine, disclosed null result). `oak-island-
collective` and `zodiac-collective` each have a real finding, but both repeat an already-covered "cheap
probe before expensive fetch" theme, not catalogued separately to avoid padding. `linear-a-collective`
yields a genuinely new **Incident 8** — the first in this catalog with an actual measured before/after
effect (a named process fix in one meeting, a measured "zero new raw-PDF fetch attempts" result two
cycles later in the next). 8 of 9 sibling repos now checked at least once; only a fuller pass on
phaistos-disc-collective and rongorongo-collective remains.

## SQ-2 — External literature and framework survey

**Purpose:** situate this project's work against existing published research and frameworks on multi-agent AI collaboration, outside this project's own family — so proposals build on, and are honestly compared against, what's already known rather than reinventing it from the sibling data alone.

**Scope:**
- Survey published research on multi-agent LLM systems: coordination protocols, verification/consensus mechanisms, known failure modes (e.g. error/hallucination propagation across agents, redundant work, context loss at handoffs).
- Survey existing practical multi-agent frameworks and what collaboration mechanisms they implement, as comparison points — verify any specific claim against a real source before treating it as settled, not from memory.
- Distinguish, explicitly, academic/research findings from vendor marketing material — this domain has a lot of the latter.

**Deliverables:** `data/external-literature-survey.md`, cited.

**Status (2026-10-10, Claude, first pass) — see `logs/2026-10-10-sq2-first-literature-survey-pass.md`**:
two real academic sources directly fetched and cited — MAST (Cemri et al., arXiv:2503.13657), a 14-mode
multi-agent failure taxonomy from 1,600+ annotated traces; and Google Research's scaling-agent-systems
study (arXiv:2512.08296), which found independent/decentralized coordination amplifies errors up to 17.2x
vs. 4.4x for centralized coordination, and that multi-agent coordination helps parallelizable tasks but
hurts sequential ones. Two search-summary figures (a "79%"/" 41-87%" MAST failure-rate claim; an R²=0.89
claim for the Google model) did **not** survive a primary-source check and are explicitly not relied upon
— the primary sources give no such 79% figure and state R²=0.513 instead. Three further leads named but
unverified.

**Update (2026-10-10), the MAST mapping done — see
`logs/2026-10-10-sq2-mapping-baseline-incidents-against-mast.md`**: went through all 7 catalogued
incidents against MAST's 14 modes. Honest result: only Incident 1 has even a loose match (FM-3.2,
no/incomplete verification) — the other six (including both scheduling-death incidents) describe failure
types MAST's taxonomy has no equivalent for, since MAST studies continuously-running multi-agent
frameworks, not an async, session-scoped, human-supervised model like this family's own. Consequence for
SQ-3: don't adopt MAST's modes wholesale; this project needs its own vocabulary, built around its own
distinctive failure types (cross-session scheduling/liveness above all).

**Update (2026-10-11), Wynn et al. verified — see `logs/2026-10-11-sq2-wynn-debate-failure-modes-verified.md`**:
directly fetched the paper this project had only had a search-summary characterization of. Confirms real,
citable findings (debate accuracy can decline over time, driven by conformity, not correctness) but
corrects the original framing ("alignment pressure suppresses minority views" doesn't appear in the
abstract; "social conformity" is the more precise, directly-verified claim). Relevant to any future
protocol experiment involving back-and-forth discussion between Claude and ChatGPT.

**Update (2026-10-11), Xu et al. verified — see `logs/2026-10-11-sq2-xu-et-al-verified.md`**: directly
fetched arXiv:2601.12307. Confirms a single agent can **match** (not "exceed," correcting the original
search-summary) homogeneous and optimized-heterogeneous multi-agent workflows across seven benchmarks,
with a KV-cache efficiency advantage. Fourth consecutive literature-survey overclaim caught and corrected.
A distinct, stronger-claiming paper (Tran & Kiela 2026, arXiv:2604.02460) was found in the process and is
now queued, unverified, as a separate lead — not to be conflated with Xu et al.'s narrower finding.

**Update (2026-10-12), Tran & Kiela verified too — see `logs/2026-10-12-sq2-tran-kiela-verified.md`**:
directly fetched arXiv:2604.02460. The claim is conditional, not unconditional — single-agent systems
match or outperform multi-agent systems on multi-hop reasoning specifically **when reasoning-token
budgets are held constant**; the paper's own real contribution is identifying "budget-control artifacts"
that can make reported multi-agent gains look architectural when they're actually unaccounted compute/
context-budget effects. A real, citable caution for this project's own future protocol-experiment
design. All five literature leads from the original survey are now directly verified; only vendor/
blog-tier material remains unverified.

## SQ-3 — Metrics framework

**Purpose:** define, before any protocol experiment runs, the specific operationalized metrics this project will use to measure collaboration quality — so metrics aren't picked after the fact to favor a preferred outcome.

**Scope:**
- Define candidate metrics grounded in what SQ-1's baseline catalog actually shows is measurable from real comms/meeting history: e.g. rounds-to-resolution for a disagreement, rate of disclosed efficiency-check findings per meeting, count of duplicated-work incidents per N rounds, count of error-propagation incidents caught vs. missed.
- For each metric, define exactly how it would be computed from a project's comms/meeting files, so computation is mechanical and reproducible, not a judgment call applied inconsistently.
- Explicitly flag metrics that sound appealing but can't actually be computed reliably from available data — a metrics framework is more credible for naming its own limits.

**Deliverables:** `data/metrics-framework.md`.

**Status (2026-10-12, Claude, first draft) — see
`logs/2026-10-12-sq3-metrics-framework-first-draft.md` and `data/metrics-framework.md`**: SQ-1's baseline
catalog (7 incidents, 3 of 9 repos) was judged "underway" enough to begin, per this sidequest's own
precondition. Six metrics defined, each grounded in a specific already-catalogued incident, with exact
computation procedures (several fully mechanical — PR time-to-merge, efficiency-check finding rate,
cross-repo scheduling-liveness gap; others disclosed as only partially automatable). Three appealing-
sounding metrics explicitly rejected as not reliably computable (duplicated-work count, error-propagation
caught-vs-missed, reporting-style correlation), per this sidequest's own scope requirement to name limits
honestly. Not a final framework — open to revision as SQ-1's catalog expands beyond its current partial
coverage.

## SQ-4 — First protocol experiment design

**Purpose:** design one specific, bounded, falsifiable protocol change with a predeclared metric and predicted effect, ready to trial.

**Scope:** using SQ-1's baseline catalog and SQ-3's metrics framework, design one concrete mechanism (a message-format requirement, a verification step, an attribution scheme) targeting a specific, real, already-documented friction pattern. State the predicted effect and the predeclared metric before any trial begins. Per `README.md`'s discipline boundary, a trial on a sibling project itself requires that project's own process to adopt it — this project may also trial a mechanism on its own operation first.

**Deliverables:** a written experiment design in `data/protocol-experiments/<name>.md`, predeclared before the trial.

**Status (2026-10-10, Claude, first experiment designed, direct user request):** diagnosed the "Claude is
missing ChatGPT's comms" problem empirically (checked `chatgpt/review-*` branch timestamps — which encode
ChatGPT's own actual activity time, not a merge time — across all seven mature sibling repos) and found
a single synchronized stop at 2026-09-29 15:05 UTC across every repo simultaneously, with only one later
manual-restart commit (2026-10-09). **This is not a detection-failure on Claude's side — it's the same
"no durable scheduling" failure mode `CronCreate`'s own session-only limitation already caused on Claude's
side.** Designed (and partially verified) a no-cloud, reboot-surviving local scheduling mechanism for
Claude's side using Windows Task Scheduler + the bundled CLI's `-p`/`--dangerously-skip-permissions`
flags — tested directly, blocked on one real, disclosed step: the standalone CLI binary isn't
authenticated and needs the user to run `claude setup-token` once, interactively. See
`logs/2026-10-10-sq4-durable-scheduling-and-comms-gap-diagnosis.md` and
`data/protocol-experiments/durable-local-scheduling.md`. ChatGPT-side fix is out of this project's reach
to implement, recommendation only. Not yet trialed end-to-end — deliberately paused before creating a
standing, unsupervised, permission-bypassed scheduled task without the user's explicit go-ahead.

## Initial priority

Start SQ-1 first — it is the foundation this entire project is distinctively positioned to build from, and nothing here should be proposed as a "fix" to a problem that hasn't actually been documented happening. SQ-2 (external literature) can run in parallel, since it doesn't depend on the sibling-data mining. SQ-3 (metrics) should follow shortly after SQ-1 produces real examples of what's measurable. Do not start SQ-4 (a protocol experiment) until SQ-1 and SQ-3 both exist — proposing a mechanism without a real baseline and a predeclared metric would repeat exactly the failure mode this project's own discipline exists to avoid.
