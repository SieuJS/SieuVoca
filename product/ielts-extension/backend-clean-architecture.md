# Backend Clean Architecture

## Purpose

Define backend layers, microservice boundaries, use cases, and ports.

## Architecture Target

The backend target is microservices, not a modular monolith.

Each service should keep Clean Architecture internally:
- Presentation endpoints adapt transport input.
- Application use cases orchestrate work.
- Domain models own business behavior.
- Infrastructure adapters implement persistence, providers, messaging, and telemetry.

The hard path is accepted intentionally: service contracts, observability, local orchestration, data ownership, and failure handling are MVP architecture concerns, not future cleanup.

## Layers

Domain layer:
- Owns entities, value objects, enums, and domain services.
- Contains no database, HTTP, browser-extension, AI SDK, speech SDK, or third-party API code.
- Uses the product's ubiquitous language directly.

Application layer:
- Owns use cases and ports.
- Coordinates domain objects and persistence/provider interfaces.
- Handles idempotency, authorization checks, sync orchestration, and review scheduling decisions.
- Routes speech/pronunciation assessment through `SpeechAssessmentProvider`.
- Routes AI enrichment through quota and API-key policy.

Infrastructure layer:
- Implements repositories and provider clients.
- Handles database mappings, FreeDictionaryAPI, AI enrichment, translation, speech assessment, telemetry, and DTO conversion.

Presentation layer:
- Exposes endpoints for extension sync and website screens.
- Validates transport payloads and calls application use cases.
- Does not contain business rules.

## Service Boundaries

Identity Profile Service:
- Owns learner identity mapping and extension preferences.
- Key concepts: Learner, Local Profile, Connected Account, Learner Extension Preferences, Learner AI Usage.
- Main use cases: connect extension profile, update result autosave preference, read sync status, update AI access settings.

Practice Capture Service:
- Owns exercise context, practice sessions, result capture, and mistake records.
- Key concepts: Practice Session, Exercise Context, Test Result, Mistake Record, Mistake Tag, Unsure Marker.
- Main use cases: save exercise context, save unsure marker, capture result screen data, store completed test, merge result data into prior context.

Vocabulary Service:
- Owns saved terms and their source context.
- Key concepts: Saved Vocabulary, Term, Phrase, Source Context, Learner Note.
- Main use cases: save highlighted term, attach dictionary entry, link term to exercise context.

Dictionary Service:
- Owns dictionary cache and enrichment.
- Key concepts: Dictionary Entry, Definition, Translation, Pronunciation, Example Sentence, Attribution, Lookup Source.
- Main use cases: lookup dictionary entry, cache FreeDictionaryAPI result, AI-enrich missing fields, return card-ready dictionary data.

Review Service:
- Owns spaced repetition and vocabulary ladder state.
- Key concepts: Review Card, Review Stage, Review Attempt, Due Review, Ease, Interval.
- Main use cases: schedule review, submit recognition result, submit context result, assess pronunciation, promote/demote stage, get due cards.

Dashboard Analytics Service:
- Owns read models for score and mistake patterns.
- Key concepts: Score History, Mistake Pattern, Question Type Breakdown, Part Breakdown, Not Enough Data State.
- Main use cases: get recent scores, get single-session summary, get mistake breakdowns when data volume is sufficient.

Parser Health Service:
- Owns parser telemetry and third-party page health monitoring.
- Key concepts: Parser Version, Parser Event, Parse Outcome, Parser Error Code.
- Main use cases: emit parser event, aggregate parser health, detect markup breakage.

AI Speech Service:
- Owns AI enrichment execution, learner AI access policy enforcement, and speech assessment provider integration.
- Key concepts: Learner AI Usage, AI Quota, Learner API Key Status, Speech Assessment.
- Main use cases: update AI access state, enrich missing dictionary fields, assess pronunciation.

## Application Use Cases

- `ConnectExtensionProfile`
- `UpdateLearnerExtensionPreferences`
- `UpdateLearnerAiAccess`
- `GetExtensionSyncStatus`
- `SaveHighlightedVocabulary`
- `LookupDictionaryCard`
- `SaveExerciseContext`
- `MarkQuestionUnsure`
- `CapturePracticeResult`
- `StoreCompletedTest`
- `MergeResultIntoExerciseContext`
- `GetVocabularyReviewQueue`
- `GetDueReviewCards`
- `SubmitReviewAttempt`
- `PromoteOrDemoteReviewStage`
- `GetScoreDashboard`
- `GetSingleSessionSummary`
- `GetMistakeDashboard`
- `RecordParserHealthEvent`
- `AggregateParserHealth`

Some component-level actions are internal steps of broader use cases, but these names are canonical for implementation planning.

## Cross-Service Events

Initial event contracts:
- `ExtensionProfileConnected`
- `LearnerPreferencesUpdated`
- `HighlightedVocabularySaved`
- `DictionaryEntryResolved`
- `ExerciseContextSaved`
- `PracticeResultCaptured`
- `PracticeResultMerged`
- `ReviewAttemptSubmitted`
- `ReviewStageChanged`
- `ParserHealthEventRecorded`

Events should be versioned. Consumers must tolerate unknown fields and duplicate delivery.

## Ports

Repository ports stay service-local:
- `LearnerPreferencesRepository`
- `LearnerAiUsageRepository`
- `ExerciseContextRepository`
- `PracticeSessionRepository`
- `MistakeRecordRepository`
- `SavedVocabularyRepository`
- `DictionaryEntryRepository`
- `ReviewCardRepository`
- `ParserHealthRepository`

Provider ports:
- `DictionaryProvider`
- `TranslationProvider`
- `AiEnrichmentProvider`
- `SpeechAssessmentProvider`
- `TelemetryProvider`

`SpeechAssessmentProvider` is used by pronunciation-stage review cards. Browser-native speech recognition can be the first adapter, but the application layer should depend only on this port.

`LookupDictionaryCard` must be reachable from both `Extension Sync API` and `Website API`. The extension path is required for highlight-triggered lookups during IELTSOnlineTests practice.

In microservices, `LookupDictionaryCard` is owned by Dictionary Service. Extension Sync API may route directly to Dictionary Service for the immediate card response, while Vocabulary Service stores the learner-owned saved term.

## Dependency Direction

Extension and website call presentation endpoints through an API gateway.

Presentation calls service-owned application use cases.

Application use cases depend on domain models and ports.

Infrastructure implements ports.

Domain depends on nothing outside itself.

Service-to-service calls must not bypass another service's public API or event contract.
