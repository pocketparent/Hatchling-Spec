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

### **File: 05_wireframes.md**
```markdown
# 05 – UX Wireframes

## Journal View:
- **Layout:** A chat-style feed displaying memory entries chronologically, with date markers.
- **Elements:** Entry cards showing:
  - Author icon/initial
  - Timestamp (displayed in user-local time)
  - Tags (e.g., Milestone, Funny, Smiley)
  - Privacy icon (lock for private, shared indicator, etc.)
  - A preview of content (text and media thumbnail)
- **Interactions:** Tapping a photo enlarges it; tapping an edit icon opens the Entry Modal.
- **Empty State:** "When a moment feels worth saving, text it to Hatchling. We'll hold onto it for you!"

## Entry Modal (Edit View):
- **Fields:** Editable text, tags (AI-suggested and custom), date selector, privacy toggle.
- **Media Display:** Shows a thumbnail if an entry has photo/video; tapping expands to full view.
- **Actions:** Auto-save or explicit “Save” button; Delete with confirmation prompt.

## SMS Confirmation Flow:
- **Inbound SMS:** User sends text, photo, voice, or video.
- **System Response:** Natural, friendly confirmation (e.g., "Added to your memory jar 🍃"), with contextual prompts (if media sent with no caption, ask "Want to add a note?").
- **Fallback/Error:** Unrecognized or garbled messages are saved and flagged as uncategorized.

## Settings / Profile:
- Breaks down into sections: Account Info, Caregivers, Notifications, Privacy, Export & Backup, and Help.
- Designed with a minimalist, calming interface following our UI style guide.
