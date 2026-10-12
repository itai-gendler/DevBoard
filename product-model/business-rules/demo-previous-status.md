---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "demo-task",
      "facts": [
        "Status",
        "Previous status"
      ],
      "effect": "changes",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    }
  ]
}
---

# Local status changes retain the preceding status

A truthy different local Status remembers the preceding status. Other demo updates do not create status-change history or change timestamps automatically, and custom/legacy values remain possible.
