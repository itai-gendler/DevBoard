---
{
  "kind": "edge",
  "routes": {
    "web": "Web"
  },
  "steps": [
    {
      "text": "The Developer requests tags for the selected Code Snippet",
      "kind": "actor",
      "entities": [
        {
          "entity": "code-snippet",
          "effect": "reads",
          "facts": [
            "Code"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product sends the selected Code Snippet content to Gemini",
      "kind": "product",
      "entities": [
        {
          "entity": "code-snippet",
          "effect": "reads",
          "facts": [
            "Code"
          ]
        }
      ],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The generation request fails or rejects unusable code",
      "kind": "condition",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    },
    {
      "text": "The Product logs failure and retains existing suggestions",
      "kind": "product",
      "entities": [],
      "contexts": {
        "web": {
          "place": "devboard-web::signed-in::board"
        }
      },
      "actor": "developer"
    }
  ],
  "references": [
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/server/routes/ai.js:7-95"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/hooks/useSuggestTags.jsx#useSuggestTags"
    },
    {
      "kind": "code",
      "role": "implementation",
      "target": "devboard/client/src/components/Board/TaskCard.jsx#TaskCard"
    }
  ]
}
---

# Retain prior suggestions after generation failure

## Trigger

The Developer requests tags for the selected code block.

## Outcome

Failure is console-only, loading ends, prior suggestions can remain and no tag write is initiated.

## Edge cases

- Blank or whitespace-only code is rejected by the tag endpoint.
- The prompt requests two or three tags, but normalization can yield fewer or none.
- Existing task tags are not changed until selection.
