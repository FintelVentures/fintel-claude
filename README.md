# Fintel plugin for Claude

Connect Claude to [Fintel](https://fintel.io) to research stocks with Fintel's financial data and
account tools. The plugin bundles:

- **MCP connector** (`.mcp.json`): the remote Fintel MCP server at `https://mcp.fintel.io/mcp`.
- **Skills** (`skills/`): research workflows that use the Fintel tools. See below.

## Skills

| Skill | Purpose | Server-side counterpart |
| --- | --- | --- |
| `fintel-research` | General Fintel questions and tool map | general agent |
| `fintel-stock-discovery` | Leaderboard and ranking shortlists | `stock_discovery` |
| `fintel-investment-thesis` | Thesis with evidence, risks, invalidation | `investment_thesis` |
| `fintel-earnings-review` | Actual vs estimate, prior period, open questions | `earnings_review` |
| `fintel-bull-bear` | Balanced bull and bear cases | `bull_bear_review` |
| `fintel-catalyst-calendar` | Dated upcoming earnings, dividends, events | `catalyst_calendar` |
| `fintel-watchlist-triage` | Triage the user's stock lists | `watchlist_triage` |
| `fintel-claim-audit` | Grade claims for support | `claim_audit` |
| `fintel-scenario-analysis` | Conditional upside/base/downside frames | `scenario_analysis` |

These are the portable subset of the production research skill catalog in
`fintel-web/docs/Agentic-Message-Board-MCP-Plan.md` (section 6.1). Tool names come from the MCP
catalog in `fintel-api`; the expansion plan in `docs/Public-API-and-MCP-Catalog-Expansion-Plan.md`
lists planned tools, and only tools that exist today are referenced. Every skill shares the same
conventions: read-only by default, confirmation before any account change, fail closed when
evidence is missing, answer opinion questions directly, and end with one bounded next step.

**Not included yet**
- `filing_delta` and `peer_comparison`: they need per-security filing and peer-analysis MCP tools,
  which are not exposed today.
- `portfolio_exposure`: needs the private portfolio snapshot that exists only in the Fintel web app.
- `thread_synthesis`: tied to Fintel team chat.
- `watchlist_review`, `watchlist_curator`, `watchlist_builder`, `profile_builder`: not yet
  documented for external use.

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

Claude Code completes OAuth through a `localhost` callback, which Fintel does not allow yet, so use
Claude on the web or desktop for sign-in until that changes.

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

https://fintel.io - Terms: https://fintel.io/terms - Privacy: https://fintel.io/privacy

## License

MIT, see `LICENSE`.
