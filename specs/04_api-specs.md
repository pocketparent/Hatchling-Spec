# 04 – API Specs

## POST /entry
**Purpose:** Create a new memory entry from SMS or app.
**Request Body (application/json):**
```json
{
  "content": "Mari tried avocado today and made a face like we poisoned her 😂",
  "media_url": "https://cdn.hatchling.ai/uploads/photo123.jpg",
  "author_id": "user_12345",
  "source_type": "sms",
  "timestamp_created": "2025-04-11T18:04:00Z",
  "date_of_memory": "2025-04-11",
  "tags": ["Funny", "Food", "Milestone"],
  "privacy": "private",
  "transcription": null
}
Response:

json
Copy
{
  "entry_id": "entry_abc123",
  "status": "created"
}
GET /entries
Purpose: Retrieve entries by journal. Query Parameters:

journal_id (required)

tag, author_id, sort (optional; sort values: "asc", "desc") Response (sample):

json
Copy
[
  {
    "entry_id": "entry_abc123",
    "content": "Mari tried avocado today...",
    "media_url": "https://...",
    "transcription": null,
    "tags": ["Funny", "Food"],
    "date_of_memory": "2025-04-11",
    "timestamp_created": "2025-04-11T18:04:00Z",
    "author": { "name": "Diana", "avatar": "D" },
    "privacy": "private",
    "source_type": "sms"
  }
]
PATCH /entry/{id}
Purpose: Update an existing entry. Request Body (application/json):

json
Copy
{
  "tags": ["Milestone", "Sweet Moment"],
  "date_of_memory": "2025-04-10",
  "privacy": "shared",
  "content": "Mari said 'dada' for the first time!",
  "transcription": null
}
Response:

json
Copy
{
  "entry_id": "entry_abc123",
  "status": "updated"
}
DELETE /entry/{id}
Purpose: Soft-delete an entry. Response:

json
Copy
{
  "entry_id": "entry_abc123",
  "status": "deleted"
}
Error Handling & Recovery:
Invalid Media: Stored with tag "unsupported" and notifies user optionally.

Transcription Failures: Leaves transcription as null with a fallback note "[No transcription available]".

Expired Magic Links: Redirect to a prompt to request a new link.

Rate Limiting: Max 20 SMS per hour per user; media size capped at 15MB per message.

sql
Copy

---
