---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer changes the Demo Task dependency selection",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Dependencies"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product saves the Demo Task dependency selections while retaining its current Status",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "changes",
          "facts": [
            "Title",
            "Description",
            "Notes",
            "Status",
            "Priority",
            "Tags",
            "Issue URL",
            "Issue number",
            "Due date",
            "Dependencies"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Task/TaskModal.jsx#TaskModal"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    }
  ]
}
---

# Remove a demo dependency

## Trigger

The Developer changes an existing demo dependency selection and saves without changing Status or selecting a new estimate.

## Outcome

The local dependency list no longer includes the removed task. A linked editor completes at the demo board.

## Edge cases

- The current task is excluded from selectable references; other loaded tasks are offered regardless of completion.
- No cycle detection, deletion cleanup or movement gate is established.
- Normal Save title validation still applies.
