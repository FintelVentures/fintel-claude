# Fintel plugin for Claude

Connect Claude to [Fintel](https://fintel.io) to research stocks with Fintel's financial data and
account tools. The plugin bundles:

- **MCP connector** (`.mcp.json`): the remote Fintel MCP server at `https://mcp.fintel.io/mcp`.
- **Skills** (`skills/`): research workflows that use the Fintel tools. See below.

## Skills

Version 0.2.0 bundles 23 portable skills: nine established workflows and fourteen specialist assessments. Each linked skill describes when to use it, its evidence tools, output and limitations. All tools require an authenticated MCP connection and the account's entitlements; inspect the live tool list before relying on a dependency. A package version does not prove that the matching server tools have been deployed.

### Established workflows

- [`fintel-research`](skills/fintel-research/SKILL.md): Answer focused stock, fund, financial-data or Fintel account questions using the live MCP tool catalog. Use for lookups and general research when no specialist workflow fits; prefer specialist skills for a full assessment.
- [`fintel-stock-discovery`](skills/fintel-stock-discovery/SKILL.md): Find research candidates from Fintel leaderboards and rankings, including squeeze candidates, yield leaders and market movers. Use for ranked shortlists; use screen-builder to design custom criteria and specialist assessments to investigate one returned stock.
- [`fintel-investment-thesis`](skills/fintel-investment-thesis/SKILL.md): Build a sourced investment thesis for one company with supporting and contradicting evidence, catalysts, risks, assumptions and invalidation conditions. Use for a deep dive or investment case rather than a narrow metric or specialist assessment.
- [`fintel-earnings-review`](skills/fintel-earnings-review/SKILL.md): Review reported earnings results, actual versus estimated figures, supported period comparisons and open questions. Use after results; use earnings-preview before an announcement and earnings-quality-review for profit-to-cash analysis.
- [`fintel-bull-bear`](skills/fintel-bull-bear/SKILL.md): Stress-test a stock thesis with the strongest supported bull and bear cases, shared assumptions, conflicting evidence and observations that would settle disagreements. Use when the user requests both sides or challenges an existing view.
- [`fintel-catalyst-calendar`](skills/fintel-catalyst-calendar/SKILL.md): Build a dated calendar of upcoming earnings, dividends and supported biotech events for one company, preserving estimated windows and coverage gaps. Use for timing; use earnings-preview or biotech-event-due-diligence for deeper event analysis.
- [`fintel-watchlist-triage`](skills/fintel-watchlist-triage/SKILL.md): Review a signed-in user's Fintel stock list using list-level filings, insider and ownership evidence to prioritize names for investigation or monitoring. Use for private watchlist triage; this does not edit lists or review a public manager portfolio.
- [`fintel-claim-audit`](skills/fintel-claim-audit/SKILL.md): Check financial claims in supplied text or a discussion against cited evidence and available Fintel observations. Identify unsupported, stale, conflicting or unverifiable claims and citation mismatches without manufacturing outside support.
- [`fintel-scenario-analysis`](skills/fintel-scenario-analysis/SKILL.md): Frame conditional upside, base and downside outcomes for a company or event with a common horizon, explicit assumptions, triggers and invalidation conditions. Use for what-if analysis; use valuation-expectations or dilution-and-runway for their dedicated calculations.

### Specialist assessments

- [`fintel-analyst-expectations-review`](skills/fintel-analyst-expectations-review/SKILL.md): Reconcile analyst price targets, rating distributions, fiscal-period forecasts and estimate dispersion for one stock. Use for consensus and disagreement analysis; this surface cannot establish historical earnings-estimate revisions without comparable snapshots.
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
- [`fintel-screen-builder`](skills/fintel-screen-builder/SKILL.md): Translate stock-screening objectives into reviewable criteria using Fintel's exact metric definitions and units. Use to design a screen; this does not execute, save or schedule it or return matched securities.
- [`fintel-short-squeeze-assessment`](skills/fintel-short-squeeze-assessment/SKILL.md): Assess whether one named stock has a supported short-squeeze setup using short interest, borrowing conditions and price/volume evidence. Use for squeeze due diligence rather than a candidate leaderboard or a single short-interest lookup.
- [`fintel-valuation-expectations`](skills/fintel-valuation-expectations/SKILL.md): Calculate revenue growth implied by a stock's valuation under explicit terminal-multiple, horizon and discount assumptions. Use for reverse valuation rather than a price target or a full DCF.

### Evidence and capability boundaries

- Resolve security listings for company or fund analysis; public manager research instead resolves an identity with `fintel.search_managers`. Screen design starts with metric definitions. Ambiguity requires clarification.
- Required data failures and denied entitlements are coverage gaps. Empty successful datasets do not justify positive or negative signals. Preserve financial periods, observation dates, currency, units and truncation metadata, and cite material facts.
- Public specialist assessments use read-only research tools. Watchlist triage reads the signed-in user's selected lists. Account changes require explicit authorization; research does not imply a trade, saved screen or alert.
- Screen builder produces dictionary-backed criteria only. Manager comparisons and fund holdings are delayed disclosures, not current trades or complete live portfolios. Scenarios use explicit assumptions and do not promise returns or event probabilities.
- The general research skill maps the current tool families. Prefer a specialist for a full assessment, a simple lookup for a single figure, and stock discovery for an existing ranked shortlist.

The fourteen specialists correspond to the versioned contracts documented in `fintel-web/docs/Agentic-Message-Board-MCP-Plan.md`. Their adjacent evaluation cases cover sparse data and misleading interpretations. Packaging validation is separate from live-model evaluation of factual support, citations, freshness, entitlements and latency. These portable instructions do not enforce the server-side Fintel agent's deterministic evidence gates; Claude executes the workflow through the authenticated MCP tools.

The package does not yet include dedicated filing-delta, peer-comparison, private-portfolio-exposure, thread-synthesis, watchlist-review/curation/building or profile-building skills. Some underlying tools are available; absence of a portable skill is not evidence that its tools are unavailable. No macro-outlook skill is included because the implemented workflows do not establish adequate macroeconomic data coverage.

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
