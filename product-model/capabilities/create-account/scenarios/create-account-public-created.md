---
{
  "kind": "primary",
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
      "text": "The Product creates an Account from the submitted fields",
      "kind": "product",
      "entities": [
        {
          "entity": "account",
          "effect": "creates",
          "facts": [
            "Name",
            "Email",
            "Password"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::public::sign-in"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product establishes the browser credential and carries the Developer toward the connected board",
      "kind": "product",
      "entities": [
        {
          "entity": "account",
          "effect": "reads",
          "facts": [
            "Name",
            "Email"
          ]
        }
      ],
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

# Register and establish connected access

## Trigger

The Developer submits Name, Email and Password for registration.

## Outcome

Registration succeeds, an account credential is retained in the browser, and the connected board is the destination. Subsequent board browsing is the start-with-account Journey.

## Edge cases

- The browser trims name and email; storage declares lowercased unique email and hashes the credential.
- A pre-existing task cache is not cleared before the board fetch.
