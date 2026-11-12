# Fintel plugin for Claude

Connect Claude to [Fintel](https://fintel.io) to research stocks with Fintel's financial data and
account tools. The plugin bundles:

- **MCP connector** (`.mcp.json`): the remote Fintel MCP server at `https://mcp.fintel.io/mcp`.
- **Skill** (`skills/fintel-research`): guidance for using the Fintel tools accurately.

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
- Bump `version` in `.claude-plugin/plugin.json` for every submitted change, since the directory
  validates and scans each version.

## Support

https://fintel.io - Terms: https://fintel.io/terms - Privacy: https://fintel.io/privacy

## License

MIT, see `LICENSE`.
