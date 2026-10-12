---
{
  "entities": [
    {
      "entity": "task",
      "collects": [
        "Title",
        "Description",
        "Notes",
        "Status",
        "Priority",
        "Tags",
        "Issue URL",
        "Issue number",
        "Due date",
        "Estimate"
      ],
      "shows": [
        "Title",
        "Description",
        "Notes",
        "Status",
        "Priority",
        "Tags",
        "Issue URL",
        "Issue number"
      ]
    },
    {
      "entity": "code-snippet",
      "collects": [
        "Language",
        "Code"
      ],
      "shows": [
        "Language",
        "Code"
      ]
    },
    {
      "entity": "recent-activity",
      "shows": [
        "Actions",
        "Times"
      ]
    },
    {
      "entity": "assignee-history",
      "shows": [
        "Previous assignees",
        "Replacement times"
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Task/TaskModal.jsx#TaskModal"
    }
  ],
  "entryPoints": [
    {
      "devboard-web": "/task/:id"
    }
  ]
}
---

# Edit Task

The selected task working context presents editable content, existing code and available histories. Board selection and the deep link share this subject. Link copying and QR presentation encode the ordinary task route without changing access. Existing Estimate is not initialized into the form, and stored timestamp-shaped Due date values can display as empty in the date input. Attempted dependency selections are sent by the form but discarded by connected persistence; they are not a kept Task fact.
