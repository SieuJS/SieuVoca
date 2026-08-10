# DDD And Language Ideas

## Purpose

Capture DDD and language ideas that should shape our product vocabulary, domain model, tickets, and API contracts.

## Idea Catalog

### Domain Language Before Technical Names

Idea: The system should be named around the learner's real workflow before technical implementation terms.

Why it matters: If the language is wrong, classes and use cases become generic and ambiguous. Later design discussions become harder because people use different terms for the same concept.

IELTS application: Keep terms like `Saved Vocabulary`, `Exercise Context`, `Practice Session`, `Mistake Record`, `Review Card`, and `Parser Health` as first-class names in code and tickets.

Source reference: Chapter 2, "Ubiquitous language", pages 29-36; "Building the glossary", pages 31-32.

### Glossary As A Living Architecture Asset

Idea: A glossary is not just documentation. It becomes the shared vocabulary for requirements, code, tests, and conversations.

Why it matters: A small product can survive informal language early, but the cost appears when implementation starts and different teams create different names for the same thing.

IELTS application: Keep [Application Dictionary](../../product/ielts-extension/application-dictionary.md) and Mintlify's Application Dictionary in sync with Linear tickets and backend class names.

Source reference: Chapter 2, "Building the glossary", pages 31-32; "Keeping business and code in sync", pages 33-35.

### Bounded Contexts Control Ambiguity

Idea: A term can mean different things in different parts of the product. Bounded contexts make the meaning explicit.

Why it matters: Without boundaries, a single overloaded model grows until unrelated behaviors leak into each other.

IELTS application: `Practice Session` belongs to Practice Capture, while `Review Attempt` belongs to Review Engine. They both involve learner answers, but they should not be represented by the same model.

Source reference: Chapter 2, "The bounded context", pages 36-41.

### Context Maps Show Relationship, Not Just Boxes

Idea: The architecture should show upstream/downstream relationships between contexts and external systems.

Why it matters: A static component list misses dependency risk. The important question is who owns meaning and who adapts to whom.

IELTS application: IELTSOnlineTests is upstream for page structure. Our extension should protect the backend through parser DTOs and parser-health telemetry, instead of letting third-party DOM assumptions spread into the domain.

Source reference: Chapter 2, "The context map", pages 42-44; Chapter 4, "The abstract context map", pages 68-71.

### Strategic Design Before Tactical Design

Idea: First decide the business boundaries and language, then decide entities, value objects, repositories, and services.

Why it matters: Tactical patterns can make the code look clean while still modeling the wrong business split.

IELTS application: Keep the bounded components stable first: Learner Profile, Practice Capture, Vocabulary Capture, Dictionary Knowledge, Review Engine, Dashboard Analytics, and Parser Health.

Source reference: Chapter 2, "Strategic analysis", pages 24-26; "Tactical design", pages 26-27.
