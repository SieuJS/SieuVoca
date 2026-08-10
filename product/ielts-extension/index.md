# IELTS Extension Documentation Index

## Purpose

This folder is the local source of truth for the IELTS Study App extension MVP. Each file owns one purpose so future design, drawing, implementation planning, and Linear ticket creation can reference stable documents.

## Reading Order

1. [Product Scope](./product-scope.md) - what we are building and not building.
2. [Validation Gates](./validation-gates.md) - assumptions that must be checked before implementation.
3. [System Architecture](./system-architecture.md) - high-level system, hidden concerns, and Linear diagram links.
4. [Backend Clean Architecture](./backend-clean-architecture.md) - layers, services, use cases, and ports.
5. [Microservices Architecture](./microservices-architecture.md) - service ownership, contracts, events, and operations.
6. [Application Dictionary](./application-dictionary.md) - ubiquitous language and domain keywords.
7. [Chrome Extension Design](./chrome-extension-design.md) - content script, popup/sidebar, background service.
8. [Website Experience](./website-experience.md) - vocabulary review, review ladder, dashboard.
9. [Data Model](./data-model.md) - records and fields.
10. [Sync And Storage](./sync-and-storage.md) - local-first behavior, connection, idempotency.
11. [Dictionary And AI](./dictionary-and-ai.md) - cache-first lookup, FreeDictionaryAPI, AI quota, speech assessment.
12. [Risk And Compliance](./risk-and-compliance.md) - copyright, ToS, privacy, parser health.
13. [Testing And Backlog](./testing-and-backlog.md) - tests and MVP sequencing.
14. [Linear References](./linear-references.md) - Linear project and document links.

## Keywords

- `Chrome Extension`
- `IELTSOnlineTests`
- `Practice Session`
- `Exercise Context`
- `Saved Vocabulary`
- `Dictionary Entry`
- `Review Card`
- `Review Stage`
- `Mistake Record`
- `Parser Health`
- `Result Autosave`
- `Clean Architecture`
- `Microservices`
- `FreeDictionaryAPI`
- `SpeechAssessmentProvider`
- `Learner AI Usage`

## Current MVP Summary

Build a Chrome extension companion for IELTSOnlineTests, starting with Listening. The extension helps learners save unknown words, source context, notes, unsure markers, and result data after submission. The website turns saved data into vocabulary review, score history, and mistake dashboards.

The backend should target microservices from the start, with Clean Architecture inside each service and domain language at the center.

## Main Open Blockers

- Capture and inspect a real submitted IELTSOnlineTests result/review page.
- Review IELTSOnlineTests terms/account-risk for read-only extension capture.
- Validate dictionary provider behavior, especially Vietnamese translation coverage.
- Validate speech/pronunciation assessment provider path.
