# 07 – QA Plan & Acceptance Criteria

## SMS Entry Submission:
- **Works When:** 
  - User sends text, photo, video, or voice; entry appears within 10 seconds.
  - Media is viewable and tagged, text is preserved, voice memos are transcribed.
- **QA Tests:**
  - Send SMS with text only, with photo only, with photo+caption.
  - Test MMS voice (.m4a) and MMS video.
  - Test duplicate messages, garbled inputs, and blank entries.
- **Parent POV:** "I sent a message to Hatchling, and it just showed up."

## Journal View:
- **Works When:** 
  - Entries display chronologically with correct filters (tag, author, privacy).
  - Tapping a photo expands it; search returns accurate results.
- **QA Tests:**
  - Apply filters (by tag, privacy, author).
  - Test "Jump to Date" if implemented.
- **Parent POV:** "It's easy to find what I logged; I can scroll through my journal seamlessly."

## Entry Modal (Edit View):
- **Works When:** 
  - All fields (text, tags, date, privacy) are editable.
  - Changes save automatically or on explicit action; deletion hides the entry (with recovery).
- **QA Tests:**
  - Edit and update fields, verify auto-save or confirmation messages.
  - Delete entries and verify soft deletion behavior.
- **Parent POV:** "I can tweak my memories without stress."

## User Account & Invite Flow:
- **Works When:** 
  - A parent logs in via SMS magic link and creates an account.
  - Co-parents/caregivers join via invite; role-based permissions are enforced.
- **QA Tests:**
  - Test complete login and account creation.
  - Validate invite flows and proper access control (co-parent vs caregiver).
- **Parent POV:** "I got my partner in and we share memories seamlessly."

## Nudges & Reminders:
- **Works When:** 
  - Nudges are sent only to users who opt in, with correct frequency settings.
  - Nudge tone is friendly and contextually appropriate.
- **QA Tests:**
  - Simulate inactivity and verify nudge behavior matches settings.
- **Parent POV:** "I only get nudged when necessary; it feels helpful."

## Export Flow:
- **Works When:** 
  - Users can export journal entries (PDF, CSV, shareable link) with applied filters.
- **QA Tests:**
  - Validate export with date ranges, tags, and author filters.
  - Test for empty journal state.
- **Parent POV:** "Exporting my memories is straightforward and reliable."

## Additional QA:
- **Accessibility:** Ensure screen reader and keyboard accessibility.
- **Error Handling:** Confirm fallback behavior for invalid media, transcription failures, and expired magic links.
- **Analytics Logging:** Verify events (entry created/edited, nudge sent, export triggered) are logged correctly (with anonymization).
