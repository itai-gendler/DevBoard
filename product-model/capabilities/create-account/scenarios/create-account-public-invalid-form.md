---
{
  "kind": "validation",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer submits the registration fields",
      "kind": "actor",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::sign-in"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The submitted input fails the client field checks",
      "kind": "condition",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::sign-in"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product presents the input error without submitting registration",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::public::sign-in"
        }
      },
      "actor": "developer"
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
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/middleware/auth.js#protect"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/auth.js#generateToken"
    }
  ]
}
---

# Reject invalid account-access input

## Trigger

The Developer submits Name, Email and Password for registration.

## Outcome

The client refuses submission and keeps the account-access process open with its error.

## Edge cases

- Email must contain an at-sign and password must have at least six characters.
- Registration additionally requires a nonblank trimmed name.
