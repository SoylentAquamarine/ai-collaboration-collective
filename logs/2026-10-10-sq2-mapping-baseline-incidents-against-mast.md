# SQ-2/SQ-1 — mapping the baseline incident catalog against MAST's failure taxonomy

**Trigger:** last cycle's own named next step, after the first external-literature-survey pass: "map SQ-1's
own 5-incident catalog against MAST's specific failure-mode labels, which would give our incident catalog
calibrated vocabulary instead of ad hoc descriptions." (The catalog has since grown to 7 incidents.)

## What's already known / not done yet

Already known: MAST's 14-mode taxonomy (`data/external-literature-survey.md`) and all 7 catalogued
incidents (`data/baseline-incident-catalog.md`). Not done: any attempt to actually apply MAST's labels to
our own incidents — the two documents have sat side by side without being cross-checked.

## Design and why it's non-circular

Go through each of the 7 incidents and ask, honestly, which (if any) MAST failure mode it most resembles —
and explicitly report when none fits well, rather than forcing a label onto an incident that doesn't
actually match just to produce a tidier-looking table.

## Honesty precommitment

If MAST's categories turn out not to cover most of this project's own incidents, report that as the real
finding — a forced, padded mapping would be worse than an honest negative result.

## Result

| Incident | Best MAST match | Fit |
|---|---|---|
| 1 — idle-tick checks new work, not old shelved decisions | FM-3.2 (no/incomplete verification) | Loose — MAST's FM-3.2 is about verifying a *task's output*, not sweeping for *unaddressed backlog*. Related in spirit, not a clean match. |
| 2 — expensive research started before a cheap disqualifying fact was checked | *(none)* | MAST has no category for "available information not consulted before starting work" — its taxonomy assumes the relevant context is already in the conversation; it doesn't score whether an agent searched its own existing context efficiently. |
| 3 — a PR sat open past its stated review window | *(none)* | MAST studies live execution traces within one conversation/run; it has no category for an SLA/timing lapse on a process artifact (a PR) that persists *across* runs. |
| 4 — public status page went stale relative to internal state | *(none, closest: FM-2.4 information withholding)* | Weak — FM-2.4 describes one agent deliberately not sharing information with another *within* an interaction; this incident is an unintentional sync lag between two artifacts, not withheld information between agents. |
| 5 — a disclosed, preempted risk (not a realized failure) | *(none — not a failure at all)* | MAST's entire taxonomy is built from failure traces. It has no "risk flagged and avoided" category, because a trace where nothing went wrong isn't a failure trace to begin with. |
| 6 — both parties' scheduling silently dies between sessions, indistinguishable from the other party choosing not to respond | *(none)* | The sharpest mismatch: MAST's traces are of *active, running* multi-agent conversations. It has no category for the automation *not running at all* between sessions — that's structurally outside what a captured execution trace can show. |
| 7 — a second synchronized resumption, confirming Incident 6's pattern | *(same as 6)* | Not a new failure mode — a replication, not a new category. |

## Decision

**The honest result is a near-total miss, not a tidy mapping** — only Incident 1 has even a loose MAST
analog, and that fit is weak. This is a real, useful finding, not a null result to bury: **MAST's taxonomy
was built from fully-autonomous, continuously-running multi-agent frameworks (AutoGen, MetaGPT, ChatDev)
evaluated on bounded coding/math/agent tasks** — a structurally different setting from this family's own
collaboration model, which is asynchronous, git-mediated, session-scoped (with scheduling that can die
*between* sessions), and human-supervised throughout. Five of our seven incidents (2, 3, 4, 5, and
especially 6-7) describe failure types that can only happen in *this* kind of model — they have no
equivalent in a framework that assumes the agents are always actively running within one conversation.

**Practical consequence for SQ-3 (metrics framework)**: this project should not adopt MAST's 14 modes
wholesale as its own metrics vocabulary. The one mode worth borrowing directly is **FM-3.2 (no/incomplete
verification)**, which does capture something real and recurring in our own catalog (Incidents 1 and,
loosely, 3). The rest of this project's own metrics need to be built from its own incident types —
especially a category MAST has no equivalent for at all: **cross-session scheduling/liveness failure**
(Incidents 6-7), which is arguably this family's single most consequential and most-repeated real problem
so far.
