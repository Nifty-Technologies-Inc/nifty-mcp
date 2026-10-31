---
name: meeting-notes-to-tasks
description: "Turn meeting notes into well-formed tasks in a project, after your review. Uses the Nifty MCP server."
---

## Inputs

- `<notes>`: The raw meeting notes to extract action items from.
- `<projectName>`: Name of the project the new tasks belong in.

Ask the user for any input they have not given yet.

## Steps

Turn these meeting notes into tasks in the project "<projectName>".

Notes:
<notes>

1. Call `planning_query` (resource=project, operation=search, query="<projectName>") to resolve the project id.
2. Extract the actionable items from the notes. Each becomes a task with a clear title, an owner if one is named, and a due date if one is mentioned.
3. Show me the proposed task list and confirm BEFORE creating anything. On approval, call `tasks_create` (resource=task, operation=create) for each — set projectId, name, description, dueAt, and assignees where known.
