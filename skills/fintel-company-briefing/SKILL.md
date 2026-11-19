---
name: fintel-company-briefing
description: Prepare a dated company briefing covering business, valuation, growth, financial strength, ownership and upcoming events. Use for a company overview with research context; use investment-thesis for a developed investment case.
---

# Company research briefing

Contract: `company_briefing` / `company-briefing-v1` in the internal agent.

Resolve the listing with `fintel.search_securities`; reuse the returned country, symbol and
company name. Inspect the live tool catalog and account entitlements. This is public read-only
research; private account tools are unnecessary.

Retrieve the profile with `fintel.get_security`, income/balance/cash_flow separately with
`fintel.get_security_financial_statement`, `ev` with `fintel.get_security_data_point`, a bounded
`fintel.get_security_owners` page and `fintel.get_security_earnings_calendar` for an explicit event
window. Use the actual tool schemas for period and pagination arguments. Dividend calendar,
curated peers or dated prices may enrich the requested scope when available.

Compare matching financial periods, units and currency; never add YTD to standalone quarters or
silently treat annual revenue as TTM. Compute growth only from comparable periods: current/prior
minus one, with a positive prior denominator and visible source values. Preserve EV reconciliation
warnings; a null or inconsistent valuation cannot support a numerical valuation conclusion.
Statement period ends do not establish publication dates. A bounded holder page cannot establish
total ownership or exits; separate holding dates from filing dates.

Lead with the assessment, then cover business, valuation, growth, financial strength, ownership
and upcoming events. Name unsupported sections, debt-maturity/guidance gaps and unknown source
lineage. Include contrary evidence and verification/change conditions. A failed required tool means
a complete briefing is unavailable; return the supported sections as explicitly partial evidence,
without outside-memory substitutes or invented figures. Empty results show coverage, not absence
of debt, owners or future events.

## Research operating contract

Define the requested security/universe, horizon and benchmark; state unspecified or not
applicable rather than inventing them. Validate observation dates, units, financial periods,
coverage and conflicting sources before combining evidence. Show formulas, input lineage and
explicit assumptions for calculations. Keep observations, inferred signals and scenarios separate.
Return a conclusion with contrary evidence, unresolved questions and what would change the
assessment. Save or monitor only when requested, through the existing authorization and
confirmation controls; a research request does not authorize persistent changes.

Read [evaluation cases](references/evaluation-cases.md) when validating or releasing this workflow.

For latest retained US filing evidence, request `source=sec` explicitly on
`fintel.get_security_financial_statement`; the default provider source can lag filings. SEC supports
annual/quarterly statements and TTM additive income/cash_flow, with per-metric filing and revision
evidence. Do not sum balances, EPS or weighted shares, mix source cohorts, or fill withheld values
from another source. Preserve fiscal periods, currencies and ratio units: margins are fractions,
cash-dividend coverage is a multiple. Use only reconciled contiguous quarters for TTM; missing
revision proof remains unavailable. Provider-typed standalone quarters do not need adjacent-quarter
subtraction; unverified duration values in `reportedValues` cannot support quarter/runway calculations.
