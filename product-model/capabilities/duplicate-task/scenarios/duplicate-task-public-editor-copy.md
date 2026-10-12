---
{
  "kind": "primary",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer requests a duplicate of the selected Demo Task after entering another nonempty code block and choosing an estimate",
      "kind": "actor",
      "entities": [
        {
          "entity": "demo-task",
          "effect": "reads",
          "facts": [
            "Title",
            "Status"
          ],
          "as": "original"
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
      "text": "The Product reads the original Code Snippet content",
      "kind": "product",
      "entities": [
        {
          "entity": "code-snippet",
          "effect": "reads",
          "facts": [
            "Language",
            "Code"
          ],
          "as": "existing-code"
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
      "text": "The Product creates the copied Demo Task and its own Code Snippet blocks",
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
            "Due date",
            "Estimate",
            "Dependencies",
            "Pomodoro count"
          ],
          "as": "copy"
        },
        {
          "entity": "code-snippet",
          "effect": "creates",
          "facts": [
            "Language",
            "Code"
          ],
          "with": "copy",
          "as": "copy-code"
        },
        {
          "entity": "code-snippet",
          "effect": "creates",
          "facts": [
            "Language",
            "Code"
          ],
          "with": "copy",
          "as": "copy-entered-code"
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
      "target": "devboard/client/src/components/Board/TaskCard.jsx#TaskCard"
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

# Duplicate current editor content

## Trigger

The Developer chooses Duplicate for an existing task.

## Outcome

Editor copying uses current form values, limits the copied title to 100 characters including its suffix, combines the existing and newly entered snippets, excludes issue linkage and clears dependencies. The copy starts its own count/order defaults in connected mode.

## Edge cases

- No assignment, histories, viewers or elapsed tracking is copied as retained user data.
- An unchanged existing estimate is not initialized into the editor copy payload.
- Without code no dependent code block is created.
- Editor completion closes the editor; a linked editor carries the Developer to the board containing the copy.
- Duplication is not refused merely because its resulting title duplicates another loaded task.
