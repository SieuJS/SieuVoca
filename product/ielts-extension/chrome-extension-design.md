# Chrome Extension Design

## Purpose

Define the extension-side responsibilities and user-facing behavior.

## Content Script

Runs on supported IELTSOnlineTests pages.

Responsibilities:
- Detect test page type, starting with Listening.
- Read page metadata: title, URL, skill, collection URL, quiz id, duration, part count, question count.
- Detect question metadata: question number, part, question type, visible prompt context, answer control type, and listening timestamp when present.
- Track learner answers where readable from the page.
- Support text selection and show the dictionary card.
- Let learners mark questions as unsure.
- Detect submit/review/result state transitions.
- Extract score and mistake metadata from review pages where available.
- Respect the learner's result autosave setting before storing completed tests remotely.
- Send captured data to the extension background service.

The content script should not inject answer hints or alter the user's answer controls.

## Dictionary Card

Appears when the learner highlights text.

MVP fields:
- Selected word or phrase.
- English meaning.
- Vietnamese translation.
- Pronunciation if available.
- Example sentence.
- Source test and question number.
- Save action.
- Optional learner note.

## Popup Or Sidebar

Shows current session status.

MVP fields:
- Current test title.
- Saved words count.
- Unsure question count.
- Sync status.
- Last sync time.
- Link to website review dashboard.
- Session summary after result page capture.
- Soft signup CTA for anonymous users after a saved word, unsure marker, or result capture.
- One-time result autosave setting: "Always save my results."

## Background Service

Coordinates storage and sync.

Responsibilities:
- Receive events from content scripts.
- Persist local records.
- Manage sync queue.
- Call backend APIs when the learner is connected.
- Retry failed syncs safely.
- Track sync status per record.

