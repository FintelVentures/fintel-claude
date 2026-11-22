# Fintel plugin for Claude

Connect Claude to [Fintel](https://fintel.io) to research stocks with Fintel's financial data and
account tools. The plugin bundles:

- **MCP connector** (`.mcp.json`): the remote Fintel MCP server at `https://mcp.fintel.io/mcp`.
- **Skills** (`skills/`): research workflows that use the Fintel tools. See below.

## Skills

Version 0.3.2 bundles 28 portable skills, including all ten R1 investment-question outcomes. Each linked skill describes when to use it, its evidence tools, output and limitations. All tools require an authenticated MCP connection and the account's entitlements; inspect the live tool list before relying on a dependency. A package version does not prove that the matching server tools have been deployed.

### Established workflows

- [`fintel-research`](skills/fintel-research/SKILL.md): Answer focused stock, fund, financial-data or Fintel account questions using the live MCP tool catalog. Use for lookups and general research when no specialist workflow fits; prefer specialist skills for a full assessment.
- [`fintel-stock-discovery`](skills/fintel-stock-discovery/SKILL.md): Find research candidates from Fintel leaderboards and rankings, including squeeze candidates, yield leaders and market movers. Use for ranked shortlists; use screen-builder to design and execute custom screens and specialist assessments to investigate one returned stock.
- [`fintel-investment-thesis`](skills/fintel-investment-thesis/SKILL.md): Build a sourced investment thesis for one company with supporting and contradicting evidence, catalysts, risks, assumptions and invalidation conditions. Use for a deep dive or investment case rather than a narrow metric or specialist assessment.
- [`fintel-earnings-review`](skills/fintel-earnings-review/SKILL.md): Review reported earnings results, actual versus estimated figures, supported period comparisons and open questions. Use after results; use earnings-preview before an announcement and earnings-quality-review for profit-to-cash analysis.
- [`fintel-bull-bear`](skills/fintel-bull-bear/SKILL.md): Stress-test a stock thesis with the strongest supported bull and bear cases, shared assumptions, conflicting evidence and observations that would settle disagreements. Use when the user requests both sides or challenges an existing view.
- [`fintel-catalyst-calendar`](skills/fintel-catalyst-calendar/SKILL.md): Build a dated calendar of upcoming earnings, dividends and supported biotech events for one company, preserving estimated windows and coverage gaps. Use for timing; use earnings-preview or biotech-event-due-diligence for deeper event analysis.
- [`fintel-watchlist-triage`](skills/fintel-watchlist-triage/SKILL.md): Review a signed-in user's Fintel stock list using list-level filings, insider and ownership evidence to prioritize names for investigation or monitoring. Use for private watchlist triage; this does not edit lists or review a public manager portfolio.
- [`fintel-claim-audit`](skills/fintel-claim-audit/SKILL.md): Check financial claims in supplied text or a discussion against cited evidence and available Fintel observations. Identify unsupported, stale, conflicting or unverifiable claims and citation mismatches without manufacturing outside support.
- [`fintel-scenario-analysis`](skills/fintel-scenario-analysis/SKILL.md): Frame conditional upside, base and downside outcomes for a company or event with a common horizon, explicit assumptions, triggers and invalidation conditions. Use for what-if analysis; use valuation-expectations or dilution-and-runway for their dedicated calculations.

### Specialist assessments

- [`fintel-analyst-expectations-review`](skills/fintel-analyst-expectations-review/SKILL.md): Reconcile analyst price targets, rating distributions, fiscal-period forecasts and estimate dispersion for one stock. Use for consensus and disagreement analysis; use retained history and fiscal-target revision tools for supported estimate-change questions.
- [`fintel-biotech-event-due-diligence`](skills/fintel-biotech-event-due-diligence/SKILL.md): Assess trial evidence, success conditions and risks for a published biotech catalyst. Use for event due diligence rather than a calendar lookup, an invented pipeline or individual medical advice.
- [`fintel-dilution-and-runway`](skills/fintel-dilution-and-runway/SKILL.md): Assess cash runway, funding needs and possible dilution before company milestones using dated financial statements and explicit burn scenarios. Use for liquidity research rather than a generic cash balance lookup.
- [`fintel-dividend-sustainability`](skills/fintel-dividend-sustainability/SKILL.md): Assess whether a company can support its dividend using payment history, payout coverage and leverage. Use for dividend safety or cut-risk research rather than yield rankings or ex-dividend dates.
- [`fintel-earnings-preview`](skills/fintel-earnings-preview/SKILL.md): Prepare for a company earnings announcement using its calendar, period-specific consensus, historical surprises and price reactions. Use before results; use earnings-review after results and earnings-quality-review for profit-to-cash analysis.
- [`fintel-earnings-quality-review`](skills/fintel-earnings-quality-review/SKILL.md): Assess whether a company's reported profits translate into operating cash and free cash flow using comparable financial statements and deterministic ratios. Use for earnings quality rather than a beat/miss recap or unsupported accounting allegations.
- [`fintel-fund-holdings-review`](skills/fintel-fund-holdings-review/SKILL.md): Review a resolved ETF or supported fund's disclosed NPORT holdings, concentrations, asset/country/currency allocations and reported flows. Use for public fund composition; bounded delayed holdings cannot establish full overlap or live exposure.
- [`fintel-insider-signal-review`](skills/fintel-insider-signal-review/SKILL.md): Assess the strength of reported insider activity for one company, including transaction types, clusters, timing and alternative explanations. Use to interpret insider signals rather than merely retrieve trades.
- [`fintel-institutional-positioning`](skills/fintel-institutional-positioning/SKILL.md): Assess disclosed institutional accumulation, distribution, concentration and reporting lag for one stock. Use to interpret positioning rather than just list holders or examine one manager's portfolio.
- [`fintel-manager-portfolio-review`](skills/fintel-manager-portfolio-review/SKILL.md): Compare one investment manager's latest two disclosed 13F portfolios using amendment-aware changes and concentration evidence. Use for a public manager portfolio; this does not read the user's private portfolio or establish current trades or performance.
- [`fintel-options-positioning-review`](skills/fintel-options-positioning-review/SKILL.md): Reconcile one stock's options flow, expiration positioning, implied volatility and gamma evidence. Use for options positioning around an event rather than one metric, a leaderboard or an execution strategy.
- [`fintel-screen-builder`](skills/fintel-screen-builder/SKILL.md): Design, validate and execute custom stock screens with Fintel Workbench. Use for compound filters, formulas, rankings, historical screening, backtests and user-requested saved screens; use stock-discovery for existing leaderboard shortlists.
- [`fintel-short-squeeze-assessment`](skills/fintel-short-squeeze-assessment/SKILL.md): Assess whether one named stock has a supported short-squeeze setup using short interest, borrowing conditions and price/volume evidence. Use for squeeze due diligence rather than a candidate leaderboard or a single short-interest lookup.
- [`fintel-valuation-expectations`](skills/fintel-valuation-expectations/SKILL.md): Calculate revenue growth implied by a stock's valuation under explicit terminal-multiple, horizon and discount assumptions. Use for reverse valuation rather than a price target or a full DCF.

- [`fintel-technical-analysis`](skills/fintel-technical-analysis/SKILL.md): Describe intraday OHLCV, session VWAP and compatible benchmark comparisons. IEX volume is sampled; historical signal testing is deferred.

### First packaged investment-question release

New portable workflows:

- [`fintel-company-briefing`](skills/fintel-company-briefing/SKILL.md): business, valuation, growth, financial strength, ownership and events with dated evidence.
- [`fintel-peer-comparison`](skills/fintel-peer-comparison/SKILL.md): curated peers with consistent growth, profitability and valuation measures.
- [`fintel-unusual-options-investigation`](skills/fintel-unusual-options-investigation/SKILL.md): flagged trades and same-window context with alternative explanations.
- [`fintel-watchlist-briefing`](skills/fintel-watchlist-briefing/SKILL.md): dated developments across a requested saved list or supplied universe, without unsolicited changes.

The other six R1 outcomes reuse `fintel-earnings-preview`, `fintel-earnings-review`,
`fintel-dividend-sustainability`, `fintel-valuation-expectations` (reverse valuation),
`fintel-short-squeeze-assessment` and `fintel-options-positioning-review` (options briefing).
Each includes evidence-gap behavior and release evaluation cases. All ten use the common scope,
evidence validation, calculation/lineage, interpretation, conclusion/counterevidence/change
conditions and requested-only persistence structure. These are instructions over existing tools;
source coverage and account entitlements remain authoritative.

### Evidence and capability boundaries

- Resolve security listings for company or fund analysis; public manager research instead resolves an identity with `fintel.search_managers`. Screening starts with `fintel.get_screening_capabilities`, followed by metric definitions and validation. Ambiguity requires clarification.
- Required data failures and denied entitlements are coverage gaps. Empty successful datasets do not justify positive or negative signals. Preserve financial periods, observation dates, currency, units and truncation metadata, and cite material facts.
- Company specialist assessments use read-only research tools. Live custom screens return rows in the same call without stored receipts; historical backtests create private receipts. Watchlist triage reads the signed-in user's selected lists. Account changes require explicit authorization; research does not imply a trade, saved screen or alert.
- Screen builder validates and executes live custom programs without polling, polls/pages historical backtest receipts, and supports user-requested saved screens and historical replay when the live tools are deployed. Execution does not save a definition. Manager comparisons and fund holdings are delayed disclosures, not current trades or complete live portfolios. Scenarios use explicit assumptions and do not promise returns or event probabilities.
- The general research skill maps the current tool families. Prefer a specialist for a full assessment, a simple lookup for a single figure, and stock discovery for an existing ranked shortlist.

Sixteen specialists, including company briefing and unusual-options investigation, correspond to the versioned contracts documented in `fintel-web/docs/Agentic-Message-Board-MCP-Plan.md`. The technical-analysis workflow is portable and does not add a separate server-side agent contract. Their adjacent evaluation cases cover sparse data and misleading interpretations. Packaging validation is separate from live-model evaluation of factual support, citations, freshness, entitlements and latency. These portable instructions do not enforce the server-side Fintel agent's deterministic evidence gates; Claude executes the workflow through the authenticated MCP tools.

The package does not yet include dedicated filing-delta, private-portfolio-exposure, thread-synthesis, watchlist-review/curation/building or profile-building skills; the new watchlist-briefing skill reuses existing list-review capabilities. Some underlying tools are available; absence of a portable skill is not evidence that its tools are unavailable. General research now covers macro observations through the source/series tools; a dedicated macro-outlook workflow remains outside this release.

## Sign-in

The connector uses OAuth. Claude registers itself automatically (dynamic client registration), then
opens a Fintel login and consent page. Approving it links your own Fintel account; tool calls use
that account's entitlements and API credits. No API key is stored in this repository.
Disconnect any time at https://fintel.io/oauth/connections.

## Install

**Claude Code**

```sh
/plugin marketplace add FintelVentures/fintel-claude
/plugin install fintel@fintel
```

Claude Code signs in through a `localhost` callback. Fintel accepts loopback callbacks
(`localhost`, `127.0.0.1`, `[::1]` on any port, path `/callback` or `/oauth/callback`), and the
consent page shows it as "An app on this computer".

**Claude.ai / desktop:** install from the Claude directory once listed, or add the connector URL
`https://mcp.fintel.io/mcp` under Settings > Connectors > Add custom connector.

## Maintaining

- Server-side OAuth and the allowlisted Claude callbacks live in `fintel-api`, `fintel-web` and
  `fintel-common`; this repository holds only the package. Callback changes there do not require a
  release here.
- When tools are added or renamed in `fintel-api`, update the tool references in `skills/`; every
  `fintel.*` name in `skills/` must exist in the `fintel-api` MCP catalog.
- Bump `version` in `.claude-plugin/plugin.json` for every submitted change, since the directory
  validates and scans each version.

## Support

Email help@fintel.io - https://fintel.io - Terms: https://fintel.io/terms - Privacy: https://fintel.io/privacy

## License

MIT, see `LICENSE`.

Screening instructions in 0.2.1 are synchronized with the OpenAI package 0.2.4. Deploy the matching API/common/jobs/web screening implementation, refresh the host catalog and verify authenticated execution; source/package validation does not establish a live-host pass.

Version 0.3.0 is synchronized with OpenAI 0.3.0. Export both plugins with the maintained
`fintel-api/integrations/package-openai-plugin.py` script (`--provider claude` for this plugin).
The exporter verifies byte-for-byte skill/reference parity and excludes marketplace wrappers
from a single-plugin archive. An exported ZIP is not a published marketplace update or a
recorded live-host evaluation. Current source-mode changes require normal application deployment
and restart; installing portable instructions alone does not deploy server contracts.

## Macro data update (0.3.1)

The existing general research and valuation skills now discover and read the 120-series FRED
catalog through three general macro tools. Native units, rates, FX orientation, missing cells,
collection health and latest-retained revision limits remain explicit. This adds an observed
risk-free input without presenting it as WACC or a completed DCF. Both provider packages retain
28 skills and the existing ten R1 workflows. Refresh the MCP catalog and update the installed
plugin to load the new guidance; exported source alone does not update a cached host.

## API catalog alignment (0.3.2)

The 28 existing workflows now cover retained analyst revisions and US fiscal-target windows/rankings,
country market breadth and technical coverage, canonical sectors/classifications, explicit SEC
annual/quarterly/TTM statements and ratios, unmapped SEC facts, retained research-change feeds,
private saved thesis/evidence checks, Damodaran country risk inputs and explicit-assumption DCF.
General research links focused references for financial/price evidence, breadth/classifications and
private research. Specialist guidance preserves valuation-date peer FX, retained market-cap baseline
dates, earnings reconciliation and live-screen versus historical-receipt behavior. Missing or
withheld evidence stays unavailable; private research remains private and writes require exact
content approval. Billing recovery uses website links, with no billing MCP tools.

This is source guidance aligned with API contracts reviewed on 2026-11-19, not a live-host acceptance
result. Both provider manifests and the workflow release are 0.3.2; skill/reference files remain
byte-identical. Install the updated plugin and refresh the MCP catalog. Server changes require their
normal deployment/restart; a package update or Git push does not deploy tools, populate collectors
or publish a directory release. No connector URL, OAuth identity or account permission changes.

## Reviewer examples

- **Fund holdings.** Call `fintel.get_fund_holdings_snapshot` with
  `{"country":"US","symbol":"VTI","limit":3}` for an ETF or substitute `ABAEX` for a mutual
  fund. Both returned holdings on the live MCP server on 23 November 2026. Coverage requires a
  US listing classified as an ETF, mutual fund or ETN and a public, ingested native N-PORT filing.
  The ticker must identify a unique SEC series through a resolved share class or an unambiguous
  legacy owner. The store lacked Vanguard 500 Index series `S000002839` (VFIAX and VOO) on that date.
  A fund can file with the SEC before its data becomes available here.
- **Peer analysis.** Call `fintel.get_security_peer_analysis` with
  `{"country":"US","symbol":"MSFT","detail":"compact"}`. If a curated group is unavailable,
  `method=gics_industry_fallback` identifies the same-market software comparison group.
- **Apple quarterly income.** Call `fintel.get_security_financial_statement` with
  `{"country":"US","symbol":"AAPL","kind":"income","source":"sec","period":"quarterly","limit":1}`.
  When the annual 10-K and nine-month 10-Q do not share revision evidence, look for the
  fiscal Q4 estimates under `asFiledDifferences`. The estimates retain both filing accessions.
- **Response detail.** Financial statements default to four periods. Set `include_evidence=true`
  and a small `limit` for filing receipts. Earnings surprises default to eight observations and
  premium sentiment to five completed sessions. Both accept `limit` or `include_history=true`
  for the retained series. Set `include_detail=true` on expiration analysis for the entitled
  intraday, strike and heatmap breakdowns. These defaults require the matching MCP server build.
