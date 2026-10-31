---
name: project-status-digest
description: "Summarize a project’s status: progress, overdue items, recent shipments, and top risks. Uses the Nifty MCP server."
---

## Inputs

- `<projectName>`: Name (or partial name) of the project to summarize.

Ask the user for any input they have not given yet.

## Steps

Summarize the current status of the project "<projectName>".

1. Call `planning_query` (resource=project, operation=search, query="<projectName>") to resolve the project id. If several match, ask me which one.
2. Call `tasks_query` (resource=task, operation=list, projectId=<id>, includeTotal=true) and page through every task.
3. Produce a concise digest: percent complete, counts by status, overdue items, what shipped recently, and the top risks or blockers. This is read-only — do not modify anything.
