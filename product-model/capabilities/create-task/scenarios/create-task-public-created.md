---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer submits the new content and selected initial column with an issue number, due date, estimate and one nonempty code block",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::new-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product creates the Demo Task and its entered Code Snippet",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "creates",
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
            "Dependencies",
            "Pomodoro count"
          ]
        },
        {
          "entity": "code-snippet",
          "effect": "creates",
          "facts": [
            "Language",
            "Code"
          ],
          "with": "demo-task"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::new-task"
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
    }
  ]
}
---

# Create a demo task

## Trigger

The Developer opens New Task, supplies content and optional code, and chooses Save.

## Outcome

The new demo task retains its supplied local status/content and starts Pomodoro count at zero. Inline completion returns to the board already being used.

## Edge cases

- Normal Save refuses a blank or duplicate loaded title.
- Optional empty fields remain empty or absent; absent demo timestamps, assignment, viewers and ordering are not synthesized.
- Normal form initialization supplies Medium priority and empty description/notes/tags; the local creator adds only the Pomodoro count default.
- Without entered code no dependent snippet is created.
- Connected persistence discards attempted dependency choices; Demo Task creation retains them.
