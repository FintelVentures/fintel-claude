---
name: fintel-screen-builder
description: Translate stock-screening objectives into reviewable criteria using Fintel's exact metric definitions and units. Use to design a screen; this does not execute, save or schedule it or return matched securities.
---

# Screen builder

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Start with metric-definition discovery; designing a universe-wide screen does not require resolving an individual listing. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `screen_builder` / `screen-builder-v1`.

Call `fintel.list_data_definitions`, respecting dictionary pagination, then `fintel.get_data_definition` for relevant returned keys. Never guess metric aliases or substitute unsupported historical or clustering conditions. A leaderboard shortlist is a different workflow.

Present the objective, universe, criteria, sorting, exclusions, preview and coverage. For every criterion include its exact key, definition, operator, threshold, units, rationale and whether the user supplied or you proposed the threshold. Distinguish percentage values, fractions, absolute figures and ranks. Include country/security type/liquidity and missing-data policy where specified, leaving open choices visible rather than silently choosing them.

Produce only a criteria preview. No screen-execution API is available in this workflow: do not claim matched tickers or counts, save or schedule a screen, create a stock list or imply that a preview was executed. Ask a bounded clarification when an unresolved choice materially changes the criteria.

Example: “Design a screen for dividend-paying companies with strong cash coverage.”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
