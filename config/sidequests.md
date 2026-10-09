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

## SQ-2 — External literature and framework survey

**Purpose:** situate this project's work against existing published research and frameworks on multi-agent AI collaboration, outside this project's own family — so proposals build on, and are honestly compared against, what's already known rather than reinventing it from the sibling data alone.

**Scope:**
- Survey published research on multi-agent LLM systems: coordination protocols, verification/consensus mechanisms, known failure modes (e.g. error/hallucination propagation across agents, redundant work, context loss at handoffs).
- Survey existing practical multi-agent frameworks and what collaboration mechanisms they implement, as comparison points — verify any specific claim against a real source before treating it as settled, not from memory.
- Distinguish, explicitly, academic/research findings from vendor marketing material — this domain has a lot of the latter.

**Deliverables:** `data/external-literature-survey.md`, cited.

**Status:** not started. Can begin in parallel with SQ-1.

## SQ-3 — Metrics framework

**Purpose:** define, before any protocol experiment runs, the specific operationalized metrics this project will use to measure collaboration quality — so metrics aren't picked after the fact to favor a preferred outcome.

**Scope:**
- Define candidate metrics grounded in what SQ-1's baseline catalog actually shows is measurable from real comms/meeting history: e.g. rounds-to-resolution for a disagreement, rate of disclosed efficiency-check findings per meeting, count of duplicated-work incidents per N rounds, count of error-propagation incidents caught vs. missed.
- For each metric, define exactly how it would be computed from a project's comms/meeting files, so computation is mechanical and reproducible, not a judgment call applied inconsistently.
- Explicitly flag metrics that sound appealing but can't actually be computed reliably from available data — a metrics framework is more credible for naming its own limits.

**Deliverables:** `data/metrics-framework.md`.

**Status:** not started — benefits from SQ-1 being underway, since the baseline catalog shows what's actually measurable.

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
