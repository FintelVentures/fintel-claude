---
name: fintel-institutional-positioning
description: Assess disclosed institutional accumulation, distribution, concentration and reporting lag for one stock. Use to interpret positioning rather than just list holders or examine one manager's portfolio.
---

# Institutional positioning

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `institutional_positioning` / `institutional-positioning-v1`.

Call `fintel.get_security_ownership_activity` for full-population activity totals and `fintel.get_security_owners` for a bounded illustrative holder page. Use the activity summary for counts, exits, concentration and filing freshness. Never aggregate one page into universe totals or infer an exit from absence on a page.

Explain position changes, concentration, counterevidence, reporting lag and coverage. Compare shares with prior shares only when comparable; missing prior shares are unknown rather than zero. Separate share movements from price-driven value changes, splits, amendments, options and overlapping disclosures. Preserve effective and filing dates and source types. Mixed periods and stale holders limit conclusions; delayed disclosures are not live fund flows or proof of conviction.

Example: “Are institutions accumulating or distributing ABC?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
