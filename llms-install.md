# Installing the Embarko MCP server

These steps are for AI agents (such as Cline) setting up this server for a user.

Embarko MCP is a remote server. There is nothing to clone, build or run locally: the client connects to `https://mcp.embarko.ai/mcp` over Streamable HTTP. There is no API key to ask for; the user signs in to Embarko through OAuth in their browser.

## 1. Add the server to the MCP settings
Add this entry to the `mcpServers` object in the MCP settings file (for Cline: `cline_mcp_settings.json`). Keep any servers already in the file.

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

The `type` must be `streamableHttp`; this server does not offer the legacy SSE transport.

## 2. Sign in
The server answers `401` until the user signs in. In Cline, open **MCP Servers**, find `embarko` and click **Authenticate**. A browser window opens for the Embarko sign-in (the same account as https://embarko.ai; signing up is free). Ask the user to finish it; do not try to sign in for them.

## 3. Verify
Call `read_app` with `{ "action": "status", "appName": "<an existing app>" }`, or deploy a small test app with `deploy_app`. If the tools are listed, the connection works.

## Tools
- `deploy_app`: deploy or update an app from its files: `{ appName, files, appType?, version? }`. Send the whole app every time.
- `read_app`: `status`, `logs`, `deployments`, `env_vars`, `domains`, `analytics` or `rename_status` for an app.
- `update_app`: `set_env_vars`, `apply_env_vars`, `register_domain`, `verify_domain`, `rollback` or `submit_feedback`.
- `app_danger_zone`: `delete_env_var`, `delete_domain`, `rename_app` or `delete_app`. Confirm with the user first.

Full guide: https://embarko.ai/docs/quickstart
