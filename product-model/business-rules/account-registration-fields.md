---
{
  "appliesTo": [
    {
      "type": "entity",
      "id": "account",
      "facts": [
        "Name",
        "Email",
        "Password"
      ],
      "effect": "creates"
    },
    {
      "type": "capability-scenario",
      "id": "create-account-public-created",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "create-account-public-invalid-form",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "create-account-public-existing-email",
      "contexts": [
        {
          "place": "devboard-web::public"
        }
      ]
    },
    {
      "type": "capability-scenario",
      "id": "create-account-public-service-failure",
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
      "target": "devboard/server/models/User.js#userSchema"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/auth.js:6-57"
    }
  ]
}
---

# Registration requires its account fields and unique email

Registration requires Name, Email and Password. The client trims name/email, requires an at-sign in email and at least six password characters; storage requires the fields, lowercases email and declares uniqueness. An existing-email response is presented. Credential hashing is internal and the password is not disclosed on the board.
