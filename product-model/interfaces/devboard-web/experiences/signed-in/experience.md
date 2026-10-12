---
{
  "actors": [
    "developer"
  ],
  "access": "authenticated",
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
  ]
}
---

# Signed in

The Developer uses account credentials for connected task requests. A truthy cached user opens the board; HTTP authentication is checked when a protected request is made, while cached content can remain visible after a failed request.
