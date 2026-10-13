---
{
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/App.jsx#PrivateRoute"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/pages/Login.jsx#handleSubmit"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/context/BoardContext.jsx#BoardProvider"
    }
  ],
  "acts": "external",
  "kind": "person",
  "relations": [
    {
      "entity": "account",
      "verb": "identifies through",
      "cardinality": "one-to-one"
    }
  ]
}
---

# Developer

A person working with tasks, account access and Demo Mode.

## Information kept

- **Browser identity** — The profile and credential the browser holds for the current session: the Demo Mode profile with the demo credential, or the signed-in Account with its issued credential.
