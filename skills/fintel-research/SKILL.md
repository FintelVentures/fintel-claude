---
name: fintel-research
description: Answer focused stock, fund, macroeconomic, interest-rate, financial-data or Fintel account questions using the live MCP tool catalog. Use for lookups and general research when no specialist workflow fits; prefer specialist skills for a full assessment.
---

# Fintel research

General workflow for focused Fintel questions. Prefer dedicated skills for discovery, thesis, reported earnings, bull/bear, catalysts, watchlist triage, claim audits and scenarios. Fifteen specialists cover short squeezes, insider signals, dividend sustainability, institutional positioning, options positioning, biotech due diligence, cash runway/dilution, valuation expectations, screen design and execution, earnings previews, earnings quality, analyst expectations, fund holdings, public manager portfolios and intraday technical analysis. Use those for a full assessment rather than assembling an incomplete generic response.

Route full company briefs to `fintel-company-briefing`, curated comparable-company questions to
`fintel-peer-comparison`, flagged-trade investigations to `fintel-unusual-options-investigation`
and consolidated list developments to `fintel-watchlist-briefing`. Options market briefings use
`fintel-options-positioning-review`; reverse valuation uses `fintel-valuation-expectations`.

## Workflow

1. For macroeconomic series, start with `fintel.list_macro_series`; no security lookup is needed. Inspect metadata and coverage with `fintel.get_macro_series`, then use `fintel.get_macro_observations` for latest or historical values. Read [macro interpretation](references/macro-series.md) for rate selection, units and economic-date limitations. For a universe screen, use `fintel-screen-builder` starting with `fintel.get_screening_capabilities`; no individual listing lookup is needed. For company/fund research, resolve the security with `fintel.search_securities` (or `fintel.get_security` /
   `fintel.lookup_identifier` for an exact identifier). Ask if the match is ambiguous.
2. Discover what is available from the connector's tool list; the catalog grows, so do not assume a
   fixed set. Pick the fewest tools that answer the question.
3. Answer first, then support with a short table or bullets of the key figures.

## Tool map (verify against the live tool list)

- Identity: `fintel.search_securities`, `fintel.get_security`, `fintel.lookup_identifier`. For managers use `fintel.search_managers`, then the returned `managerId` with `fintel.get_manager_portfolio_changes`.
- Market breadth: `fintel.list_market_breadth`, then `fintel.get_market_breadth`; see [breadth and classifications](references/breadth-and-classifications.md) for denominators, technicals and coverage.
- Classifications: `fintel.list_sectors` or `fintel.search_classifications`, then `fintel.get_classification`, `fintel.list_classification_children`, `fintel.list_classification_securities` and `fintel.get_security_classification`. Reuse returned identities, not guessed sector slugs.
- Prices: `fintel.get_last_price`, `fintel.get_price_bars`, `fintel.get_intraday_bars` (sampled IEX volume). Prefer the technical-analysis skill for session VWAP, compatible benchmark comparisons and setup limitations; historical signal testing is deferred.
- Disclosed stock ownership: `fintel.get_security_owners` for a bounded page and `fintel.get_security_ownership_activity` for population totals. Fund composition: `fintel.get_fund_holdings_snapshot` for native NPORT holdings, allocations and flows.
- Insiders: `fintel.get_security_insiders`. Classifications, filing dates and trade dates matter; omitted plan information remains unknown.
- Short selling: `fintel.get_short_interest`, `fintel.get_short_volume`, `fintel.get_borrow_rate`, `fintel.get_fails_to_deliver`. Short-sale volume and FTDs cannot substitute for short interest.
- Dividends and earnings: `fintel.get_security_dividends`, `fintel.get_security_earnings`, `fintel.get_security_dividend_calendar`, `fintel.get_security_earnings_calendar`, `fintel.get_security_earnings_surprises`, `fintel.get_security_earnings_price_drift`.
- Analyst views: `fintel.get_security_analyst_ratings`, `fintel.get_security_price_targets`, `fintel.get_security_forecast`, `fintel.get_security_analyst_estimates`. For retained revision history use `fintel.get_security_analyst_estimate_revisions`; US fiscal-target windows use `fintel.get_security_estimate_revision_signals` and `fintel.get_estimate_revision_rankings`. Distinguish receipt dates from provider revision/publication times and preserve excluded coverage.
- Financial statements and calculations: `fintel.get_security_financial_statement` (balance, income, cash_flow) and `fintel.calculate_research_scenario` (cash_runway, reverse_valuation, earnings_quality, discounted_cash_flow). For US filing evidence request statement `source=sec` explicitly; `fintel.get_sec_financial_facts` reads unmapped observations by returned CIK. See [financial and price evidence](references/financial-and-price-evidence.md) before combining statements, ratios, valuation or prices. Match financial periods, currency and scale; normalize capex to positive spending for scenario-calculator inputs, and omit unknown inputs rather than guessing zeros.
- Options: `fintel.get_security_options_flow_sentiment`, `fintel.get_security_options_sentiment_by_expiration`, `fintel.get_security_implied_volatility`, `fintel.get_security_gamma_exposure`. Preserve session/quote/expiration dates and model assumptions.
- Biotech: `fintel.get_security_biotech_catalysts`, then `fintel.get_biotech_catalyst` using a returned published ID for detail. Empty coverage is not an invented pipeline.
- Peers: `fintel.get_security_peers`, `fintel.get_security_peer_analysis` for the curated set and comparison provenance.
- Rankings: `fintel.get_security_rankings`, `fintel.list_leaderboards`, `fintel.get_leaderboard`.
- Definitions and individual metrics: `fintel.list_data_definitions`, `fintel.get_data_definition`, `fintel.get_security_data_point`. Use exact returned keys and units.
- Changes: `fintel.get_security_changes` and `fintel.get_securities_changes` for retained filings, insider forms, analyst actions and estimate endpoint changes; page with returned `meta.next_args`. Empty events do not prove unchanged conditions.
- Custom screens: `fintel.get_screening_capabilities`, `fintel.validate_screen`, `fintel.run_screen`, `fintel.get_screen_run`; use screen-builder for execution, owned saved-screen operations and historical replays. Live execution returns rows in the same call without a receipt or polling. `get_screen_run` is for historical backtest receipts. A criteria preview alone is unexecuted.
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
  account (stock lists, alerts, notebooks, team content, saved screen definitions) without describing
  the concrete change and obtaining explicit user intent. Read-only lookups need none. A request
  to execute a live screen authorizes that call; a historical backtest creates a private expiring
  receipt. Saving a definition is separate.
- This is research support, not personalized investment advice.

For macro questions, retain the provider citation/source link, economic date, retrieval time and
collection/observation freshness warnings. Do not treat an economic date as a historical knowledge cutoff.

For private personal research, see [saved thesis tools](references/private-research.md).
Do not read private thesis or watchlist data into team/public research. The public workflow does
not require personal context. On quota exhaustion, use returned website billing links; billing
status, purchases and subscription changes are not MCP tools. Never raise an API-key limit.

Public feed labels may be neutral identifiers. Preserve their distinctions and returned citations;
do not infer confidential provider identities or describe a neutral label as an originating exchange.

Read [financial and price evidence](references/financial-and-price-evidence.md) for dated close,
EOD fallback and retained market-cap baseline interpretation, including when a screen and quote
use different observation dates.
