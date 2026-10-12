---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/tasks.js:7-127"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/models/Task.js#taskSchema"
    }
  ],
  "relations": [
    {
      "entity": "code-snippet",
      "verb": "contains",
      "cardinality": "one-to-many"
    },
    {
      "entity": "recent-activity",
      "verb": "has",
      "cardinality": "one-to-one"
    },
    {
      "entity": "assignee-history",
      "verb": "has",
      "cardinality": "one-to-one"
    },
    {
      "entity": "time-tracker",
      "verb": "has mounted",
      "cardinality": "one-to-many"
    },
    {
      "entity": "pomodoro",
      "verb": "is attached to",
      "cardinality": "one-to-many"
    }
  ]
}
---

# Task

A task retained through connected persistence.

## Information kept

- **Title** — The task title.
- **Description** — Task description text.
- **Notes** — Task notes; the Private Notes label does not establish private disclosure.
- **Status** — The current task column value.
- **Previous status** — The column value preceding the most recent actual status change, when available.
- **Priority** — Low, Medium or High priority.
- **Tags** — The task tag values.
- **Issue URL** — The manually supplied GitHub issue link.
- **Issue number** — The supplied issue number, when present.
- **Assignee** — The assigned account, when present; assignment is not ownership.
- **Due date** — The task deadline, when present.
- **Estimate** — The selected estimate text, when present.
- **Order** — The ordering value used within its column, when present.
- **Pomodoro count** — Completed focus-session credits associated with the task.
- **Created** — Creation time, when available.
- **Last changed** — Most recent saved change time, when available.
- **Viewers** — Recorded account references added once when an individual task is retrieved; viewer recording leaves task timestamps unchanged.

## States

### Backlog

Work held before active progress.

### In Progress

Work in active progress.

### Review

Work placed in review.

### Done

Work marked done.
