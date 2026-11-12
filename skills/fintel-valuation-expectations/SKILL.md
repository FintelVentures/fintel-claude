---
name: fintel-valuation-expectations
description: Calculate revenue growth implied by a stock's valuation under explicit terminal-multiple, horizon and discount assumptions. Use for reverse valuation rather than a price target or a full DCF.
---

# Valuation expectations

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `valuation_expectations` / `valuation-expectations-v1`.

Call `fintel.get_security_data_point` with `key=ev` and `fintel.get_security_financial_statement` with `kind=income`. Align enterprise-value currency/scale with dated revenue and distinguish market-value date from financial period.

Call `fintel.calculate_research_scenario` with `kind=reverse_valuation`, `currency`, `enterpriseValue`, `revenue`, `terminalRevenueMultiple`, integer `years` (1..30) and fractional `discountRate` (0..1). Years, discount and multiple are explicit user assumptions or clearly labeled illustrative assumptions. Use calculator outputs for implied terminal revenue and CAGR, including sensitivity cases. Omit unavailable observations; negative EV or nonpositive revenue is outside the domain.

Explain inputs, implied expectations, sensitivity, sourced comparison, limitations and coverage. The model discounts terminal revenue-multiple value only and excludes interim cash flows, margins and future dilution. It is not a full DCF, fair-value estimate or unique market forecast. Do not invent numerical effects for excluded factors.

Example: “What revenue growth does ABC's current valuation require?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
