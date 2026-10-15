# Nifty MCP Server

The official [Model Context Protocol](https://modelcontextprotocol.io) server for
[Nifty](https://nifty.pm). It gives AI agents access to your Nifty workspace: tasks, projects,
messages, documents, files and more. It works with Claude, ChatGPT, Cursor and any other client
that supports remote MCP servers.

This is a hosted (remote) server. There is nothing to install or run. This repository holds its
public description, registry metadata (`server.json`) and connection guide. The server itself is
operated by Nifty.

## Connect

**Endpoint:** `https://mcp.niftypm.com/mcp` (Streamable HTTP)

**Easiest:** in Nifty, open **Settings → MCP** (`app.nifty.pm/settings/mcp`). The wizard covers
Claude, Claude Code, ChatGPT and Cursor, with a ready-to-paste config or an OAuth connector flow.

**Manually:** add the endpoint as a remote MCP server in your client. Clients that support OAuth
sign you in with your Nifty account. Other clients send a Personal Access Token as a Bearer token:

```
Authorization: Bearer <your Nifty personal access token>
```

Create tokens at `app.nifty.pm/settings/personal-access-tokens`.

Claude Code example:

```sh
claude mcp add --transport http nifty https://mcp.niftypm.com/mcp
```

## What it exposes

Tools are grouped by domain (tasks, planning, communication, people, knowledge, reporting, admin),
and each domain has three verbs:

| Tool | Purpose |
|------|---------|
| `{domain}_query` | Browse, filter, paginate, or full-text search |
| `{domain}_mutate` | Create and update, link relations, bulk writes |
| `{domain}_destroy` | Delete |

Every call runs as the signed-in user (or the token's agent identity), with that user's Nifty
permissions. The server only sees what you can see.

## Docs and support

- Documentation: [docs.nifty.pm/mcp](https://docs.nifty.pm/mcp)
- Support: [nifty.pm](https://nifty.pm)

## License

The contents of this repository are MIT-licensed (see [LICENSE](./LICENSE)). The hosted service is
covered by Nifty's terms of service.
