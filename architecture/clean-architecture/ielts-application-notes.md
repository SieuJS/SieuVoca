# IELTS Application Notes

## Purpose

Translate the Clean Architecture ideas into concrete direction for the IELTS Study App extension MVP.

## Recommended Backend Shape

Use microservices for the first backend.

Why:

- The project goal now includes learning and practicing the harder distributed architecture path.
- Bounded components are already named clearly enough to become service candidates.
- External volatility is high: IELTSOnlineTests parsing, dictionary providers, AI enrichment, speech assessment, and analytics all benefit from explicit service ownership.
- Clean Architecture can still keep each service internally understandable.

Source reference: Chapter 9, "Microservices versus modular monoliths", pages 219-253.

## Service Boundaries

Use these initial services:

- Identity Profile Service
- Practice Capture Service
- Vocabulary Service
- Dictionary Service
- Review Service
- Dashboard Analytics Service
- Parser Health Service
- AI Speech Service

Implementation rule: each service should expose application use cases through public APIs/events and own its persistence boundary. Other services should not reach into its database internals.

Source reference: Chapter 2, "The bounded context", pages 36-41; Chapter 3, "Applying modularization", pages 51-52.

## Presentation Split

Keep two presentation APIs:

- `Extension Sync API`
- `Website API`

Both APIs route to service-owned application use cases. Dictionary lookup from highlighted text must be reachable through `Extension Sync API` because that interaction starts on IELTSOnlineTests pages.

Source reference: Chapter 4, "Boundaries and deployment of the presentation layer", pages 79-82; "API-only presentation", pages 88-89.

## Application Use Cases

Keep the canonical use-case list as the planning unit. Treat each use case as a task-oriented application service.

High-priority examples:

- `SaveHighlightedVocabulary`
- `LookupDictionaryCard`
- `SaveExerciseContext`
- `CapturePracticeResult`
- `StoreCompletedTest`
- `MergeResultIntoExerciseContext`
- `SubmitReviewAttempt`
- `PromoteOrDemoteReviewStage`
- `RecordParserHealthEvent`
- `AggregateParserHealth`

Source reference: Chapter 5, "Task orchestration", pages 96-99; "Outline of an application layer", pages 106-110.

## Domain Behavior To Keep Out Of Controllers

Do not place these decisions in route handlers:

- Review stage promotion and demotion.
- Mistake tag classification.
- Practice result merge rules.
- Dictionary lookup fallback order.
- Result autosave decision rules.
- Parser-health aggregation meaning.

Source reference: Chapter 5, "Task orchestration", pages 96-99; Chapter 6, "Devising a domain model", pages 138-147.

## Provider Ports

Keep these provider boundaries explicit:

- `DictionaryProvider`
- `TranslationProvider`
- `AiEnrichmentProvider`
- `SpeechAssessmentProvider`
- `TelemetryProvider`

Why:

- They isolate external volatility.
- They keep provider SDKs out of the domain.
- They make tests possible without real network calls.
- They allow fallback behavior when quota, latency, browser support, or downstream service availability fails.

Source reference: Chapter 8, "Responsibilities of the infrastructure layer", pages 190-191; Chapter 3, "Designing for testability", pages 58-60.

## Dashboard Read Models

Dashboard analytics should use service-owned read models fed by events where possible.

Candidate read models:

- Recent Listening scores.
- Wrong count by test.
- Mistake breakdown by question type.
- Mistake breakdown by Listening part.
- Parser health by parser version and page type.

Source reference: Chapter 8, "Introducing command/query separation", pages 208-213.

## MVP Risk Gates

Keep these gates explicit before implementation depends on them:

- Submitted review/result page capture.
- IELTSOnlineTests terms/account-risk check.
- Backend-proxied FreeDictionaryAPI behavior.
- Speech assessment provider viability.

Source reference: Chapter 4, "Business requirements engineering", pages 74-79; Chapter 11, "Debt amplifiers", pages 290-293.

## Design Consequences

- Prefer stable domain language over generic service names.
- Keep local-first extension storage as an edge concern, not a domain persistence model.
- Keep parser DTOs separate from domain entities.
- Use idempotency keys in application use cases, not controller-only code.
- Treat parser failures as product telemetry, not only local console errors.
- Treat microservice contracts as first-class deliverables.
- Add local orchestration, health checks, logs, tracing, retries, and contract tests to MVP architecture.
- Do not share domain models or writable database tables across services.

Source reference: Chapter 1, "Clean architecture", pages 18-20; Chapter 9, "Facts about microservices", pages 224-235; "From modules to microservices", pages 249-253.
