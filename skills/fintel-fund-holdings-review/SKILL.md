---
name: fintel-fund-holdings-review
description: Review a resolved ETF or supported fund's disclosed NPORT holdings, concentrations, asset/country/currency allocations and reported flows. Use for public fund composition; bounded delayed holdings cannot establish full overlap or live exposure.
---

Use Fintel’s authenticated MCP tools for this public-data research workflow. Inspect tool availability and entitlement results before analysis. If required tools fail or are unavailable, explain the missing coverage; do not replace them with model memory. Successful empty results support only limited coverage claims. Use public research tools for this task; private account reads and mutations are unnecessary.

Contract: `fund_holdings_review` / `fund-holdings-review-v1`.

Resolve the fund listing with `fintel.search_securities`, then call `fintel.get_fund_holdings_snapshot` with its returned country/symbol and optional `limit` (1..100, default 20).

Explain fund/series identity, report period, filing date, top disclosed holdings, concentration, asset/instrument/country/currency allocations and reported flows. Use full-filing allocation aggregates for totals. Top holdings are a bounded excerpt and cannot establish complete overlap or the absence of a position.

NPORT reports are delayed. Native amendments are not ingested; disclose this limitation. Ambiguous or unsupported funds return unavailable coverage. Preserve nulls and unclassified allocation labels. Market-value allocations do not establish net derivatives exposure. Flows use SEC month numbers within the filing’s three-month window, not retrieval months. Do not infer missing dates, full holdings or share-class identity.

Example: “What does this ETF own, and where is its concentration?”

Write in the user’s language. Cite material observations with their source dates and clearly identify missing metadata. Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
