---
{
  "entities": [
    {
      "entity": "task",
      "shows": [
        "Title",
        "Description",
        "Status",
        "Previous status",
        "Priority",
        "Tags",
        "Issue number",
        "Assignee",
        "Due date",
        "Estimate",
        "Order",
        "Pomodoro count",
        "Created",
        "Last changed"
      ]
    },
    {
      "entity": "code-snippet",
      "shows": [
        "Language",
        "Code"
      ]
    },
    {
      "entity": "account",
      "shows": [
        "Name"
      ]
    },
    {
      "entity": "board-preferences",
      "shows": [
        "Column names",
        "Pinned tasks",
        "Browsing choices",
        "Previous visit"
      ],
      "collects": [
        "Column names",
        "Browsing choices"
      ]
    },
    {
      "entity": "pomodoro",
      "shows": [
        "Phase",
        "Remaining time",
        "Completed sessions",
        "Attached task"
      ]
    },
    {
      "entity": "time-tracker",
      "shows": [
        "Elapsed time"
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/KanbanBoard.jsx#KanbanBoard"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/Column.jsx#Column"
    }
  ]
}
---

# Board

The task collection presents matching task content, column counts, focus timing, elapsed trackers and derived summaries. Search includes title, description, tags, priority and snippet code; tag selection matches exact stored spelling. Priority sorting and pin precedence affect visible order.

Created is presented as relative time. Due date and Last changed contribute overdue/stale indicators rather than raw timestamp displays.
