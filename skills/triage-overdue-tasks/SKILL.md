---
name: triage-overdue-tasks
description: "Work through your own overdue tasks and decide what to reschedule, reassign, drop, or do now. Uses the Nifty MCP server."
---

Help me triage MY overdue tasks.

1. Call `tasks_query` (resource=task, operation=list) with assignee = me, dueAt_lt = <now, ISO 8601>, completed = false. Page through all of them.
2. For each overdue task, recommend exactly one action — reschedule, reassign, drop, or do-now — with a one-line reason.
3. Apply only the changes I approve, via `tasks_mutate` (resource=task, operation=update): a new dueAt, or add/remove an assignee. One task at a time; confirm before each write.
