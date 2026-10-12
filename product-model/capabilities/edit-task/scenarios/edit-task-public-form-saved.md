---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer selects the saved content to work on with an explicitly chosen estimate",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title"
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
      "text": "The Developer changes the form content and confirms Save with an explicitly chosen estimate",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product saves the submitted Demo Task content while retaining its current Status",
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
            "Estimate",
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/tasks.js:7-127"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/models/Task.js#taskSchema"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/ai.js:7-95"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/hooks/useSuggestTags.jsx#useSuggestTags"
    }
  ]
}
---

# Save editable task content

## Trigger

The Developer edits the selected task, chooses an estimate and saves while leaving Status unchanged.

## Outcome

Submitted content is saved and the editor closes. A linked editor carries the Developer back to the board; an inline editor completes in the current board.

## Edge cases

- Without newly entered code existing snippets remain.
- An unchanged existing estimate is omitted from initialForm and the payload, so ordinary Save does not automatically erase it.
- Normal Save checks title against the loaded collection.
- Failure before a successful response can keep the form busy and open.
