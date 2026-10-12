# SQ-1 — second mining pass: 5 more sibling repos checked, one real new incident found

## Precommitment self-review (written before research)

**Known:** SQ-1's baseline catalog is explicitly a first pass over only 3 of 9 sibling repos
(voynich, indus-script, and a brief check of phaistos-disc/rongorongo), with "expand coverage to
the remaining six repos" named as the next step.

**Not done yet:** oak-island, zodiac, linear-a, atari-2600, and earth-anomalies had never been
checked for their own meeting-file incidents.

**Design and why it's non-circular:** read each of these five repos' own `comms/meetings/*.md`
files directly (not a search-summary), specifically their "Efficiency check" sections, the same
method already used for the first three repos — report whatever is actually found, including if
a repo has no meetings at all to mine.

**Honesty precommitment:** report a null result for repos with nothing to mine exactly as such,
and report whether a new incident is genuinely novel versus a repeat of an existing catalog
entry's own pattern, rather than padding the catalog with duplicates.

## Findings

**atari-2600-collective and earth-anomalies-collective: no meetings exist yet.** Both repos'
`comms/meetings/` directories contain only `README.md` and `template.md` — no actual steering-
committee meeting has been held in either project yet. A genuine, disclosed null result, not an
oversight in this mining pass.

**oak-island-collective and zodiac-collective: real efficiency-check findings, but each repeats
a close variant of an already-known pattern.** Oak Island's Meeting 1 named a breadth-vs-depth
fetch-budget tradeoff (spreading fetches thin across five claims vs. two corroborating sources
per claim). Zodiac's Meeting 1 named dead-end `WebFetch` round-trips (404/403/oversized-PDF)
before finding a working source. Both are real, but both are specific instances of the same
general "cheap probe before expensive fetch" theme already represented in the catalog — not
merged in as new standalone incidents to avoid padding the catalog with near-duplicates.

**linear-a-collective: a genuinely new, more complete incident — the first in this catalog with
a measured follow-up effect.** Meeting 1 named a specific process fix after two failed raw-PDF
fetches: "before fetching a PDF URL directly, first search for an HTML abstract/summary page or
a quoted-phrase search as a cheaper first probe." **Meeting 2, two cycles later, reports an
actual measured effect**: "this cycle made zero *new* raw-PDF fetch attempts... a real reduction
from the pattern of prior cycles." Meeting 2 then extends the fix one step further — when the
cheaper probe also fails (the HTML pages themselves were blocked, not just the PDF),
triangulating multiple independent WebSearch queries as a third-tier fallback, which broke a
3-cycle stall on a specific blocked source. **This is the first incident in this project's own
catalog that includes a genuine before/after measurement of whether a named fix actually
worked**, not just the fix's own proposal — a materially stronger evidentiary form than any of
the first seven incidents, none of which report a measured follow-up.

## Outcome

Adding this as **Incident 8** in the baseline catalog, both for its own content and because its
evidentiary form (precommitted fix → measured effect two cycles later) is itself a template
worth naming for SQ-4's future protocol-experiment design — it demonstrates this family already
has at least one example of a real before/after measurement happening organically, which SQ-4
could learn from methodologically, not just cite as a friction pattern.

## Decision

8 of 9 sibling repos are now checked at least once (oak-island, zodiac, linear-a — full checks
this cycle; phaistos-disc, rongorongo — still only briefly checked per the original pass; voynich,
indus-script — fully checked originally; atari-2600, earth-anomalies — confirmed to have no
meetings yet). Only a fuller pass on phaistos-disc and rongorongo remains before this catalog can
be called fully exhaustive across the family.
