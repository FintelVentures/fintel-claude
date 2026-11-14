---
name: fintel-watchlist-briefing
description: Summarize meaningful dated developments across a requested saved Fintel watchlist or explicitly supplied securities. Use for a consolidated read-only briefing; use watchlist-triage when prioritizing an investigation queue.
---

# Watchlist briefing

This portable workflow reuses the internal `watchlist_triage`/`watchlist_review` capabilities;
it does not introduce a new server-side contract or change list contents.

Establish the universe and lookback. For a saved personal list, discover it with
`fintel.list_stock_lists`, clarify ambiguous matches, then read `fintel.get_stock_list` and
`fintel.list_stock_list_items` using the returned ID. Page membership before claiming full-list
coverage. Use only the requested authorized personal list. Do not copy private membership into a
team/public response; a team-context request needs an authorized team list and matching tools.
If the host cannot establish that scope, explain the gap rather than reading a personal list.

For saved-list coverage, call `fintel.get_stock_list_filings`, `fintel.get_stock_list_insiders`
and `fintel.get_stock_list_owners` for that same list. Preserve each tool's actual date window,
counts, pagination and errors; absence from an excerpt does not establish no developments.
For an explicit supplied ticker universe, resolve each with `fintel.search_securities` and use
available per-security ownership/insider and earnings-calendar reads, reporting filing evidence
as unavailable if no suitable exposed read exists. Do not read private lists for a supplied universe.

Add bounded per-security earnings/dividend calendars when the user requests upcoming events.
Apply the same evidence funnel across the examined universe. Label each name with supported
meaningful developments, their source/observation/filing periods, contrary evidence, open questions
and what would change the assessment. Filing dates are distinct from holding and transaction dates;
newly filed holdings are not current trades. Show examined versus requested names and per-name
coverage failures. Use 'no material change in examined evidence' only for successfully examined
coverage, never for a failed or omitted name. This is a briefing, not a portfolio-return analysis.

Return a concise overall conclusion and per-security briefing. Missing required membership or
consolidated evidence prevents a complete saved-list briefing; preserve supported partial evidence
and the exact gap. Classifying an item as 'monitor' does not authorize creating an alert, changing
a list, saving a journal or posting to a team.

## Research operating contract

Define the requested security/universe, horizon and benchmark; state unspecified or not
applicable rather than inventing them. Validate observation dates, units, financial periods,
coverage and conflicting sources before combining evidence. Show formulas, input lineage and
explicit assumptions for calculations. Keep observations, inferred signals and scenarios separate.
Return a conclusion with contrary evidence, unresolved questions and what would change the
assessment. Save or monitor only when requested, through the existing authorization and
confirmation controls; a research request does not authorize persistent changes.

Read [evaluation cases](references/evaluation-cases.md) when validating or releasing this workflow.
