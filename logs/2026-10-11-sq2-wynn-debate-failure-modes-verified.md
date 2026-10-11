# SQ-2 — verifying a named lead from the first literature survey: Wynn et al. on debate failure modes

**Trigger:** the first literature-survey pass (2026-10-10) named two leads as "search-synthesis tier only,
unverified": Wynn et al. (2025) on debate-induced conformity, and Xu et al. (2026) on single-agent
baselines matching multi-agent performance. This cycle checks the first directly.

## What's already known / not done yet

Already known: a search-summary characterization only — "debate-style systems... alignment pressure within
a debate loop can suppress correct minority views." Not done: confirming the paper's actual title, authors,
or whether that specific framing is accurate to what the paper itself argues.

## Design and why it's non-circular

Searched to identify the specific paper, then directly fetched its arXiv abstract page rather than relying
on the search summary's own paraphrase of the paraphrase.

## Honesty precommitment

Report what the paper's own abstract actually says, including where it's narrower or differently framed
than the original search-summary characterization — not force a match to the earlier framing.

## Result

**"Talk Isn't Always Cheap: Understanding Failure Modes in Multi-Agent Debate"** — Andrea Wynn, Harsh
Satija, Gillian Hadfield (arXiv:2509.05396, ICML MAS Workshop 2025). Directly fetched abstract confirms
real, citable findings: debate "can sometimes be harmful rather than helpful," accuracy "can decline over
time" even when stronger models outnumber weaker ones, and models "frequently shift from correct to
incorrect answers in response to peer reasoning" — favoring agreement over scrutinizing flawed reasoning.

**Disclosed correction to the original search-summary framing**: the specific phrase "alignment pressure
suppresses correct minority views" does not appear in the abstract and may overstate what's confirmed at
this sourcing tier — the closest actual content is "social conformity" and peer-agreement bias, a related
but not identical framing. Recorded as the more precise, directly-verified characterization rather than
the catchier paraphrase.

## Decision

Upgrading this lead from search-synthesis tier to directly-fetched tier in `data/external-literature-survey.md`.
Relevant to this project's own standing concern about collaboration quality: if a future protocol experiment
ever involves multi-round back-and-forth between Claude and ChatGPT converging toward one answer, Wynn et
al.'s finding (debate accuracy can *decline* with more rounds, driven by conformity rather than
correctness) is a real, citable reason not to assume more discussion is automatically better. Xu et al.
(2026) remains unverified — a lead for a future cycle, not pursued here to keep this update focused.
