# Clean Architecture Notes Index

## Purpose

This folder captures derived architecture ideas from `crawl/clean-architecture.txt` and maps them to the IELTS Study App backend and extension design.

These notes are not a replacement for the book. They are a working idea catalog: short interpretations, source pointers, and concrete implications for our system.

## Source

- Book: `Clean Architecture with .NET`
- Author: Dino Esposito
- Local extracted source: `crawl/clean-architecture.txt`
- Source PDF/text is copyrighted. Keep these notes as summaries and do not copy long passages into product docs.

## Files

- [Source Map](./source-map.md) - chapter, section, and page references.
- [DDD And Language](./ddd-and-language.md) - ubiquitous language, bounded contexts, and context maps.
- [Modularity](./modularity.md) - modularity principles, microservices, and dependency direction.
- [Layering](./layering.md) - presentation, application, domain, domain service, and infrastructure layer ideas.
- [Testing And Debt](./testing-and-debt.md) - testability, technical debt, and technical credit.
- [IELTS Application Notes](./ielts-application-notes.md) - direct application to the IELTS Study App.

## How To Use

Use this folder when deciding:

- Which backend component owns a behavior.
- Whether a concept belongs in domain, application, infrastructure, or presentation.
- How to name use cases, entities, services, ports, and DTOs.
- How to keep microservice boundaries clean.
- Which architecture risks should become validation gates or tests.

## Quick Keywords

- `Ubiquitous Language`
- `Bounded Context`
- `Context Map`
- `Modular Monolith`
- `Presentation Layer`
- `Application Layer`
- `Domain Layer`
- `Domain Service`
- `Infrastructure Layer`
- `Repository`
- `DTO`
- `CQRS`
- `Technical Debt`
- `Technical Credit`
