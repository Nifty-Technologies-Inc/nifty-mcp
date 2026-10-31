---
name: plan-my-week
description: "Draft a realistic day-by-day plan for the week from your open, due-soon tasks. Uses the Nifty MCP server."
---

Plan my week from my open tasks.

1. Call `tasks_query` (resource=task, operation=list) with assignee = me (my team-member id), dueAt_lte = <end of this week, ISO 8601>, completed = false, sort = dueAt. Page through all results using the returned cursor.
2. Group the tasks by project and by day, and propose a realistic day-by-day plan for the rest of the week. Call out overloaded days and anything already overdue.
3. Confirm the plan with me BEFORE calling `tasks_mutate` (resource=task, operation=update) to reschedule anything (startAt / dueAt). Never reschedule without my confirmation.
