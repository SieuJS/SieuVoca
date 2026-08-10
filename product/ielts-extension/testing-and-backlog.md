# Testing And Backlog

## Purpose

Define verification coverage and MVP sequencing.

## Extension Tests

- Capture and inspect a submitted review/result page before building score or mistake dashboard parsing.
- Parse exported IELTSOnlineTests Listening HTML.
- Extract title, URL, quiz id, skill, parts, question numbers, question types, and timestamps.
- Detect answer controls for q_type 6, 8, and 9.
- Save highlighted vocabulary with context.
- Mark unsure question.
- Persist local records.
- Queue records for sync.
- Emit parser-health events on success and failure paths.
- Do not show a completed-test storage prompt to a connected learner with `resultAutosaveEnabled=true` on repeated result captures.
- Show a combined connect + enable autosave CTA for anonymous learners on result summary.

## Backend Tests

- Accept idempotent vocabulary sync.
- Accept idempotent exercise context sync.
- Check dictionary cache before calling FreeDictionaryAPI.
- Store external/AI-enriched dictionary entries for future cache hits.
- Accept practice session and mistake records.
- Merge later result data into earlier exercise records.
- Reject unauthenticated sync for remote persistence.
- Verify each service owns its persistence boundary.
- Verify public API contracts between gateway, Extension Sync API, Website API, and services.
- Verify event contracts for vocabulary saved, practice result captured, review attempt submitted, and parser health recorded.
- Verify duplicate event delivery does not create duplicate records.
- Verify service-to-service timeout, retry, and fallback behavior for Dictionary Service and AI Speech Service.

## Website Tests

- Show synced vocabulary in review queue.
- Run recognition review.
- Schedule next review based on self-rating.
- Promote and demote review stages according to the defined ladder rules.
- Show score dashboard from practice session data.
- Show mistake breakdown by question type and part.
- Show "not enough data yet" for pattern widgets before enough sessions exist.

## MVP Backlog

1. Capture and inspect a real submitted IELTSOnlineTests Listening review/result page.
2. Review IELTSOnlineTests terms/account-risk for read-only extension capture.
3. Validate backend-proxied FreeDictionaryAPI, cache-first lookup, and fallback enrichment.
4. Validate speech assessment provider path.
5. Microservice local orchestration, gateway, health checks, logs, tracing, and contract-test skeleton.
6. Extension manifest and IELTSOnlineTests content script.
7. Page parser for logged-in Listening practice pages.
8. Parser-health event model.
9. Local storage model and sync queue.
10. Highlight-to-dictionary card with raw-save fallback.
11. Save vocabulary and exercise context.
12. Unsure question marker.
13. Backend sync endpoints across the service map.
14. Website vocabulary list and recognition review.
15. Review scheduling and stage promotion state.
16. Extension session-end summary with anonymous signup CTA.
17. Result/review page parser for score and mistakes, if validation passes.
18. Score dashboard single-session widgets.
19. Mistake pattern dashboard widgets, after enough captured data exists.
