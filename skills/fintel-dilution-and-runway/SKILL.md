---
name: fintel-dilution-and-runway
description: Assess cash runway, funding needs and possible dilution before company milestones using dated financial statements and explicit burn scenarios. Use for liquidity research rather than a generic cash balance lookup.
---

# Dilution and runway

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `dilution_and_runway` / `dilution-and-runway-v1`.

Call `fintel.get_security_financial_statement` for matching `balance` and `cash_flow` periods and `fintel.get_security_data_point` for `CommonSharesOutstanding`. Preserve currency, scale, financial dates and annual/quarterly/TTM basis; cumulative YTD cash flow is not a standalone quarter.

Use `fintel.calculate_research_scenario` with `kind=cash_runway`, `currency`, `cash`, `restrictedCash`, `committedOutflows`, `operatingCashFlow`, positive-spending `capex` and `periodMonths`. Omit missing inputs so it returns `insufficient_evidence`; never silently assume absent commitments or restricted cash are zero. Report available cash, historical burn, runway and burn sensitivities only when supported. Non-burning periods do not imply infinite runway.

Explain liquidity, burn, runway, dilution, milestones and coverage. Distinguish shelves/ATMs from executed raises, basic from fully diluted shares and contingent exercises from cash received. Debt access, future financing and warrant terms require evidence, not presumed availability.

Example: “Can ABC fund operations through its next milestone without dilution?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
