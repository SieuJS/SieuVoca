# Layering Ideas

## Purpose

Capture how the book's layer ideas map to our Clean Architecture backend.

## Presentation Layer

Idea: Presentation adapts the outside world into application requests. It should not own business rules.

IELTS application:

- `Extension Sync API` accepts extension events and sync payloads.
- `Website API` serves dashboard, review, and account screens.
- Both APIs can call `LookupDictionaryCard`, but neither owns dictionary policy.
- Controllers/routes validate transport shape, authenticate, and call use cases.

Source reference: Chapter 4, "The presentation layer", pages 65-89; "API-only presentation", pages 88-89.

## Application Layer

Idea: Application services orchestrate tasks. They coordinate domain models, repositories, providers, transactions, logging, caching, and exceptions.

IELTS application:

- Use cases such as `SaveHighlightedVocabulary`, `CapturePracticeResult`, and `SubmitReviewAttempt` belong here.
- Idempotency, sync orchestration, authorization checks, and provider fallback order belong here.
- Cache-first dictionary lookup is an application policy that calls `DictionaryEntryRepository` before `DictionaryProvider`.

Source reference: Chapter 5, "Task orchestration", pages 96-99; "Data transfer", pages 99-106; "Implementation facts", pages 106-128.

## Domain Layer

Idea: The domain layer models behavior, not only data.

IELTS application:

- `ReviewCardState` should expose behavior for stage progression and failure tracking.
- `MistakeTag` should be an enum/value object, not arbitrary free text.
- `PracticeSession` should express result completeness and whether mistake details are available.
- `SavedVocabulary` should model review readiness and source context, not just a word string.

Source reference: Chapter 6, "Devising a domain model", pages 138-147; "Treating software anemia", pages 148-149.

## Domain Services

Idea: Domain services are useful when domain behavior does not naturally belong to a single entity or value object.

IELTS application:

- `ReviewStagePolicy` can decide promotion/demotion across review attempts.
- `MistakeTaggingPolicy` can classify visible mistakes from parser output.
- `PracticeResultMergePolicy` can merge result-page data into earlier exercise context.
- Avoid domain services that directly query databases or call AI providers.

Source reference: Chapter 7, "What is a domain service, anyway?", pages 170-173; "Common scenarios for domain services", pages 173-177.

## Infrastructure Layer

Idea: Infrastructure hides persistence and external service complexity from the domain and application layers.

IELTS application:

- Implement repository ports with the chosen database.
- Implement `DictionaryProvider` with FreeDictionaryAPI.
- Implement `AiEnrichmentProvider` with the chosen AI provider.
- Implement `SpeechAssessmentProvider` with browser-native speech first where possible, then a server-side provider if required.
- Implement `TelemetryProvider` for parser health and sync events.

Source reference: Chapter 8, "Responsibilities of the infrastructure layer", pages 190-191; "Implementing the persistence layer", pages 192-208.

## Read Models And CQRS

Idea: Query needs can diverge from write models when dashboards and reporting become important.

IELTS application:

- Keep write models focused on saved vocabulary, exercise context, practice sessions, and review state.
- Build dashboard read models for recent scores, wrong count by test, mistake breakdowns, and parser health aggregates.
- Do not force chart data to be computed from rich domain entities at request time if it becomes slow.

Source reference: Chapter 8, "Introducing command/query separation", pages 208-213.
