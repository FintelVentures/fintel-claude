---
name: fintel-earnings-quality-review
description: Assess whether a company's reported profits translate into operating cash and free cash flow using comparable financial statements and deterministic ratios. Use for earnings quality rather than a beat/miss recap or unsupported accounting allegations.
---

Use Fintel’s authenticated MCP tools for this public-data research workflow. Inspect tool availability and entitlement results before analysis. If required tools fail or are unavailable, explain the missing coverage; do not replace them with model memory. Successful empty results support only limited coverage claims. Use public research tools for this task; private account reads and mutations are unnecessary.

Contract: `earnings_quality_review` / `earnings-quality-review-v1`.

Resolve the listing with `fintel.search_securities`. Call `fintel.get_security_financial_statement` separately with `kind=income`, `kind=cash_flow` and `kind=balance`. Choose matching annual, quarterly or TTM periods.

For arithmetic use `fintel.calculate_research_scenario` with `kind=earnings_quality`, `currency`, `revenue`, `netIncome`, `operatingCashFlow` and positive-spending `capex`. Omit missing inputs; the calculator returns `insufficient_evidence`. Use its results for FCF, cash conversion and margins.

Explain profitability, cash conversion, capital spending, contradictory evidence and next verification. Align dates, currency, units and accounting basis before comparisons. Cumulative YTD is not a standalone quarter. Nonpositive profit/revenue denominators cannot support reassuring ratio interpretations.

Basic statements do not contain a full receivables/inventory or exceptional-item breakdown. Accounting explanations need cited evidence; cash divergence alone does not establish fraud. The legacy Piotroski score is not a substitute for verified observations.

Example: “Are US:ABC’s reported profits translating into cash?”

Write in the user’s language. Cite material observations with their source dates and clearly identify missing metadata. Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
