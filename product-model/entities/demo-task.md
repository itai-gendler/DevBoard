---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
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
      "verb": "has inherited",
      "cardinality": "one-to-one"
    },
    {
      "entity": "assignee-history",
      "verb": "has inherited",
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
    },
    {
      "entity": "demo-task",
      "verb": "depends on",
      "cardinality": "many-to-many"
    }
  ]
}
---

# Demo Task

A locally retained task in Demo Mode. Optional metadata may be absent or inherited from a previously loaded task snapshot.

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
- **Viewers** — Recorded mock viewer identifiers; the explicit Demo Mode identity and viewer routine use different identifier keys.
- **Dependencies** — Other demo tasks selected as dependencies, without transition enforcement.
