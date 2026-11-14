---
name: fintel-peer-comparison
description: Compare a company with its curated Fintel peers using consistent growth, profitability and valuation metrics. Use for comparable-company analysis rather than a single multiple or an invented peer universe.
---

# Peer comparison

Uses the existing internal `peer_comparison` contract; the portable skill supplies host instructions.
Resolve the subject through `fintel.search_securities`, then call both
`fintel.get_security_peers` and `fintel.get_security_peer_analysis` with its returned country/symbol.
Preserve the returned peer-selection method and company names. Do not silently replace the curated
set with model-selected companies. Additional user-specified comparables must be labelled separately.
This is public read-only research and needs no private account tools.

Read metric definitions, currency, units, financial periods, rank direction, population count and
missing/excluded observations from the responses. Use the live metric catalog/definitions when a
key is unclear; do not guess aliases. Separate incompatible periods/bases and currencies. Prefer
returned ranks/medians to arithmetic on a truncated excerpt. If calculating a rank or median,
show inputs, direction, tie policy and the compared non-null population; do not convert missing
values into zero. A negative earnings multiple is not evidence of cheapness.

Return the peer universe and provenance, a compact consistent growth/profitability/valuation
comparison, rankings only where comparable, the principal trade-offs, contrary evidence and what
would change the comparison. Disclose excluded metrics/names and partial or denied coverage. If
either required peer tool fails, stop the complete comparison rather than inventing a substitute
peer set or full-population ranking. Coverage varies by security and entitlement.

## Research operating contract

Define the requested security/universe, horizon and benchmark; state unspecified or not
applicable rather than inventing them. Validate observation dates, units, financial periods,
coverage and conflicting sources before combining evidence. Show formulas, input lineage and
explicit assumptions for calculations. Keep observations, inferred signals and scenarios separate.
Return a conclusion with contrary evidence, unresolved questions and what would change the
assessment. Save or monitor only when requested, through the existing authorization and
confirmation controls; a research request does not authorize persistent changes.

Read [evaluation cases](references/evaluation-cases.md) when validating or releasing this workflow.
