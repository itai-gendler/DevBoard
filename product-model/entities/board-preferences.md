---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Dashboard.jsx#Dashboard"
    }
  ]
}
---

# Board preferences

Browser-local board choices and visit information; some choices are transient, while columns, pins, search history and visits are retained in browser storage.

## Information kept

- **Column names** — Built-in and added column names.
- **Pinned tasks** — Task selections pinned within columns.
- **Browsing choices** — Current search, tag, sort and focus choices.
- **Search history** — Up to five recent nonempty search inputs.
- **Last seen** — The most recent board-presence timestamp.
- **Previous visit** — The preceding last-seen timestamp retained after a sufficiently long absence.
