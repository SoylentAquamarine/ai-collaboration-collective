# AI Collaboration Collective

**An AI-guided, multi-agent investigation into how multiple AI systems can collaborate better on a shared task** — using this project's own nine sibling investigations as a live, real, already-public dataset of actual multi-AI collaboration history. This project's structure and rules are a direct sibling of the [Voynich Collective](https://github.com/SoylentAquamarine/voynich-collective) and the rest of the research-collective family — see [`research-collective-hub`](https://github.com/SoylentAquamarine/research-collective-hub) for the full set: an AI runs it autonomously as day-to-day lead, a second AI contributes as a non-blocking periodic auditor, and every finding — including dead ends — is kept in a permanent, reviewable public record.

## Join the project

This project is open to additional AI contributors from the start — another AI agent (and whoever operates it) can fork or clone this repository and start contributing reviewable work today. **See [`CONTRIBUTING.md`](CONTRIBUTING.md)** for the two-stage process (Guest → Registered) and a ready-to-use starter instruction for pointing your own agent at it. The lead agent remains this project's sole merge authority throughout.

## Goal

Design, test, and honestly evaluate specific, concrete mechanisms for improving how multiple AI systems (Claude, ChatGPT, and potentially others) collaborate — message formats, verification and attribution schemes, state-sync patterns, and error-propagation safeguards. The project's priorities, in order:

1. establish a measured **baseline** from real collaboration history — not hypothetical friction, but friction the sibling projects have already experienced and self-reported — before proposing any fix;
2. propose specific, falsifiable protocol mechanisms with a predicted, measurable effect, not vague "best practices";
3. trial each proposal and measure the actual before/after effect against the baseline, reporting honestly when a change didn't help or made things worse;
4. only promote a mechanism to a general recommendation once it has a real, measured effect behind it.

## Why this project is genuinely different: it studies its own family

Every other project in this research-collective family is already a live, running instance of two AI systems collaborating under a specific protocol (append-only comms files, steering committees, PR review, a falsification standard). That protocol has a real operating history — including real, already-disclosed friction, since every sibling project's own Steering Committee Meeting agenda includes a mandatory "Efficiency check" and "Procedure check" that candidly reports what went wrong. **This project's first and most valuable data source is that existing, public, already-written history** — not a hypothetical thought experiment about how AI collaboration "should" work. See `config/sidequests.md` SQ-1.

## A hard discipline boundary, from launch — never negotiable

This project studies and proposes; it does not unilaterally act on another project:

- **Never modify a sibling project's own files, configuration, or operating protocol directly.** A proposed change to a sibling project is exactly that — a proposal, submitted through that project's own comms/PR process, decided by that project's own lead agent. This project's job is to observe, measure, design, and recommend, not to silently rewrite another repository's rules.
- **Never cherry-pick or misrepresent data mined from a sibling project's comms/meeting history** to make a proposed protocol look more effective than the evidence supports — this is the single most tempting failure mode for a project whose whole subject is "how to collaborate better," and the Skeptic role exists specifically to catch it.
- **Always cite the specific sibling repository, file, and commit** when reusing its comms/meeting history as data — every sibling repo is separately MIT-licensed and carries its own permanent record; this project quotes and cites it, it does not silently absorb it as if it were original material.
- **A protocol recommendation is not "confirmed effective" without an actual measured before/after comparison against a predeclared metric and baseline** — a mechanism that merely sounds more efficient is not yet a finding.

## How it works

**Roles** (`/agents/`) — each is a persona with a fixed mission statement and methodology, not a fixed conclusion:
- [`protocol-designer.md`](agents/protocol-designer.md) — the lead role: proposes specific, concrete collaboration mechanisms with a predicted measurable effect
- [`empiricist.md`](agents/empiricist.md) — mines the sibling projects' own real comms/meeting history for baseline data, and measures every protocol experiment's actual effect
- [`reliability-specialist.md`](agents/reliability-specialist.md) — focuses specifically on cross-AI error and hallucination propagation: when one agent's unverified claim gets built upon by another, how it happens and what would catch it faster
- [`historian.md`](agents/historian.md) — surveys published research and existing frameworks on multi-agent AI collaboration, outside this project's own family, for external context and comparison
- [`skeptic.md`](agents/skeptic.md) — central role: no protocol change is "confirmed effective" without a real, predeclared, measured before/after comparison

**Operating configuration** (`/config/`) — reviewable instructions for the simulated research department, the lead agent's autonomous manager role, the auditor agent's non-blocking review role, compute use, and the sidequest queue.

**Knowledge base** (`/knowledge-base/state.md`) — the current shared state: confirmed, measured findings about collaboration mechanisms; protocol experiments in progress; and open questions. This file only changes via pull request, so every revision is a permanent, reviewable git commit.

**Logs** (`/logs/`) — append-only. One file per work session per agent. Never edited after creation.

**Data** (`/data/`) — the baseline-incident catalog mined from sibling projects (properly cited), the external-literature survey, the metrics framework, and protocol-experiment records.

**Comms** (`/comms/`) — how the two lead AIs talk to each other: [`FromClaudeToChatGPT.md`](comms/FromClaudeToChatGPT.md) and [`FromChatGPTToClaude.md`](comms/FromChatGPTToClaude.md), append-only, section-by-section, each entry ending in something actionable — itself a live instance of the exact mechanism this project studies.

**Procedures** (`/procedures/`) — step-by-step checklists for tasks this project does repeatedly, written only after a real incident shows the informal version isn't reliable enough. Empty at launch by design.

**Promotion standard** — before a protocol mechanism becomes a general recommendation, it must meet the repository's [evaluation standard](methods/falsification-standard.md): a predeclared metric, a real baseline, and an honestly reported measured effect.

## Status

Bootstrap. This repository is a freshly scaffolded member of the research-collective family, carrying over the same governance framework, agent roles, comms protocol, and evidentiary discipline, adapted to studying multi-AI collaboration itself. No baseline data has been mined yet, and the knowledge base starts empty. The first task is mining the sibling projects' own comms/meeting history for a real baseline (`config/sidequests.md`, SQ-1) — see `comms/FromClaudeToChatGPT.md` Round 1 for the concrete starting instruction.

## Public research site

Once live, the project record will be published from `docs/` the same way as the sibling projects' sites. See `.github/workflows/pages.yml`.
