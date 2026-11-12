---
name: fintel-research
description: Research stocks and companies with Fintel data. Use for any question about a ticker or company, ownership, insider activity, short interest, dividends, analyst views or the user's Fintel account, when no more specific Fintel skill fits.
---

# Fintel research

General workflow for Fintel questions. More specific skills exist for discovery, thesis, earnings,
bull/bear, catalysts, watchlist triage, claim audits and scenarios; prefer them when they fit.

## Workflow

1. Resolve the security with `fintel.search_securities` (or `fintel.get_security` /
   `fintel.lookup_identifier` for an exact identifier). Ask if the match is ambiguous.
2. Discover what is available from the connector's tool list; the catalog grows, so do not assume a
   fixed set. Pick the fewest tools that answer the question.
3. Answer first, then support with a short table or bullets of the key figures.

## Tool map (verify against the live tool list)

| Question | Tools |
| --- | --- |
| Identify / look up | `fintel.search_securities`, `fintel.get_security`, `fintel.lookup_identifier` |
| Prices | `fintel.get_last_price`, `fintel.get_price_bars` |
| Ownership | `fintel.get_security_owners` |
| Insiders | `fintel.get_security_insiders` |
| Short selling | `fintel.get_short_interest`, `fintel.get_short_volume`, `fintel.get_borrow_rate`, `fintel.get_fails_to_deliver` |
| Dividends / earnings | `fintel.get_security_dividends`, `fintel.get_security_earnings`, `fintel.get_security_data_point` |
| Analysts | `fintel.get_security_analyst_ratings`, `fintel.get_security_price_targets`, `fintel.get_security_forecast` |
| Rankings / boards | `fintel.get_security_rankings`, `fintel.list_leaderboards`, `fintel.get_leaderboard` |
| Definitions of a metric | `fintel.list_data_definitions`, `fintel.get_data_definition` |
| The user's account and lists | `fintel.get_account`, `fintel.list_stock_lists`, `fintel.get_stock_list` |

Filing-based data (for example 13F ownership) lags the period end; say so.

## Conventions (all Fintel skills)

- Use the Fintel connector for market data, never memory. Call only the tools you need and report
  the as-of date or period the tools return.
- Use the company `name` returned by Fintel. Never infer a company name from a ticker.
- Fail closed: if a tool this workflow requires is unavailable or returns nothing, say what is
  missing and what you could not assess. Do not substitute outside web research or invent figures.
- Finish with a short coverage note (examined, unavailable, stale), then ONE bounded next step that
  names its subject, for example "Want me to run an earnings review on NVDA?" A plain "yes" then
  resumes that action.
- If asked which option you prefer, answer directly: state the preference first, then the criteria,
  the key assumption, and what would change it. Name the missing fact if evidence is incomplete.
  Do not refuse with boilerplate such as "I can't give recommendations".
- Analysis is not authorization. Never create, change or delete anything in the user's Fintel
  account (stock lists, alerts, notebooks, team content) without describing the change and getting
  explicit confirmation first. Read-only lookups need none.
- This is research support, not personalized investment advice.
