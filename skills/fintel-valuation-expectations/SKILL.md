---
name: fintel-valuation-expectations
description: Calculate revenue growth implied by a stock's valuation under explicit terminal-multiple, horizon and discount assumptions. Use for reverse valuation rather than a price target or a full DCF.
---

# Valuation expectations

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `valuation_expectations` / `valuation-expectations-v1`.

Required workflow (do not skip these steps even if you can reproduce the arithmetic):

1. Retrieve `fintel.get_security_data_point` with `key=ev` and `key=MarketCap` for the resolved listing. Preserve each value's currency, scale, provider source and date semantics. `as_of_date` may be a dispatcher calculation/cache date; it is not automatically a quote observation date. A profile's market capitalization is a separate observation and is not a synchronized substitute. If `meta.valuation_validation` reports `inconsistent` or `insufficient_evidence`, respect the withheld value and explain the returned reason; do not reconstruct an approved valuation from its diagnostic components. `arithmetically_consistent` establishes arithmetic only.
2. Retrieve `fintel.get_security_financial_statement` with `kind=income` and `period=ttm`. Select the newest returned observation containing positive `Revenue` and its currency. If TTM is unavailable, request `period=annual` and explicitly label that alternative and its period end. Never use an undated `Revenue` data point or derive revenue by dividing EV by `EvToRevenue`: agreement between related metrics is not independent validation. Do not silently use quarterly revenue or multiply it by four.
3. Reconcile valuation inputs before calculating. EV differs from equity market capitalization because of debt, minority interest, preferred equity and cash; a difference alone is not an error. For a discrepancy needing explanation, retrieve the exact keys `Debt`, `MinorityInterest`, `PreferredStockValueOutstanding` and `CashAndEquivalents` with `fintel.get_security_data_point`. Check EV against market cap plus debt, minority interest and preferred equity minus cash, preserving available component dates, units and currencies. Never treat missing components as zero, infer a debt/cash adjustment from the residual, or silently mix incompatible snapshots. A profile mismatch may reflect a different source/date; establish that from returned evidence rather than assuming it.
4. If revenue has no supported annual/TTM basis, currencies/scales cannot be aligned, or a material valuation discrepancy remains unresolved, stop with an insufficient-evidence explanation and the specific missing observations. Do not lead with numerical implied growth and bury the issue in a qualification. If the market observation date is unverified, do not call the result a current valuation. Offer an explicitly hypothetical calculation only as a separate user choice, with accepted inputs.
5. For supported inputs, call `fintel.calculate_research_scenario` with `kind=reverse_valuation`, `currency`, `enterpriseValue`, `revenue`, `terminalRevenueMultiple`, integer `years` (1..30) and fractional `discountRate` (0..1). Call it separately for each requested sensitivity case. Use the returned required terminal revenue and CAGR, not standalone mental arithmetic. If the calculator is unavailable, report the gap instead of presenting a completed workflow. Years, discount and multiple are explicit user assumptions or clearly labeled illustrative assumptions. Negative EV or nonpositive revenue is outside the domain.

Show a compact input table with value, currency/scale, source, effective/observation date and revenue period basis/end. Distinguish the retrieval date from the observation dates. Cite the statement and calculator results as well as valuation metrics so the reader can verify that the required workflow ran.

Explain inputs, implied expectations, sensitivity, sourced comparison, limitations and coverage. The model discounts terminal revenue-multiple value only and excludes interim cash flows, margins and future dilution. It is not a full DCF, fair-value estimate or unique market forecast. Do not invent numerical effects for excluded factors.

Example: “What revenue growth does ABC's current valuation require?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
