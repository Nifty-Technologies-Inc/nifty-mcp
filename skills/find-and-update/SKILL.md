---
name: find-and-update
description: "Find the tasks matching a description and apply a change — with a review step first. Uses the Nifty MCP server."
---

## Inputs

- `<what>`: What to find, e.g. "tasks due this week with no assignee".
- `<change>`: The change to apply, e.g. "set the due date to Friday".

Ask the user for any input they have not given yet.

## Steps

Find the tasks matching "<what>" and apply this change: <change>.

1. Call `tasks_query` — operation=search with query="<what>" for a keyword match, or operation=list with field filters when "<what>" names concrete fields (status, dueAt, assignee, …). Show me the matches.
2. Describe exactly what "<change>" will set on each matched task.
3. Confirm, then apply via `tasks_mutate` (resource=task, operation=update), one task at a time. Never bulk-update without showing me the list first.
