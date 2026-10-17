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

**Manually:** add the endpoint as a remote MCP server and send a Nifty Personal Access Token as a
Bearer token. Create one at `app.nifty.pm/settings/personal-access-tokens`:

```
Authorization: Bearer <your Nifty personal access token>
```

Claude, ChatGPT and Microsoft 365 Copilot can instead sign in with your Nifty account through
Nifty's connector, started from **Settings → MCP**. Other clients need the token.

The plugin and extension manifests in this repository read the token from the `NIFTY_PAT`
environment variable (Gemini CLI asks for it when you install the extension):

```sh
export NIFTY_PAT=<your Nifty personal access token>
```

Claude Code example:

```sh
claude mcp add --transport http nifty https://mcp.niftypm.com/mcp --header "Authorization: Bearer $NIFTY_PAT"
```

### Install as a plugin or extension

This repository is also a plugin for the clients that install from a Git repo:

| Client | Install |
|--------|---------|
| Claude Code | `/plugin marketplace add Nifty-Technologies-Inc/nifty-mcp`, then `/plugin install nifty@nifty` |
| Gemini CLI | `gemini extensions install https://github.com/Nifty-Technologies-Inc/nifty-mcp` |
| Cursor | Copy [`mcp.json`](./mcp.json) into `.cursor/mcp.json`, or add the endpoint in **Settings → MCP** |
| Cline | See [llms-install.md](./llms-install.md) |

### Clients that only support stdio

Bridge with [`mcp-remote`](https://github.com/geelen/mcp-remote). Keep the space out of `args` by
putting the whole header value in `env`:

```json
{
  "mcpServers": {
    "nifty": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.niftypm.com/mcp", "--header", "Authorization:${NIFTY_AUTH}"],
      "env": { "NIFTY_AUTH": "Bearer <your Nifty personal access token>" }
    }
  }
}
```

## Example prompts

- "What's overdue in the Website Redesign project? Group it by assignee."
- "Create a task in Marketing called 'Draft Q4 launch post', assign it to me, due Friday."
- "Summarize this week's messages in the Product discussion."
- "Move every task tagged 'bug' in the Mobile App project to the In Review status."
- "Which milestones in the Client Onboarding project are at risk?"
- "Find the doc about our release checklist and list its open items."

## Tools

Tools are grouped by domain, and each domain has three verbs: `_query` (browse, filter, paginate,
full-text search), `_mutate` (create, update, link relations, bulk writes) and `_destroy` (delete).

| Tool | What it does |
|------|--------------|
| `tasks_query` | Find tasks, checklists and reminders |
| `tasks_mutate` | Create or update tasks, checklists and reminders |
| `tasks_destroy` | Delete tasks, checklists and reminders |
| `planning_query` | Find projects, portfolios, milestones and goals |
| `planning_mutate` | Create or update projects, portfolios, milestones and goals |
| `planning_destroy` | Delete projects, portfolios, milestones and goals |
| `communication_query` | Find chats, messages and check-ins |
| `communication_mutate` | Create or update chats, messages and check-ins |
| `communication_destroy` | Delete chats, messages and check-ins |
| `knowledge_query` | Find docs and files |
| `knowledge_mutate` | Create or update docs and files |
| `knowledge_destroy` | Delete docs and files |
| `people_query` | Find members |
| `people_mutate` | Invite or update members |
| `people_destroy` | Remove members |
| `reporting_query` | Find time entries, charts and project activity |
| `reporting_mutate` | Create or update time entries and charts |
| `reporting_destroy` | Delete time entries and charts |
| `admin_query` | Find labels, roles, favorites and custom fields |
| `admin_mutate` | Create or update labels, roles and favorites |
| `admin_destroy` | Delete labels, roles and favorites |

The full machine-readable list (descriptions and input schemas) is published at
[`mcp.niftypm.com/.well-known/mcp/server-card.json`](https://mcp.niftypm.com/.well-known/mcp/server-card.json).

Every call runs as the signed-in user (or the token's agent identity), with that user's Nifty
permissions. The server only sees what you can see.

## Prompts

- `plan_my_week`: Draft a realistic day-by-day plan for the week from your open, due-soon tasks.
- `project_status_digest`: Summarize a project’s status: progress, overdue items, recent shipments, and top risks.
- `triage_overdue_tasks`: Work through your own overdue tasks and decide what to reschedule, reassign, drop, or do now.
- `standup_digest`: Draft a Yesterday / Today / Blockers standup update from your tasks.
- `meeting_notes_to_tasks`: Turn meeting notes into well-formed tasks in a project, after your review.
- `find_and_update`: Find the tasks matching a description and apply a change — with a review step first.

## Docs and support

- Documentation: [Nifty MCP Server guide](https://help.niftypm.com/en/articles/15603530-nifty-mcp-server-connect-your-ai-assistants)
- Support: [nifty.pm](https://nifty.pm)

## License

The contents of this repository are MIT-licensed (see [LICENSE](./LICENSE)). The hosted service is
covered by Nifty's terms of service.
