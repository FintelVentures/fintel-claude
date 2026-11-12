---
name: fintel-short-squeeze-assessment
description: Assess whether one named stock has a supported short-squeeze setup using short interest, borrowing conditions and price/volume evidence. Use for squeeze due diligence rather than a candidate leaderboard or a single short-interest lookup.
---

# Short squeeze assessment

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `short_squeeze_assessment` / `short-squeeze-assessment-v1`.

Call `fintel.get_short_interest`, `fintel.get_borrow_rate` and `fintel.get_price_bars` using their advertised bounded-history arguments. Compare reported short shares, days to cover, borrow cost and available inventory against dated price and volume observations. Short float requires a compatible sourced float denominator. Optional `fintel.get_short_volume` and `fintel.get_fails_to_deliver` provide distinct evidence, not substitutes for short interest.

Lead with a provisional assessment, then positioning, counterevidence, catalysts, invalidation conditions and coverage. Keep settlement dates separate from quote timestamps. Borrow inventory is provider-specific, not total lending supply. Short-sale volume is not outstanding short interest; FTDs do not establish illegal activity or a forced-buy date. High short interest alone does not establish squeeze probability or timing.

Example: “Can ABC sustain a short squeeze?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
