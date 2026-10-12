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
          "place": "devboard-web::signed-in::new-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product creates the task and its entered Code Snippet",
      "kind": "product",
      "entities": [
        {
          "entity": "task",
          "effect": "creates",
          "facts": [
            "Title",
            "Description",
            "Notes",
            "Status",
            "Previous status",
            "Priority",
            "Tags",
            "Issue URL",
            "Issue number",
            "Due date",
            "Estimate",
            "Order",
            "Pomodoro count",
            "Created",
            "Last changed",
            "Viewers"
          ],
          "to": "Review"
        },
        {
          "entity": "code-snippet",
          "effect": "creates",
          "facts": [
            "Language",
            "Code"
          ],
          "with": "task"
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::new-task"
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

# Create a task in Review

## Trigger

The Developer opens New Task, supplies content and optional code, and chooses Save.

## Outcome

The new task enters Review with saved content, independent snippet identity and server defaults. Inline completion returns to the board already being used.

## Edge cases

- Normal Save refuses a blank or duplicate loaded title.
- Optional empty fields remain empty or absent; absent demo timestamps, assignment, viewers and ordering are not synthesized.
- Stored defaults include Medium priority, empty description/notes/tags, no previous status, order and Pomodoro count zero, and creation/change timestamps.
- Without entered code no dependent snippet is created.
- Connected persistence discards attempted dependency choices; Demo Task creation retains them.
