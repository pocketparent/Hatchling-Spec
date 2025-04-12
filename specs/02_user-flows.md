# 02 – User Flows

## Onboarding & Login:
- **SMS Magic Link Flow:** 
  - The user enters their phone number.
  - They receive an SMS with a magic login link (valid for 10 minutes; one-time use).
  - If the number is registered, they log in; if not, they are prompted to create an account.
- **Account Creation (for new users):**
  - Prompt for name, with optional avatar selection.
  - Set default privacy (Private/Shared/Public) and opt in to nudges (frequency: daily, weekly, occasionally).

## Subscription Sign-Up:
- During onboarding, the user is prompted to start a 14-day free trial (with Stripe Checkout for billing).
- Trial-to-paid conversion is handled via Stripe webhooks. Notifications are sent when the trial is nearing its end.

## Entry Submission Flow:
- **SMS or App Entry:** Users send text, photo, voice, or video to Hatchling.
- The backend receives the submission at the `/entry` endpoint.
- AI processing auto-tags the memory (e.g., Milestone, Funny, Smiley).
- The entry is stored with metadata (date of memory, timestamp in UTC, author, and privacy).
- Unparseable or corrupted entries are stored in a holding queue as “uncategorized.”

## Edit Flow:
- Tapping an entry in the Journal View opens an Edit Modal.
- Users can update text, tags, date, and privacy.
- Changes are auto-saved (with a "Changes saved automatically" confirmation).

## Co-Parent / Caregiver Invite Flow:
- The logged-in user can invite a co-parent or caregiver by entering their phone number and selecting a role.
- The invite is sent via SMS with a magic link.
- The invitee then completes a lightweight account creation flow.

## Webhook & Subscription Events:
- A dedicated webhook endpoint (`/stripe/webhook`) handles trial expiration, payment status changes, and subscription updates.
