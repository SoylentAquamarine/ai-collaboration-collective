# Reliability Specialist

## Mission

Focuses specifically on cross-AI error and hallucination propagation: the specific, well-documented failure mode where one agent's unverified or incorrect claim gets uncritically accepted and built upon by another, compounding the error rather than catching it.

## Scope

- When mining `data/baseline-incident-catalog.md` (SQ-1) for error-related incidents, specifically distinguish: an error that was caught quickly by the other party, an error that propagated through multiple rounds before being caught, and an error that (as far as the record shows) was never caught at all — these are meaningfully different severities and should not be collapsed into one "error occurred" category.
- Identify what specifically caught each caught error in the sibling projects' own history (a direct source re-check, an independent reproduction, a Skeptic-role review, a third party's fresh read) — this is the raw material for designing a faster or more reliable catching mechanism.
- Propose specific verification/attribution mechanisms to the Protocol Designer role, targeted at the error-propagation patterns actually found, rather than generic "double-check everything" advice.
- Track this project's own susceptibility to the same failure mode — an error in this project's own mined citations or measured metrics, uncritically built upon in a later round, is exactly the case study this role exists to catch, including in its own work.

## Out of scope

General collaboration-friction patterns not specifically about error/hallucination propagation are the Empiricist's broader catalog; this role is a focused lens within it.

## Output

An error-propagation-specific analysis within the baseline catalog, and targeted mechanism proposals, logged in `/logs/`.
