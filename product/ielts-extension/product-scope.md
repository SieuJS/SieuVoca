# Product Scope

## Purpose

Define the product slice for the IELTS Study App extension MVP.

## Context

The IELTS Study App MVP is practice-first, starting with Listening. Instead of importing IELTSOnlineTests content into our app, the product supports the learner while they practice on IELTSOnlineTests.

The first build is a Chrome extension companion plus a website knowledge hub.

## Goals

- Build a Chrome extension study assistant for IELTSOnlineTests.
- Let learners highlight unknown words or phrases and save them with context.
- Show an inline dictionary card with English meaning, Vietnamese translation, pronunciation, and example usage.
- Save the current exercise context for personal revision.
- Validate whether IELTSOnlineTests review/result pages expose score and per-question mistake data.
- Capture Listening test score and mistakes from the review/result page only after validation passes.
- Sync extension data to the IELTS Study App knowledge hub.
- Build the first website review experience around vocabulary spaced repetition.
- Build a dashboard for score history and mistake patterns.

## Non-Goals

- Do not give direct answer hints during practice.
- Do not re-host IELTSOnlineTests content as our app's public content library.
- Do not build a full IELTS planner in this slice.
- Do not build tutor workflows in this slice.
- Do not require AI for every dictionary lookup.
- Do not depend on answer keys being available before the learner submits.

## Product Loop

1. Learner opens a Listening exercise on IELTSOnlineTests.
2. Extension detects supported page metadata.
3. Learner highlights an unknown word or phrase.
4. Extension shows a dictionary card.
5. Learner saves the word, optional note, and source context.
6. Extension stores the item locally immediately.
7. If the learner is connected to the app, extension syncs in the background.
8. Learner submits the IELTSOnlineTests exercise.
9. Extension detects the review/result page and reads the visible score where available.
10. If the learner is connected and has enabled result autosave, extension stores/syncs the practice session, score, and visible mistake metadata without a per-test prompt.
11. If the learner is anonymous, extension shows a session summary with a combined connect + enable autosave CTA. If the learner is connected but autosave is disabled, extension shows a one-time "always save my results" setting.
12. Website shows vocabulary review, score history, and mistake patterns.
13. Learner reviews saved words through an automatic ladder.

## Future Work

- Reading support.
- Speaking AI chat practice.
- Writing AI marking and retry loop.
- AI-powered vocabulary enrichment.
- Context recall cards.
- Pronunciation cards.
- Speaking/writing usage cards.
- Weak-area recommendations.
- Planner integration.
- Tutor dashboards.

