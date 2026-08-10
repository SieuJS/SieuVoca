# System Architecture

## Purpose

Describe the system-level boundaries and drawing references.

## System Flow

High-level flow:

`Chrome Extension -> API Gateway -> Extension Sync API -> Service Use Cases -> Service Domain -> Repository/Provider Ports -> Infrastructure`

Website flow:

`Website -> API Gateway -> Website API -> Service Use Cases -> Service Domain -> Repository/Provider Ports -> Infrastructure`

Extension-triggered dictionary lookups use `Extension Sync API`, not `Website API`, because the learner highlights words while practicing in the extension. Website review screens may also request dictionary data through `Website API`, but both presentation APIs must be able to reach `LookupDictionaryCard`.

The backend target is microservices. Each bounded component should become an independently deployable service or a clearly owned service candidate. Clean Architecture still applies inside every service.

Initial service map:
- `Identity Profile Service`
- `Practice Capture Service`
- `Vocabulary Service`
- `Dictionary Service`
- `Review Service`
- `Dashboard Analytics Service`
- `Parser Health Service`
- `AI Speech Service`

Synchronous calls should be reserved for user-facing reads and immediate command responses. Cross-service propagation should prefer events for result captured, vocabulary saved, review attempted, parser health recorded, and dictionary entry enriched.

## Hidden Concerns To Show In Architecture

- Anonymous local profile vs connected account.
- Local-first storage and sync queue.
- Result autosave preference.
- Parser health telemetry.
- Review-page validation gate.
- Cache-first dictionary lookup.
- FreeDictionaryAPI attribution.
- AI fallback and quota/API-key state.
- Speech assessment.
- Service ownership and cross-service contracts.
- Observability, tracing, and service health.
- Terms/account-risk gate.
- Private revision boundary.

## Linear Diagram Source

Editable Mermaid diagrams are stored in Linear:

`https://linear.app/sieu-nguyen/document/system-architecture-diagrams-530ed3444364`

The Linear diagram document includes:
- System Context.
- Clean Architecture Backend.
- Vocabulary Capture and Dictionary Lookup Flow.
- Practice Result Capture Flow.
- Review Ladder Flow.
- Pronunciation Assessment Flow.
- Dashboard Data Availability.

## Risk Gate Note

Terms/account-risk is a product and launch checklist concern, not a bounded component or domain entity.
