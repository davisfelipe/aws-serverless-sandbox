---
alwaysApply: true
---

# Development Patterns & Best Practices

As a Node.js and TypeScript backend developer, you must strictly follow these coding patterns in all code generation, editing, and code review processes. Assume all code is production-grade.

## Core Architectural Principles

- **Always** enforce SOLID, DRY, KISS, and YAGNI principles continuously.
- **Always** implement Domain-Driven Design (DDD) to isolate core business rules within the Domain Layer, strictly decoupled from infrastructure.

## Clean Architecture Layering & Strict Directory Structure

- **Always** maintain strict logical and physical separation between the Domain and Application layers.
- **Never** place application orchestration logic or Use Cases inside the Domain directory.
- **Always** restrict the Domain directory exclusively to pure business rules: Entities, Value Objects, Domain Services, Domain Exceptions, and Ports.
- **Always** isolate external integrations, database adapters, API clients, and cloud-specific mechanisms within the Infrastructure directory.
- **Always** confine all execution entry points to the Handlers directory. Handlers must strictly parse incoming events, delegate to Use Cases, and format responses.

## Naming Conventions

- **Always** enforce PascalCase for all TypeScript file names.
- **Always** align the file name exactly with the primary exported class, interface, or function.
- **Never** append redundant technical suffixes to file names. Rely strictly on the directory hierarchy to provide architectural context.
- **Always** utilize ubiquitous language for domain components, rejecting generic technical terminology.

## Object-Oriented & Structural Patterns

- **Always** apply the Dependency Injection (DI) pattern to decouple components.
- **Never** utilize hardcoded instantiations for external dependencies or infrastructure services.

## Functional Programming Boundaries

- **Limit** Functional Programming (FP) paradigms exclusively to pure logic, data transformations, and stateless asynchronous streams.
- **Never** mix FP paradigms within Object-Oriented infrastructure components that inherently require stateful or imperative execution.

## Type Safety & Strictness

- **Never** use the `any` type. Utilize `unknown` paired with strict type narrowing for unverified data.
- **Always** mandate explicit return types for all functions, methods, and Use Cases to prevent unintended type inference.
- **Never** utilize the non-null assertion operator. Handle null or undefined values explicitly and safely.
- **Always** enforce immutability using `readonly` properties for Data Transfer Objects, Domain Entities, and Value Objects.

## Async Programming & Concurrency

- **Always** mandate `async/await` syntax over raw promise chains to ensure readability and preserve stack traces.
- **Never** utilize asynchronous callbacks within sequential array iterations. Utilize `for...of` loops for sequential execution or `Promise.all` for parallel execution.
- **Always** enforce explicit handling of Promise rejections to prevent fatal runtime terminations.

## Error Handling & Data Validation

- **Always** enforce strict schema validation on all incoming data at the application boundaries prior to Domain layer ingestion.
- **Never** throw generic Error instances. Mandate the creation and utilization of specific, custom exception classes for precise error propagation.

## Testing Practices

- **Always** structure tests according to the Arrange, Act, Assert (AAA) pattern.
- **Always** confine mocking exclusively to architectural boundaries.
- **Never** mock internal domain logic or value objects.
- **Always** mandate that the entire test suite executes successfully following any codebase modification. Reject any code introducing failing tests.
- **Always** enforce a minimum test coverage threshold of 80% specifically targeting business logic. Mandate corresponding tests for all new code prior to acceptance.