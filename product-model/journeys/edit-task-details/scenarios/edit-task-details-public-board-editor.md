---
{
  "kind": "primary",
  "result": "achieved",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer opens selected Demo Task content",
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
          "place": "devboard-web::public::board"
        }
      },
      "actor": "developer",
      "capability": "browse-tasks"
    },
    {
      "text": "The Product carries the selected subject into Edit Demo Task and attaches the mounted Pomodoro timer to the current selection; an existing estimate is not initialized, and a stored timestamp may not populate the date input",
      "kind": "product",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Description",
            "Notes",
            "Status",
            "Priority",
            "Tags",
            "Issue URL",
            "Issue number",
            "Due date"
          ]
        },
        {
          "entity": "pomodoro",
          "effect": "changes",
          "facts": [
            "Attached task"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer",
      "capability": "browse-tasks"
    },
    {
      "text": "The Developer changes form content and confirms Save with an explicitly chosen estimate without changing Status",
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
      "actor": "developer",
      "capability": "edit-task"
    },
    {
      "text": "The Product saves the submitted Demo Task content",
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
      "actor": "developer",
      "capability": "edit-task"
    },
    {
      "text": "The Product completes the editor and carries the Developer back toward the board",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer",
      "capability": "edit-task"
    },
    {
      "text": "The Developer browses the resulting board",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::board"
        }
      },
      "actor": "developer",
      "capability": "browse-tasks"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/TaskPage.jsx#TaskPage"
    },
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

# Edit task details — public board editor

## Trigger

The Developer opens a card to edit its selected subject.

## Outcome

The requested content change is saved with Status unchanged, and the Developer finishes at the board. The board-to-editor hand-off begins this Journey.
