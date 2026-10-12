---
{
  "entities": [
    {
      "entity": "account",
      "collects": [
        "Name",
        "Email",
        "Password"
      ]
    }
  ],
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
    }
  ]
}
---

# Sign In

The account-access process takes registration or sign-in input and presents its outcome; it also offers explicit Demo Mode entry.
