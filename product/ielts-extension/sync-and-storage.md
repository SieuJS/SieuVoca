# Sync And Storage

## Purpose

Define local-first behavior, connection flow, idempotency, and conflict rules.

## Local-First Behavior

The extension must save locally before attempting network sync. This keeps capture reliable when the user is not logged in or is offline.

Records should be append-only where possible. Later review-page capture can enrich earlier exercise records by matching source URL, quiz id, question number, and local session id.

## Login And Connection

The extension can work without login in local mode.

When the learner connects to the IELTS Study App:
- Existing local records are queued for sync.
- New records auto-sync in the background.
- The popup/sidebar shows sync status.
- A session-end summary appears after a result/review page is captured.

For anonymous users, the session-end summary should still appear locally and include a soft signup CTA. The CTA should not block local saving.

Completed test storage should follow the same sync model as vocabulary once the learner has opted in. Connected learners with result autosave enabled should not see a per-test storage prompt.

For anonymous learners, the result summary should present a combined connect + enable autosave action, not a standalone remote-save toggle.

## Conflict Handling

Records should use idempotency keys so repeated sync attempts do not create duplicates.

Suggested idempotency key:
- source site
- canonical URL or quiz id
- question number when relevant
- normalized term when relevant
- local created timestamp bucket

If the backend already has a matching record, it should merge missing fields instead of overwriting richer data.

