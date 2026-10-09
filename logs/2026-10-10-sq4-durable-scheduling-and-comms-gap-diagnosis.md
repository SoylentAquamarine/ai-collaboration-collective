# SQ-4 — first protocol experiment: diagnosing the "missing comms" problem and designing durable, local scheduling

**Trigger:** direct user instruction: have this project figure out (a) a 3-hour loop for both Claude and
ChatGPT that survives reboots, with no cloud dependency, and (b) why Claude keeps missing ChatGPT's
comms — and keep analyzing and refining the process on an ongoing basis.

## What's already known / not done yet

Already known going in: this project's own host session (the one actually running this investigation)
has itself lost its `CronCreate`-based 3-hour loop at least twice across this family's history (a
confirmed multi-day gap, 2026-09-29 to 2026-10-03, and the loop's own job dying silently again before
2026-10-09) — `CronCreate` jobs are explicitly session-only per their own tool description and do not
survive the hosting Claude Code session closing. Not known going in: why ChatGPT's comms specifically
seemed sparse to the lead agent across recent cycles, or whether a durable, no-cloud local scheduling
mechanism actually exists for either party.

## Method and why this is non-circular

Part (b) first, since the user's framing ("claude is missing chatgpt's comms") contains a testable
empirical claim: either ChatGPT produced comms that Claude's own per-cycle fetch check failed to notice,
or ChatGPT's own comms production itself stopped. These have different fixes (a detection-reliability fix
vs. a ChatGPT-side scheduling fix), so the diagnosis had to come before any design work. Checked git
history directly across all seven mature sibling repos — not Claude's own memory of recent cycles, which
is exactly the kind of self-report this project's own `methods/falsification-standard.md` treats as
weaker than a direct, reproducible check.

## Result — part (b): the comms gap is not a detection failure, it's a synchronized stop on ChatGPT's own side

ChatGPT's connector uses a documented, consistent pattern across this entire project family: when it
lacks direct push credentials to a repo, it routes work through a `chatgpt/review-<YYYYMMDD>-<HHMM>`
branch and PR instead of pushing to `main` directly — and that branch name **encodes ChatGPT's own actual
activity timestamp**, not a merge time. Checking the most recent `chatgpt/review-*` branch name across
all seven mature repos:

```
voynich-collective:        chatgpt/review-20260929-1505
rongorongo-collective:     chatgpt/review-20260929-1505
oak-island-collective:     chatgpt/review-20260929-1505
zodiac-collective:         chatgpt/review-20260929-1505
linear-a-collective:       chatgpt/review-20260929-1505
indus-script-collective:   chatgpt/review-20260929-1505
phaistos-disc-collective:  chatgpt/review-20260929-1505
```

**Identical timestamp, every single repo.** This is not a gradual per-project decline — it is a single,
synchronized, hard stop across the entire family at **2026-09-29 15:05 UTC**, consistent with ChatGPT's
own loop (whatever mechanism runs it) dying all at once, the same way Claude's own `CronCreate` job
silently dies when its hosting session closes. The one apparent exception — a single direct-push commit
to `voynich-collective` on 2026-10-09 ("Queue pinned independent J8 reproduction") — lands on the exact
date the user told Claude, in this same family's own history, "I just kickstarted chatgpt again": a single
manual restart, not a resumed autonomous cadence. No `chatgpt/review-*` activity and no further commits
followed it.

**Conclusion, stated plainly: Claude was not missing anything most of this time. There has been very
little to miss, because ChatGPT's own durable-loop mechanism has the same fragility Claude's does.** The
user's framing ("claude is missing chatgpt's comms") correctly identifies a real, felt problem, but the
actual mechanism is closer to "neither AI has a scheduling system that survives a host restart" than "one
AI isn't reading the other's messages." This reframing matters for which fix is worth building.

**Disclosed, not independently confirmed**: this finding establishes *when* ChatGPT's activity stopped and
that it was synchronized, not *why* its own scheduling mechanism failed — that detail isn't visible from
this side. The timing is close enough to Claude's own documented session gap (discovered broken
2026-10-03, after being set up "every 3 hours" on an earlier date) to suggest a plausible shared trigger —
e.g. the user's own machine or working session closing around 2026-09-29 — but this is a plausible
hypothesis, not confirmed, and is stated as such.

## Result — part (a): a durable, no-cloud local scheduling mechanism for Claude's side exists, with one real blocker identified

Investigated the actual Claude Code CLI binary bundled with the desktop app
(`C:\Users\Steph\AppData\Roaming\Claude\claude-code\<version>\claude.exe`) rather than assuming a
mechanism — directly tested its capabilities:

- **`-p`/`--print`**: runs non-interactively, prints the result, and exits — confirmed via `--help`,
  explicitly notes "the workspace trust dialog is skipped when Claude is run in non-interactive mode."
- **`--dangerously-skip-permissions`**: bypasses all tool-permission prompts, required for headless
  execution since nothing will be present to approve them. The CLI's own help text recommends this "only
  for sandboxes with no internet access" — this environment has internet access, so this is a real,
  disclosed risk tradeoff for the design below, not a casual default.
- **This combination, invoked by Windows Task Scheduler on a recurring 3-hour trigger with "run whether
  user is logged on or not" and "run at task creation, even if the computer is on batteries / after a
  missed scheduled start" options, would be genuinely durable across both app-session closure and system
  reboots** — unlike `CronCreate`, which is explicitly in-memory and tied to one running session. No cloud
  dependency: everything runs on the local machine, matching the user's explicit "no cloud" requirement
  (ruling out the `/schedule` cloud alternative previously offered and declined by implication here).

**Real blocker found, not glossed over**: tested the actual invocation (`claude.exe -p "..."
--dangerously-skip-permissions`) and it failed immediately — `"Not logged in · Please run /login"`. The
standalone CLI binary does not share the desktop app's own authenticated session; it needs its own
credential. The CLI exposes exactly the right tool for this, `claude setup-token` ("Set up a long-lived
authentication token (requires Claude subscription)") — but this is an interactive, one-time OAuth-style
login step that has to be run by the user (or with the user directly present), not something this session
can or should complete unattended on the user's behalf.

## Honesty precommitment, kept

Reporting the auth blocker exactly as found, including that it stops the design from being fully
deployable today, rather than presenting an untested design as if it were already working.

## Decision and next steps

1. **Part (b) is substantively answered**: the fix for "ChatGPT's comms feel missing" is the same fix as
   part (a) — durable scheduling on *both* sides, not a Claude-side detection change. No change to
   Claude's own per-cycle fetch/check procedure is recommended based on this evidence.
2. **Part (a), Claude's side, is designed and partially verified**: the mechanism is real and tested up to
   the auth boundary. **Needs the user to run `claude setup-token` once** (interactive) before a Task
   Scheduler job can be created and tested end-to-end. Not yet created as a standing scheduled task —
   deliberately paused here rather than silently establishing new persistent, unsupervised, permission-
   bypassed automation without the user's explicit awareness of exactly what that means (it would run
   indefinitely, including when no one is watching, with every tool-permission check disabled).
3. **Part (a), ChatGPT's side, is out of this project's reach to implement directly** — this project can
   observe and recommend, never modify another system's infrastructure. What's needed, stated as a
   recommendation: whatever actually runs ChatGPT's side of this collaboration needs an equivalent
   OS/server-level durable trigger (a true background scheduled task or server cron calling the API
   directly), not a mechanism that dies when the hosting session/window closes — the same lesson learned
   the hard way on Claude's side via `CronCreate`'s own documented session-only limitation.
4. **Ongoing**: per the user's own framing ("keep analyzing and refining"), this is an opened thread, not
   a closed one — re-check whether ChatGPT's own `chatgpt/review-*` cadence resumes and whether its
   pattern changes once (if) its own scheduling is made durable, and report that as new baseline data.
