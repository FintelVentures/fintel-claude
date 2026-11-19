---
name: fintel-dividend-sustainability
description: Assess whether a company can support its dividend using payment history, payout coverage and leverage. Use for dividend safety or cut-risk research rather than yield rankings or ex-dividend dates.
---

# Dividend sustainability

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `dividend_sustainability` / `dividend-sustainability-v1`.

Call `fintel.get_security_dividends`, then `fintel.get_security_data_point` separately for the exact keys `DividendCashOpsPayoutRatio`, `DividendPayoutRatio` and `LeverageRatio`. Optional yield or growth data cannot replace those inputs. Preserve financial periods, dates and units; disclose when comparable coverage is unavailable.

Explain payment history and cuts, payout coverage, leverage, counterevidence and monitoring conditions. Distinguish recurring and special dividends, corporate-action adjustments and conditional future payments. Nonpositive earnings or operating cash invalidate reassuring payout-ratio interpretations. Identify issuer type from evidence: REITs, banks, BDCs and funds may require measures absent from this surface. High yield is not sustainability. DividendScore v2 is a shadow candidate, not an approved production predictor; do not invent cut probabilities.

Example: “Is ABC's dividend supported by cash generation?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.

## Research operating contract

Define the requested security/universe, horizon and benchmark; state unspecified or not
applicable rather than inventing them. Validate observation dates, units, financial periods,
coverage and conflicting sources before combining evidence. Show formulas, input lineage and
explicit assumptions for calculations. Keep observations, inferred signals and scenarios separate.
Return a conclusion with contrary evidence, unresolved questions and what would change the
assessment. Save or monitor only when requested, through the existing authorization and
confirmation controls; a research request does not authorize persistent changes.

## Statement coverage and competing cash needs

Supplement proxy payout metrics with `fintel.get_security_financial_statement` for comparable
income, cash_flow and balance periods when available. Inspect payout component methodology:
DPS × current shares is a proxy, not actual cash dividends paid during that fiscal period.
For actual-period cash payout, use statement dividends paid, operating cash and positive capex
spending only when returned and compatible: FCF = operating cash − capex; cash payout = common
cash dividends / FCF for positive FCF. Show source rows and units. Do not substitute financing
outflows for dividends or count special dividends as recurring requirements. Examine supported
debt service, buybacks and liquidity obligations; absent maturity schedules remain unknown.
If comparable statements are unavailable, label the result a limited proxy review and withhold a
complete dividend-coverage conclusion. Negative/zero denominators cannot support reassuring ratios.

For latest retained US filing evidence, request `source=sec` explicitly on
`fintel.get_security_financial_statement`; the default provider source can lag filings. SEC supports
annual/quarterly statements and TTM additive income/cash_flow, with per-metric filing and revision
evidence. Do not sum balances, EPS or weighted shares, mix source cohorts, or fill withheld values
from another source. Preserve fiscal periods, currencies and ratio units: margins are fractions,
cash-dividend coverage is a multiple. Use only reconciled contiguous quarters for TTM; missing
revision proof remains unavailable. Provider-typed standalone quarters do not need adjacent-quarter
subtraction; unverified duration values in `reportedValues` cannot support quarter/runway calculations.
