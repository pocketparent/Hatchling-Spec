
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
