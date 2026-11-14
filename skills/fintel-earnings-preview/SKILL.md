---
name: fintel-earnings-preview
description: Prepare for a company earnings announcement using its calendar, period-specific consensus, historical surprises and price reactions. Use before results; use earnings-review after results and earnings-quality-review for profit-to-cash analysis.
---

Use Fintel’s authenticated MCP tools for this public-data research workflow. Inspect tool availability and entitlement results before analysis. If required tools fail or are unavailable, explain the missing coverage; do not replace them with model memory. Successful empty results support only limited coverage claims. Use public research tools for this task; private account reads and mutations are unnecessary.

Contract: `earnings_preview` / `earnings-preview-v1`.

Resolve the listing with `fintel.search_securities`. Then retrieve:

- `fintel.get_security_earnings_calendar`
- `fintel.get_security_analyst_estimates`
- `fintel.get_security_earnings_surprises`
- `fintel.get_security_earnings_price_drift`

Use the returned country/symbol for every lookup. Optional `fintel.get_security_current_range` or `fintel.get_security_implied_volatility` can supply options context when entitled.

Explain the announcement date/status, fiscal period, consensus and dispersion, relevant historical evidence, business questions to watch and conditional scenarios. Cite sources and distinguish missing evidence from neutral evidence.

Forecast fiscal periods do not establish estimate snapshot freshness. Do not infer revisions from successive forecast periods. Preserve annual/quarterly, GAAP/adjusted and currency differences. Historical drift offsets use exact calendar days, with missing bars left missing. Options ranges have their own quote dates, expirations and horizons; they do not establish earnings-move probabilities.

Example: “Prepare an earnings preview for US:NVDA; what should I watch?”

Write in the user’s language. Cite material observations with their source dates and clearly identify missing metadata. Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.

## Research operating contract

Define the requested security/universe, horizon and benchmark; state unspecified or not
applicable rather than inventing them. Validate observation dates, units, financial periods,
coverage and conflicting sources before combining evidence. Show formulas, input lineage and
explicit assumptions for calculations. Keep observations, inferred signals and scenarios separate.
Return a conclusion with contrary evidence, unresolved questions and what would change the
assessment. Save or monitor only when requested, through the existing authorization and
confirmation controls; a research request does not authorize persistent changes.

When exposed and entitled, `fintel.get_security_analyst_estimate_revisions` may add retained
same-fiscal-period revision evidence, including receipt dates, contributors and dispersion.
Respect missing receipts, earliest coverage and unknown accounting/currency basis. Optional
`fintel.get_security_earnings_event_study` provides explicitly benchmarked session-window context;
keep it separate from the legacy calendar-day drift. Never label current consensus as the
historical pre-announcement expectation without retained supporting evidence.
