# Microservices Architecture

## Purpose

Define the microservice-first architecture direction for the IELTS Study App backend.

## Decision

The backend should be built as microservices from the start.

This is intentionally harder than a modular monolith. The product will pay the complexity cost early so the architecture practice, service boundaries, deployment model, and observability are real from day one.

Clean Architecture still applies inside each service.

## Service Map

Identity Profile Service:
- Owns learner identity mapping, connected account state, extension preferences, result autosave, and AI access state.
- Publishes learner preference and profile connection events.

Practice Capture Service:
- Owns exercise context, practice sessions, result capture, mistake records, and unsure markers.
- Publishes exercise-context and practice-result events.

Vocabulary Service:
- Owns saved vocabulary, learner notes, source context links, and vocabulary-to-exercise relationships.
- Calls Dictionary Service for card-ready dictionary data.
- Publishes vocabulary-saved events.

Dictionary Service:
- Owns reusable dictionary entries, cache-first lookup, FreeDictionaryAPI integration, attribution, and AI enrichment requests.
- Publishes dictionary-entry-resolved events.

Review Service:
- Owns review cards, spaced repetition, review attempts, review-stage promotion, and due-card queues.
- Consumes vocabulary-saved and dictionary-entry-resolved events.
- Publishes review-attempt and review-stage-changed events.

Dashboard Analytics Service:
- Owns read models for score history, single-session summaries, mistake trends, and not-enough-data states.
- Consumes practice-result, mistake, unsure-marker, and review events.

Parser Health Service:
- Owns parser telemetry ingestion, parser version health, failure aggregation, and markup-breakage detection.
- Consumes parser-health events from the extension sync flow.

AI Speech Service:
- Owns AI quota enforcement, learner API-key status usage, AI enrichment execution, and speech assessment provider integration.
- Exposes provider-backed capabilities to Dictionary Service and Review Service.

## API Entry Points

Use an API gateway or backend-for-frontend edge to expose:
- `Extension Sync API`
- `Website API`

The gateway should handle:
- Authentication and session context forwarding.
- Request routing.
- Correlation IDs.
- Basic rate limiting.
- Transport-level validation.

Business rules remain inside service application layers.

## Communication Rules

Use synchronous calls for:
- Immediate dictionary card lookup.
- Current sync status.
- Dashboard reads.
- Due review queue reads.
- Commands where the user needs immediate success or failure.

Use events for:
- Vocabulary saved.
- Dictionary entry resolved.
- Exercise context saved.
- Practice result captured.
- Practice result merged.
- Review attempt submitted.
- Review stage changed.
- Parser health event recorded.

Events should be idempotent, versioned, and safe for duplicate delivery.

## Data Ownership

Each service owns its persistence tables or schema.

Do not share writable database tables across services.

Read models may duplicate data through events when needed for dashboard performance.

## MVP Operational Requirements

Because microservices are the chosen path, the MVP needs these from the beginning:
- Local orchestration for all services.
- Per-service health checks.
- Structured logs with correlation IDs.
- Basic distributed tracing.
- Service-to-service timeout and retry policy.
- Dead-letter or failed-event handling.
- Contract tests for public APIs and events.
- Seed data for local development.

## Main Risks

Operational overhead:
- More services mean more local dev, deployment, and debugging work.

Boundary mistakes:
- If boundaries are wrong, network contracts make refactoring harder.

Data consistency:
- Cross-service workflows need idempotency and eventual-consistency rules.

Testing cost:
- Unit tests are not enough. Contract and integration tests become mandatory.

## Guardrails

- Keep service count small and tied to real bounded contexts.
- Do not split a service only because a class is large.
- Every service must have a clear owner, database boundary, public API, and event contract.
- Shared code must be boring: primitives, auth helpers, observability helpers, and contract types only.
- Domain models are not shared packages.

## Source Reference

This direction intentionally chooses the harder path discussed in `Clean Architecture with .NET`, Chapter 9, "Microservices versus modular monoliths", pages 219-253.

The notes in [Modularity Ideas](../../architecture/clean-architecture/modularity.md) and [IELTS Application Notes](../../architecture/clean-architecture/ielts-application-notes.md) record the tradeoff.
