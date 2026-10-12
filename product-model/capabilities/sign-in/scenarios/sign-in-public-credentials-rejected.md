---
{
  "kind": "validation",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer submits email and password",
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
      "text": "The submitted credentials do not match a registered identity",
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
      "text": "The Product presents the invalid-credentials response",
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

# Reject credentials that do not match

## Trigger

The Developer submits Email and Password for sign-in.

## Outcome

The invalid email/password response is presented without establishing a new browser credential.
