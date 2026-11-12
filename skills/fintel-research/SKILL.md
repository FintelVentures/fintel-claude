---
name: fintel-research
description: Answer focused stock, fund, financial-data or Fintel account questions using the live MCP tool catalog. Use for lookups and general research when no specialist workflow fits; prefer specialist skills for a full assessment.
---

# Fintel research

General workflow for focused Fintel questions. Prefer dedicated skills for discovery, thesis, reported earnings, bull/bear, catalysts, watchlist triage, claim audits and scenarios. Fourteen specialists cover short squeezes, insider signals, dividend sustainability, institutional positioning, options positioning, biotech due diligence, cash runway/dilution, valuation expectations, screen design, earnings previews, earnings quality, analyst expectations, fund holdings and public manager portfolios. Use those for a full assessment rather than assembling an incomplete generic response.

## Workflow

1. Resolve the security with `fintel.search_securities` (or `fintel.get_security` /
   `fintel.lookup_identifier` for an exact identifier). Ask if the match is ambiguous.
2. Discover what is available from the connector's tool list; the catalog grows, so do not assume a
   fixed set. Pick the fewest tools that answer the question.
3. Answer first, then support with a short table or bullets of the key figures.

## Tool map (verify against the live tool list)

- Identity: `fintel.search_securities`, `fintel.get_security`, `fintel.lookup_identifier`. For managers use `fintel.search_managers`, then the returned `managerId` with `fintel.get_manager_portfolio_changes`.
- Prices: `fintel.get_last_price`, `fintel.get_price_bars`.
- Disclosed stock ownership: `fintel.get_security_owners` for a bounded page and `fintel.get_security_ownership_activity` for population totals. Fund composition: `fintel.get_fund_holdings_snapshot` for native NPORT holdings, allocations and flows.
- Insiders: `fintel.get_security_insiders`. Classifications, filing dates and trade dates matter; omitted plan information remains unknown.
- Short selling: `fintel.get_short_interest`, `fintel.get_short_volume`, `fintel.get_borrow_rate`, `fintel.get_fails_to_deliver`. Short-sale volume and FTDs cannot substitute for short interest.
- Dividends and earnings: `fintel.get_security_dividends`, `fintel.get_security_earnings`, `fintel.get_security_dividend_calendar`, `fintel.get_security_earnings_calendar`, `fintel.get_security_earnings_surprises`, `fintel.get_security_earnings_price_drift`.
- Analyst views: `fintel.get_security_analyst_ratings`, `fintel.get_security_price_targets`, `fintel.get_security_forecast`, `fintel.get_security_analyst_estimates`. Forecast periods do not establish consensus snapshot freshness or historical revisions.
- Financial statements and calculations: `fintel.get_security_financial_statement` (balance, income, cash_flow) and `fintel.calculate_research_scenario` (cash_runway, reverse_valuation, earnings_quality). Match financial periods, currency and scale; normalize capex to positive spending, and omit unknown inputs rather than guessing zeros.
- Options: `fintel.get_security_options_flow_sentiment`, `fintel.get_security_options_sentiment_by_expiration`, `fintel.get_security_implied_volatility`, `fintel.get_security_gamma_exposure`. Preserve session/quote/expiration dates and model assumptions.
- Biotech: `fintel.get_security_biotech_catalysts`, then `fintel.get_biotech_catalyst` using a returned published ID for detail. Empty coverage is not an invented pipeline.
- Peers: `fintel.get_security_peers`, `fintel.get_security_peer_analysis` for the curated set and comparison provenance.
- Rankings: `fintel.get_security_rankings`, `fintel.list_leaderboards`, `fintel.get_leaderboard`.
- Definitions and individual metrics: `fintel.list_data_definitions`, `fintel.get_data_definition`, `fintel.get_security_data_point`. Use exact returned keys and units; criteria previews do not execute a screen.
- The user's account and lists: `fintel.get_account`, `fintel.list_stock_lists`, `fintel.get_stock_list`, `fintel.list_stock_list_items`. Restrict private reads to account-related requests.

Filing-based data lags the period end. Keep report periods separate from filing and retrieval dates. Top-N excerpts cannot establish absent holdings or whole-portfolio overlap. Numeric values returned as normalized dollars do not need an additional historical thousands conversion.

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
