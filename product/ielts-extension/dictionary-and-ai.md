# Dictionary And AI

## Purpose

Define dictionary lookup, AI enrichment, AI quota, and speech assessment behavior.

## Dictionary Lookup Policy

Lookup order:
1. Search our cached dictionary database.
2. Search FreeDictionaryAPI through the backend on cache miss.
3. Use AI to generate missing meaning, Vietnamese translation, example, or pronunciation guidance.
4. Store external and AI-enriched results in our database for future reuse.

FreeDictionaryAPI calls should be proxied through our backend, not made directly from the extension.

Because the 1,000 requests/hour/IP limit would apply to the backend IP, cache-first lookup is a hard requirement before launch.

Stored entries based on FreeDictionaryAPI/Wiktionary should keep source and attribution metadata.

If provider latency or rate limits are poor, the extension should still allow saving the raw term and source context, then enrich the record later on the website.

## AI Access Model

Selected model: hybrid.

The app provides a small free AI quota for a smooth first-time experience. Advanced or heavy AI features support the learner's own API key.

Raw learner API keys must be stored only in the secure secret mechanism chosen by implementation, not in ordinary domain tables or logs.

## Speech Assessment

Pronunciation assessment should use the `SpeechAssessmentProvider` port.

Candidate path:
- Validate browser Web Speech API first for MVP speech-to-text.
- Add a server-side speech-to-text or pronunciation assessment adapter if browser support is not enough.
- If speech assessment is unavailable, pronunciation review can fall back to manual self-rating.

