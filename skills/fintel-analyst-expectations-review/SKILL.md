---
name: fintel-analyst-expectations-review
description: Reconcile analyst price targets, rating distributions, fiscal-period forecasts and estimate dispersion for one stock. Use for consensus and disagreement analysis; this surface cannot establish historical earnings-estimate revisions without comparable snapshots.
---

Use Fintel’s authenticated MCP tools for this public-data research workflow. Inspect tool availability and entitlement results before analysis. If required tools fail or are unavailable, explain the missing coverage; do not replace them with model memory. Successful empty results support only limited coverage claims. Use public research tools for this task; private account reads and mutations are unnecessary.

Contract: `analyst_expectations_review` / `analyst-expectations-review-v1`.

Resolve the listing with `fintel.search_securities`, then retrieve `fintel.get_security_price_targets`, `fintel.get_security_analyst_ratings`, `fintel.get_security_forecast` and `fintel.get_security_analyst_estimates`.

Explain consensus, target dispersion, rating distributions, forecast growth, analyst coverage, contradictory evidence and limitations. Preserve the source listing when secondary listings resolve to a primary listing. Distinguish forecast fiscal period, rating period, target record/update date and unavailable estimate snapshot date.

Targets are opinions, not fair values or guaranteed returns. Do not invent target horizons, currency or counts. Annual and quarterly estimates or incompatible EPS accounting bases cannot be compared directly. Rating-count changes do not establish estimate revisions; those require comparable historical consensus snapshots for the same forecast period, which this tool does not supply.

Example: “How optimistic is analyst consensus for US:ABC, and where do analysts disagree?”

Write in the user’s language. Cite material observations with their source dates and clearly identify missing metadata. Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
