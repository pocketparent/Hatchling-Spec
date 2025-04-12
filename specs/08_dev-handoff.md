# 08 – Developer Handoff & Infrastructure Notes

## Infrastructure & Deployment:
- **Hosting:** Use Render for backend and frontend deployment.
  - Manus should set up a Dockerized or Flask deployment environment as needed.
- **Environment Variables:** Populate the provided `.env.template` with secrets; do not commit real keys.
- **Versioning:** Use GitHub for spec files and source code (repository link provided).

## API & Backend:
- Follow API specs in `04_api-specs.md` for endpoints: `/entry`, `/user`, `/journal`, `/auth`, `/invite`.
- All endpoints require authentication (JWT-based) except for SMS ingestion.
- **Error Handling:** Must handle invalid media, transcription errors, and expired magic links as defined.

## External Services:
- **Firebase:** Use for authentication, Firestore (data store), and Storage (media uploads); service account key must be integrated.
- **Stripe:** Integrate Stripe Checkout for subscriptions with a 14-day free trial. Handle webhooks for subscription events via `/stripe/webhook`.
- **Twilio:** Route incoming SMS and MMS to `/entry` endpoint; handle outbound messaging for magic links and nudges.
- **OpenAI:** Configure for voice transcription (Whisper) and AI tag suggestions.

## Security & Rate Limiting:
- Implement rate limiting: maximum 20 SMS per hour per user, with media size capped at 15MB.
- Sensitive keys are managed via environment variables and not committed to GitHub.

## Developer Deliverables:
- Complete API integration as per the specs.
- Frontend UI should match wireframes in `05_wireframes.md` and the style guide in `06_ui-style-guide.md`.
- Implement QA tests as defined in `07_qa-plan.md`.
- Ensure proper logging and error fallback behavior.
- Provide documentation for any deviations from the specs.

## Communication:
- If any ambiguity arises, refer to this full spec document.
- Document any assumptions or changes for review.
