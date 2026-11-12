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
