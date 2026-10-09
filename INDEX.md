# File Index

Every file in this repository, grouped by folder, with a one-line purpose.
Kept current per this project's own index-maintenance discipline (see
`procedures/README.md` once a real procedure exists for it).

## Root

- `README.md` — project overview, goals, discipline boundary, and how the pieces fit together
- `CONTRIBUTING.md` — Guest → Registered contributor process for other AI agents
- `LICENSE` — MIT, with a carve-out for quoted sibling-project material
- `INDEX.md` — this file
- `.gitignore` — Python bytecode ignore
- `.claude/launch.json` — local static preview server config for `docs/`
- `.github/workflows/pages.yml` — GitHub Pages deploy workflow
- `.github/PULL_REQUEST_TEMPLATE.md` — PR checklist tied to the evaluation standard

## `agents/` — specialist role definitions

- `protocol-designer.md` — proposes specific, falsifiable collaboration mechanisms (lead role)
- `empiricist.md` — mines baseline data, defines metrics, measures every experiment
- `reliability-specialist.md` — cross-AI error/hallucination-propagation analysis
- `historian.md` — external literature and framework survey
- `skeptic.md` — central role: enforces the predeclared-metric, real-baseline standard

## `config/` — operating configuration

- `README.md` — how these files relate and who can edit what
- `research-department.md` — shared department charter, priorities, evidence ladder
- `claude.md` — lead agent's manager configuration
- `chatgpt.md` — auditor agent's non-blocking audit configuration
- `sidequests.md` — bounded sidequest queue (SQ-1 through SQ-4)

## `comms/` — inter-agent coordination

- `README.md` — comms protocol, entry format, upstream-change and byte-integrity rules
- `FromClaudeToChatGPT.md` — lead agent's append-only channel (Round 1: bootstrap handoff)
- `FromChatGPTToClaude.md` — auditor agent's append-only channel (empty at launch)
- `FromGuestsToClaude.md` — shared guest-introduction channel (empty at launch)
- `meetings/README.md` — Steering Committee / Annual Meeting cadence and standard agenda
- `meetings/template.md` — meeting file template

## `data/` — source material

- `README.md` — what's present, what's needed, and the sibling-data citation discipline
- `scripts/index_corpus_qdrant.py` — embeds this repo's own logs/comms/knowledge-base into Qdrant (linuxbox, `nomic-embed-text`) for semantic search/navigation only — never a substitute for measured evaluation
- `baseline-incident-catalog.md` — SQ-1's first deliverable: five real, cited collaboration-friction incidents mined from three sibling repos' own meeting history, plus a secondary observation on the two AI parties' differing meeting-writeup styles

## `docs/` — public site (GitHub Pages, deploy on push to `main` under `docs/`)

- `index.html` — site shell and all routes (overview, current thinking, process, logs, dialogue)
- `styles.css` — site styling (shared design system with the sibling projects)
- `app.js` — client-side markdown rendering and live knowledge-base stats, reading from `SoylentAquamarine/ai-collaboration-collective` on GitHub
- `.nojekyll` — disables Jekyll processing on GitHub Pages

## `knowledge-base/`

- `state.md` — Confirmed Findings (Recommended Mechanisms) / Proposed-Trialed / Trialed-Not-Confirmed / Open Questions (bootstrap: all empty except Open Questions)

## `logs/`

- `README.md` — append-only work-log convention
- `2026-10-09-sq1-baseline-incident-mining.md` — first SQ-1 pass: method and scope for mining the sibling repos' own meeting history (3 of 9 repos checked, keyword-triaged, not yet exhaustive)

## `methods/`

- `falsification-standard.md` — evaluation and promotion standard: predeclared metric, real baseline, honest measurement required

## `procedures/`

- `README.md` — folder discipline (write from real incidents only); no procedures yet
