# 03 – Data Models

## Memory Entry Schema:
- **entry_id:** string (unique internal ID)
- **content:** string (freeform text or voice transcription)
- **media_url:** string (signed URL for photo, video, or voice)
- **transcription:** string or null (if a voice note is auto-transcribed)
- **tags:** array of strings (auto-suggested via AI, user-editable)
- **date_of_memory:** ISO date (user-editable)
- **timestamp_created:** datetime in UTC (internal use)
- **author_id:** string (links to a user profile)
- **privacy:** enum [private, shared, public]
- **source_type:** enum [sms, app, voice]
- **deleted_flag:** boolean (soft delete)
- **journal_id:** string (for multi-child support, future-proofing)

## User Schema:
- **user_id:** string (unique internal key)
- **name:** string
- **phone_number:** string (used for SMS login and display in profile)
- **email:** string or null (optional)
- **avatar:** string (image URL or initials)
- **role:** enum [parent, co_parent, caregiver]
- **permissions:** enum [edit, view]
- **default_privacy:** enum [private, shared, public]
- **nudge_opt_in:** boolean
- **nudge_frequency:** enum [daily, weekly, occasionally]
- **account_created:** datetime (internal)
- **last_active:** datetime (internal)
- **subscription_status:** enum [trial, active, inactive]
- **stripe_customer_id:** string

## Role Permissions Matrix:
| Role       | Log Entries | Edit Entries | View Private | Export | Manage Roles |
|------------|-------------|--------------|--------------|--------|--------------|
| Parent     | ✅          | ✅           | ✅           | ✅     | ✅           |
| Co-Parent  | ✅          | ✅           | ✅           | ✅     | ❌           |
| Caregiver  | Optional    | ❌           | ❌           | ❌     | ❌           |
