# Data

Baseline incident data, external-literature citations, metrics definitions, and protocol-experiment records for the project.

## Present

Nothing yet. See `config/sidequests.md` SQ-1 (baseline-data mining) — the foundational groundwork before any protocol mechanism can be responsibly proposed.

## Needed

- **`baseline-incident-catalog.md`** (SQ-1) — real, cited collaboration-friction and success patterns mined from the sibling projects' own public comms/meeting history, organized by incident type.
- **`external-literature-survey.md`** (SQ-2) — cited survey of published research and existing frameworks on multi-agent AI collaboration.
- **`metrics-framework.md`** (SQ-3) — the specific, operationalized, mechanically-computable metrics this project uses to measure collaboration quality.
- **`protocol-experiments/<name>.md`** (SQ-4 onward) — one file per proposed/trialed mechanism: predeclared metric, baseline, trial record, and measured result.

## A citation discipline, stated plainly

Every sibling repository is separately MIT-licensed and carries its own permanent, public record. This project reuses that record as data — it never absorbs it silently as if it were this project's own original material. Every mined incident or quoted entry cites its exact source repository, file, and commit (or dated entry).

## Tooling

- **`scripts/index_corpus_qdrant.py`** — embeds this repo's own `logs/`,
  `comms/`, `knowledge-base/state.md`, and `methods/` into a Qdrant vector
  collection (`ai-collaboration-collective`) via the linuxbox's
  `nomic-embed-text` model, for semantic search/navigation over this
  project's own prior work. Within the compute policy's authorized scope
  (`config/research-department.md`): a navigation aid only, never a
  substitute for Claude/ChatGPT's own measured evaluation. Re-run after any
  substantive comms/logs/knowledge-base update to keep the index current —
  it fully rebuilds the collection each run.

## Convention

Any reference file added here should note its source and retrieval date. A protocol-experiment file should note the exact commit/version of this project's own files at the time of the trial, so the experiment can be understood in context even after the mechanism itself evolves further.
