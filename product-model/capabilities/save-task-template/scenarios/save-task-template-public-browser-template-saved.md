---
{
  "kind": "primary",
  "routes": {
    "web": "New Task",
    "edit": "Edit Task"
  },
  "steps": [
    {
      "text": "The Developer requests saving the current form as a template",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::new-task"
        },
        "edit": {
          "place": "devboard-web::public::edit-task"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product appends a Task template in browser storage",
      "kind": "product",
      "entities": [
        {
          "entity": "task-template",
          "effect": "creates",
          "facts": [
            "Name",
            "Title",
            "Description",
            "Priority",
            "Tags"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::new-task"
        },
        "edit": {
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
    }
  ]
}
---

# Save current form content as a browser-local template

## Trigger

The Developer supplies a nonblank form title and chooses Save as reusable template.

## Outcome

A new template retains the form title as Name/Title, description, priority and comma-separated tag input. The form itself remains unsaved.

## Edge cases

- A blank title disables template saving.
- Existing templates are appended to; no browser, application, editing or removal of templates is established.
- Malformed stored template data or unavailable storage can prevent completion; uniform recovery is not promised.
