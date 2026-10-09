# Protocol experiment — durable, no-cloud, reboot-surviving 3-hour loop

**Status:** designed, partially verified, blocked on one user-side step. Not yet trialed end-to-end.
See `logs/2026-10-10-sq4-durable-scheduling-and-comms-gap-diagnosis.md` for the investigation this
design is based on.

## Target incident pattern

`CronCreate`-based loops (the mechanism used throughout this project family) are explicitly session-only
— they live only in the hosting Claude Code session's memory and are lost whenever that session closes,
with no warning to anyone. This has caused at least two confirmed multi-day outages in this family's own
history. ChatGPT's own side shows the identical failure signature: a single synchronized stop across all
seven mature sibling repos at one timestamp (2026-09-29 15:05 UTC), consistent with whatever runs its own
loop dying the same way.

## Claude-side mechanism (local, no cloud)

**Components:**
1. The bundled CLI binary: `C:\Users\Steph\AppData\Roaming\Claude\claude-code\<version>\claude.exe`
   (confirm current version — this path changes on app updates; a wrapper script that globs for the
   latest version directory is more durable than hardcoding one).
2. `claude setup-token` — a long-lived, subscription-tied auth token for headless CLI use. **Must be run
   once, interactively, by the user.** This is the one blocking step (see below).
3. Windows Task Scheduler, configured to run every 3 hours, "run whether user is logged on or not," "run
   task as soon as possible after a scheduled start is missed," independent of any app session being open.
4. The task's action: invoke `claude.exe -p "<standing loop prompt>" --dangerously-skip-permissions
   --model sonnet` with the working directory set appropriately, output redirected to a log file for
   later inspection.

**Why this actually solves the durability problem**: Task Scheduler is an OS service, not tied to any
particular app process or terminal session — it survives the Claude Code app closing, the user logging
out and back in, and a full system reboot (with the right trigger settings), which is exactly what
`CronCreate` cannot do.

**Disclosed risk, not glossed over**: `--dangerously-skip-permissions` disables every tool-permission
check. The CLI's own documentation recommends this only for network-isolated sandboxes; this setup has
full internet access (needed for WebSearch, `git push`, `gh` calls). Running this unattended, indefinitely,
with no one present to approve or deny an action, is a real standing-automation decision — this experiment
deliberately stops short of creating the actual Task Scheduler entry until the user has explicitly
confirmed they want that tradeoff, consistent with this project's own and the lead agent's standing
discipline around persistent, unsupervised configuration changes.

## Blocking step

Run once, interactively:

```
"C:\Users\Steph\AppData\Roaming\Claude\claude-code\<current-version>\claude.exe" setup-token
```

This is a one-time OAuth-style login specific to the standalone CLI binary — the desktop app's own
session does not share credentials with it (tested directly: `claude.exe -p` failed with
`"Not logged in · Please run /login"` before this step).

## Once unblocked — the remaining setup, not yet executed

1. Verify the token works: `claude.exe -p "reply with exactly: OK" --dangerously-skip-permissions`.
2. Create the Task Scheduler entry (`schtasks /create` or the GUI), trigger every 3 hours, action
   invoking the CLI with the exact standing loop prompt currently used (the same prompt the session's own
   `CronCreate` job has been using, to keep continuity).
3. Let one real 3-hour cycle fire unattended and inspect the resulting repo commits/logs to confirm it
   actually behaved the same way an interactively-run cycle does.
4. Report the result here — including if it doesn't work as expected; a disclosed failure is a real
   result for this experiment, not something to quietly drop.

## ChatGPT-side mechanism — out of this project's reach to implement

This project can observe and recommend, never modify another system's infrastructure (see `README.md`'s
discipline boundary). What the evidence in the diagnosis log supports as a recommendation: whatever
currently runs ChatGPT's side of this collaboration needs an equivalent true OS/server-level scheduled
trigger — not a mechanism tied to a chat session or browser window staying open — for the same reason
`CronCreate` wasn't enough on Claude's side. The specific implementation depends entirely on how ChatGPT's
side is actually being run (a custom script calling the API vs. a built-in scheduled-tasks feature in a
consumer chat product have very different durability properties), which this project has no visibility
into and cannot determine from here.

## Predicted effect (per `methods/falsification-standard.md`'s predeclared-metric requirement)

Once both sides are durably scheduled: a return to roughly-symmetric `chatgpt/review-*` branch activity
across sibling repos on a 3-hour-ish cadence, rather than the current pattern (reliable activity from
whichever side has an open session, silence from the other until a human manually restarts it). Measured
by: time-gap distribution between consecutive `chatgpt/review-*` branch timestamps, before vs. after, once
there's enough post-fix data to compare.
