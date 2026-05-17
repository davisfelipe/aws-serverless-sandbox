---
alwaysApply: true
---

# Development Patterns & Best Practices

As a Node.js and TypeScript backend developer, you must strictly follow these coding patterns in all code generation, editing, and code review processes. Always assume the code is production-grade.

## Core Architectural Principles

- **Always** adhere to SOLID, DRY, KISS, and YAGNI principles.
- **Always** implement Domain-Driven Design (DDD) patterns for core business logic (Domain Layer), separating domain rules from infrastructure.

## Object-Oriented & Structural Patterns

- **Always** use the Dependency Injection (DI) pattern to decouple infrastructure services (e.g., Repositories, Use Cases, Controllers). Avoid hardcoded instantiations of external services.

## Functional Programming Boundaries

- **Limit** Functional Programming (FP) principles exclusively to pure logic, data transformations, and stateless asynchronous streams.
- **Do not** mix FP paradigms inside OOP infrastructure classes (like DI containers or TypeORM/Prisma repositories) where stateful or imperative execution is required.

## Type Safety & Strictness

- **Never** use the `any` type. If the type is truly unknown, use `unknown` and perform type narrowing/guards before operating on the data.
- **Always** define explicit return types for all functions, methods, and Use Cases to prevent unintended type inference and contract breaches.
- **Never** use the non-null assertion operator (`!`) to bypass TypeScript's null safety. **Always** handle `null` or `undefined` explicitly.
- **Always** use `readonly` properties for Data Transfer Objects (DTOs), Domain Entities (unless mutation is controlled via methods), and Value Objects to guarantee immutability.

## Async Programming & Concurrency

- **Always** use `async/await` syntax instead of raw `.then()/.catch()` promise chains to maintain readable code and preserve accurate stack traces.
- **Never** use `async` callbacks inside `Array.prototype.forEach()`. **Always** use `for...of` loops for sequential asynchronous execution, or `Promise.all()` for parallel execution.
- **Always** handle Promise rejections explicitly. Unhandled promise rejections are treated as fatal errors in modern Node.js environments.

## Error Handling & Data Validation

- **Always** validate incoming data at the application boundaries (API requests, SQS messages, Environment Variables) using schema validators (e.g., Zod) before passing data to the Domain layer.
- **Never** throw generic `Error` instances. **Always** define and throw custom exception classes (e.g., `ValidationError`, `InfrastructureError`, `EntityNotFoundError`) to allow precise error handling in upper layers.

## Testing Practices

- **Always** structure tests using the AAA pattern (Arrange, Act, Assert).
- **Always** mock dependencies at the boundaries (e.g., mocking Interface Adapters/Ports). **Never** mock internal domain logic or value objects.
- **Always** ensure that all unit and integration tests execute successfully and pass without errors after any code implementation, refactoring, or modification. **Never** commit or accept code that breaks the existing test suite.
- **Always** maintain a minimum test coverage of 80% on the business logic. Every new feature, use case, or fix must include the necessary tests to meet or exceed this threshold before the implementation is considered complete.
