---
name: standup-digest
description: "Draft a Yesterday / Today / Blockers standup update from your tasks. Uses the Nifty MCP server."
---

Draft my standup update.

1. Call `tasks_query` (resource=task, operation=list, assignee = me) three ways: (a) completedAt_gte = <start of yesterday, ISO> for what I FINISHED, (b) dueAt_lte = <end of today, ISO> with completed = false for what I’m DOING today, and (c) dueAt_lt = <now, ISO> with completed = false for anything OVERDUE.
2. Write a three-part standup — Yesterday / Today / Blockers — from (a), (b), and (c) respectively. A few bullets each.
3. Read-only: do not change any task.
