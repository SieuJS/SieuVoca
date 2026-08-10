# Testing And Debt Ideas

## Purpose

Capture ideas about testability, technical debt, and technical credit that should shape MVP sequencing.

## Idea Catalog

### Testability Is A Design Constraint

Idea: Testability should influence structure, not be bolted on after implementation.

Why it matters: A clean architecture that cannot be tested without browsers, databases, and external APIs will slow every change.

IELTS application: Parser behavior, dictionary fallback policy, review-stage promotion, result autosave, and idempotent sync should be testable without running Chrome or calling real providers.

Source reference: Chapter 3, "Testability", page 50; "Designing for testability", pages 58-60.

### Validation Gates Prevent Load-Bearing Guesswork

Idea: Architecture should expose assumptions that can break the product.

Why it matters: A missing validation step can make later design look complete while depending on data that may not exist.

IELTS application: The review/result page capture gate must remain before score and mistake dashboard implementation.

Source reference: Chapter 4, "Business requirements engineering", pages 74-79; Chapter 11, "Debt amplifiers", pages 290-293.

### Technical Debt Is Sometimes Rational, But Must Be Tracked

Idea: Shortcuts can be a business decision, but unmanaged shortcuts compound.

Why it matters: The problem is not every shortcut. The problem is hidden shortcuts with no owner, no repayment plan, and no boundary.

IELTS application: If result parsing starts with a narrow IELTSOnlineTests selector set, record parser version, failure codes, and known unsupported page variants.

Source reference: Chapter 11, "The hidden cost of technical debt", pages 285-293.

### Technical Credit Comes From Small Correct Moves

Idea: Refactoring, clear names, tests, and simple boundaries create credit that makes future change cheaper.

Why it matters: A product with technical credit can make pragmatic tradeoffs without collapsing under its own complexity.

IELTS application: The application dictionary, fixed mistake tag enum, canonical use-case list, parser health events, and provider ports are technical-credit moves for this MVP.

Source reference: Chapter 11, "The hidden profit of technical credit", pages 293-299; "The power of refactoring", pages 295-297.

### Debt Amplifiers Matter More Than Individual Shortcuts

Idea: Lack of documentation, missing skills, rapid prototypes, and scope creep amplify technical debt.

Why it matters: These risks turn small local shortcuts into system-wide confusion.

IELTS application: Keep the split docs, Linear references, and Mintlify docs aligned. Do not let extension, backend, and website teams invent separate names or contracts.

Source reference: Chapter 11, "Debt amplifiers", pages 290-293.
