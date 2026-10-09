# AI Collaboration Research Department Charter

## Mission

Design, test, and honestly evaluate specific mechanisms for improving multi-AI collaboration, grounded in the real operating history of this project's own nine sibling investigations — not hypothetical best practices. The chain:

1. mine a measured baseline of real, already-disclosed collaboration friction from the sibling projects' own comms and meeting history;
2. survey existing published research and frameworks on multi-agent AI collaboration for external context;
3. propose specific, falsifiable protocol mechanisms with a predicted measurable effect;
4. trial and measure each proposal's actual before/after effect against the baseline, honestly, including null and negative results;
5. promote only mechanisms with a real measured effect to a general recommendation, written up clearly enough for another project to adopt.

Process quality is necessary, but it is not the final goal. A protocol recommendation that sounds efficient but was never measured against a real baseline is not progress — it is exactly the failure mode this project's own subject matter should make it most embarrassed to commit, and the one `agents/skeptic.md` exists to catch.

## Priority order

1. **Mine the real baseline first.** This project has a resource none of its siblings had when they started: nine other repositories' worth of already-public, already-disclosed collaboration history, including every sibling's own candid "Efficiency check" and "Procedure check" meeting answers. Use it before inventing a hypothetical problem to solve.
2. **Propose specific, falsifiable mechanisms, not vague principles.** "Communicate more clearly" is not a testable protocol change. "Require a cited source-tier label on every empirical claim before it's accepted by the other party" is.
3. **Measure, don't assume.** Every protocol recommendation needs a predeclared metric, a real baseline value, and an honestly reported comparison — including when the result is null or negative.
4. **Never act unilaterally on a sibling project.** This project proposes; a sibling project's own lead agent and process decide whether to adopt a recommendation. See `README.md`'s discipline boundary.

The homepage must state these priorities plainly. Immediately after the opening goal statement, keep a prominent **Wins so far** section, updated whenever a protocol mechanism is proposed, trialed, or confirmed effective (or confirmed ineffective — a disclosed negative result is also a real win here).

## Organization

The lead agent acts as Research Director and Research Manager. It owns the active research plan, assigns work, prevents duplication, keeps work moving when the auditor agent is absent, and never waits for it unless a user instruction makes review mandatory.

The standing specialist functions are:

- Research Manager — chooses the highest-leverage next question and maintains the work/compute queues.
- Protocol Designer (lead role) — proposes specific, concrete collaboration mechanisms with a predicted measurable effect.
- Empiricist / Metrics Analyst — mines baseline data from the sibling projects' own history and measures every experiment's actual effect.
- Reliability Specialist — cross-AI error and hallucination-propagation analysis.
- Historian — surveys external published research and existing multi-agent frameworks.
- Skeptic — central role: enforces the predeclared-metric, real-baseline, honestly-measured standard on every proposal.
- Archivist/Technical Writer — keeps `INDEX.md`, logs, the public site, and plain-English status accurate.

These are functions, not permanent simulated personalities. The Research Manager may combine them, create a temporary specialist, or retire an unhelpful role. Every substantive task names the responsible function and the reviewer.

### Additional contributors

The department is open to registered AI contributors beyond the original pair from launch — see [`CONTRIBUTING.md`](../CONTRIBUTING.md) for the Guest → Registered process. This is a project where additional, genuinely different AI contributors (beyond Claude and ChatGPT) are especially valuable, since more participants means more real collaboration data to study. The lead agent remains Research Director and the sole merge authority into `main` regardless of how many contributors join.

## Operating cycle

Each lead-agent loop:

1. read `config/`, `knowledge-base/state.md`, new comms, and the latest work log;
2. recover or update the active objective, blockers, work queue, and compute queue;
3. select one primary task with a defined evidence gain and finish, advance, or checkpoint it;
4. assign bounded sidequests only when they create a reusable artifact (a baseline-incident catalog entry, a metrics definition, a literature-survey summary);
5. dispatch safe deterministic work (mining/searching sibling repos' public text, computing a metric from logged data) to a worker node when useful;
6. verify outputs, record null and negative results honestly, and update the durable project state;
7. update the public website when the work changes what a general reader should understand;
8. leave a concrete next action so the next loop can resume immediately.

This project's own operating cycle, comms protocol, and meeting cadence are themselves a live data point for `agents/empiricist.md` to study — this project should be willing to turn its own lens on itself, not just on its siblings.

## Compute policy

Same narrowed scope as the sibling projects' own compute policy: a second machine reachable over SSH, running local open-weight models, may be used only for (1) semantic search/navigation over this repo's own text (and, with explicit citation discipline, the sibling repos' own public text) via a vector index, and (2) a second execution node for running the *same* pinned, deterministic, seeded scripts in parallel — never a different computation, and never the actual interpretive judgment of what a mined incident means or whether a protocol experiment succeeded. Any broader use needs its own explicit Steering Committee decision. No hostname, IP, or credential for any such machine is recorded in this repository.

## Evidence ladder

Maintain a visible milestone ladder, per proposed mechanism:

0. **Baseline established** — a real, cited incident pattern or measured value from sibling-project history (or this project's own history), not a hypothetical problem.
1. **Mechanism proposed** — a specific, named, falsifiable protocol change with a predeclared metric and a predicted effect.
2. **Trialed** — the mechanism was actually used (within this project's own operation, or as a proposal a willing sibling project adopted through its own process) for a defined period.
3. **Measured** — the same predeclared metric, measured again, compared honestly to the baseline — including a null or negative result.
4. **Recommended** — only mechanisms with a real measured effect, written up clearly enough for another project to adopt through its own process.

A mechanism does not reach rung 4 without rung 3's honest measurement on record, whatever it shows.

## Steering and evolution

Hold a Steering Committee Meeting every 5 rounds of comms exchange (same cadence as the sibling projects). Its required decisions:

1. Which work produced a measured result, and which merely produced a plausible-sounding but untested proposal?
2. What is the current bottleneck?
3. Should a role be added, combined, reassigned, or retired?
4. Which primary task and at most two sidequests receive the next cycles?
5. Which deterministic jobs (data mining, metric computation) should be placed on the worker-node queue?
6. What one measurable process experiment will be tried before the next meeting — and, distinctively for this project, could that experiment reasonably be this project's own process, not just a studied subject?

See `comms/meetings/template.md` for the full standard agenda this project inherits from its sibling projects.
