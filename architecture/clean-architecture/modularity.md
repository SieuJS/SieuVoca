# Modularity Ideas

## Purpose

Capture modularity ideas that should guide the microservice-first backend shape.

## Idea Catalog

### Layers And Tiers Are Not The Same Thing

Idea: A layer is a logical responsibility boundary. A tier is a deployment boundary.

Why it matters: Splitting deployment creates distributed complexity. If we choose it intentionally, each deployed service still needs a clean internal layer model.

IELTS application: Keep presentation, application, domain, and infrastructure separated inside every service.

Source reference: Chapter 1, "Layers, tiers, and modularization", page 7; Chapter 3, "Applying modularization", pages 51-52.

### Microservice-First Is An Intentional Difficulty Choice

Idea: Microservices can support independent ownership and scaling, but they require deployment, observability, data ownership, and communication maturity.

Why it matters: Choosing microservices early is not just a folder split. It changes testing, local development, debugging, data consistency, and failure handling.

IELTS application: Start with a small set of real services tied to bounded contexts: Identity Profile, Practice Capture, Vocabulary, Dictionary, Review, Dashboard Analytics, Parser Health, and AI Speech.

Source reference: Chapter 9, "Facts about microservices", pages 224-235; "Can microservices fit all applications?", pages 235-245; "Modular monoliths", pages 245-253.

### Treat Bounded Contexts As Service Boundaries

Idea: Service boundaries should follow stable business boundaries, not arbitrary technical layers.

Why it matters: Wrong boundaries create chatty service calls and duplicated concepts.

IELTS application: `Practice Session` belongs to Practice Capture Service. `Review Card` belongs to Review Service. `Dictionary Entry` belongs to Dictionary Service. `Learner AI Usage` belongs to Identity Profile Service, while provider execution belongs to AI Speech Service.

Source reference: Chapter 2, "The bounded context", pages 36-41; Chapter 9, "From modules to microservices", pages 249-253.

### Dependency Direction Is The Real Architecture

Idea: Clean boundaries are enforced by dependency direction, not by folder names alone.

Why it matters: If the domain imports HTTP, database, browser, or AI SDK details, the system is clean only on paper.

IELTS application: Domain types should not import Chrome extension DTOs, Prisma models, FreeDictionaryAPI schemas, AI SDK responses, telemetry payloads, or another service's database models.

Source reference: Chapter 1, "Clean architecture", pages 18-20; Chapter 5, "Boundaries and deployment of the application layer", pages 129-131.

### Simplest Solution Still Needs Boundaries

Idea: Simplicity is not a license to mix responsibilities. The simplest solution should remain maintainable and testable.

Why it matters: MVP shortcuts become expensive when they erase the system's core boundaries.

IELTS application: It is acceptable to implement fewer services first only if the service contracts are explicit. It is not acceptable to hide cross-service boundaries inside one controller or shared database.

Source reference: Chapter 3, "The simplest solution ever", pages 56-60.
