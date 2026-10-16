# Installing the Nifty MCP server

Nifty's MCP server is hosted. There is no package to install and no command to run: add the
remote endpoint to your MCP client configuration.

- **Endpoint:** `https://mcp.niftypm.com/mcp`
- **Transport:** Streamable HTTP
- **Auth:** a Nifty Personal Access Token sent as a Bearer token. The user creates one at
  `https://app.nifty.pm/settings/personal-access-tokens` and pastes it in. Never invent a token.
  The server does not support OAuth dynamic client registration, so a client cannot sign in on
  its own: send the token.

## Cline

Add this to `cline_mcp_settings.json`. `type` must be `streamableHttp`; without it Cline falls back
to the legacy SSE transport.

```json
{
  "mcpServers": {
    "nifty": {
      "type": "streamableHttp",
      "url": "https://mcp.niftypm.com/mcp",
      "headers": {
        "Authorization": "Bearer <NIFTY_PERSONAL_ACCESS_TOKEN>"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## Clients that only support stdio

Bridge with [`mcp-remote`](https://github.com/geelen/mcp-remote). Keep the space out of `args`
by putting the whole header value in `env`:

```json
{
  "mcpServers": {
    "nifty": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.niftypm.com/mcp", "--header", "Authorization:${NIFTY_AUTH}"],
      "env": { "NIFTY_AUTH": "Bearer <NIFTY_PERSONAL_ACCESS_TOKEN>" }
    }
  }
}
```

## Check it works

Ask the assistant to list your Nifty projects. It should call `planning_query` and return projects
from your workspace.
