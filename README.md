<p align="center"><img src="assets/embarko-logo.png" alt="Embarko" width="120"></p>

# Embarko MCP

Deploy and host AI-built apps and websites, and get a live URL without any DevOps setup. [Embarko](https://embarko.ai) runs the app at `https://<app-name>.embarko.app`.

This is a remote MCP server (Streamable HTTP) at `https://mcp.embarko.ai/mcp`. Nothing to install: your AI tool connects to it, and you sign in to Embarko once through OAuth (the same account as embarko.ai).

## Tools
| Tool | What it does |
|---|---|
| `deploy_app` | Deploy or update an app from its files (`appName`, `files`, optional `appType`, `version`) |
| `read_app` | App status, logs, deployments, env vars, domains, analytics |
| `update_app` | Set env vars, add and verify a custom domain, roll back, send feedback |
| `app_danger_zone` | Delete an env var or domain, rename or delete an app |

## Connect from Cline
Install it from the Cline MCP Marketplace, or open **MCP Servers → Configure MCP Servers** and add this to `cline_mcp_settings.json`:
```json
{
  "mcpServers": {
    "embarko": {
      "type": "streamableHttp",
      "url": "https://mcp.embarko.ai/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```
Then click **Authenticate** next to `embarko` in the MCP Servers list and sign in to Embarko in the browser. `type` must be `streamableHttp` (the server has no SSE endpoint). Agent-driven install steps are in [llms-install.md](llms-install.md).

## Connect from Claude
Add it from the Claude directory: https://claude.ai/directory/embarko

Or in Claude Code:
```bash
claude mcp add --transport http embarko https://mcp.embarko.ai/mcp
```
then run `/mcp` and sign in.

## Connect from Kiro
[![Add to Kiro](https://kiro.dev/images/add-to-kiro.svg)](https://kiro.dev/launch/mcp/add?name=embarko&config=%7B%22url%22%3A%22https%3A%2F%2Fmcp.embarko.ai%2Fmcp%22%2C%22disabled%22%3Afalse%7D)

Or add it manually to `.kiro/settings/mcp.json` ([docs](https://kiro.dev/docs/mcp/configuration/)):
```json
{
  "mcpServers": {
    "embarko": {
      "url": "https://mcp.embarko.ai/mcp",
      "disabled": false
    }
  }
}
```

## MCP Registry
The server is listed in the official MCP Registry as `com.walkover.embarko/embarko`; [server.json](server.json) is the listing. The logo shown there comes from `icons` in `server.json`. To publish a change, bump `version` in `server.json`, then:
```bash
mcp-publisher login dns --domain embarko.ai --private-key "..."
mcp-publisher publish
```

## Docs
- Quickstart: https://embarko.ai/docs/quickstart
- Connectors: https://embarko.ai/docs/connectors

## Support
- Email: hello@embarko.ai
- Privacy Policy: https://embarko.ai/privacy
