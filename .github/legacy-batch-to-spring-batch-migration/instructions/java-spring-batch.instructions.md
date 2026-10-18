---
description: Java and Spring Batch development standards
applyTo: "**/*.java"
---

# Java & Spring Batch Standards

## 1. General Java Standards

- Use Java 17 and Spring Boot 3.x.
- Follow SOLID and Clean Code principles.
- Apply appropriate design patterns only when necessary.
- Keep implementations simple, maintainable and testable.
- Avoid unnecessary abstractions and code duplication.
- Prefer composition over inheritance unless inheritance is justified.
- Keep methods focused and cyclomatic complexity low.
- Split methods containing excessive conditional logic.
- Design business logic to minimize the impact of future changes.
- Do not introduce unrelated refactoring.

## 2. Naming Conventions

- Classes: UpperCamelCase.
- Methods and variables: lowerCamelCase.
- Constants: UPPER_SNAKE_CASE.
- Packages: lowercase.
- Use meaningful, business-oriented names.
- Avoid ambiguous abbreviations.

## 3. DTO & Entity

- Use Lombok for DTO classes.
- Avoid unnecessary boilerplate code.
- Reuse common fields when their semantics are equivalent.
- Do not introduce inheritance solely because field names match.
- Prefer composition for reusable DTO structures.
- Use appropriate JPA mapping strategies for shared entity fields.
- Avoid inappropriate Lombok annotations on JPA entities.

## 4. Package Structure

<!-- PACKAGE_TREE: TO BE PROVIDED -->

- Follow the defined package structure.
- Do not introduce new packages without architectural justification.
- Provide a concise package-info.java for relevant packages.
- Keep responsibilities separated.

## 5. Constants & Utilities

- Utility classes must have private constructors.
- Group related constants using appropriate nested static classes.
- Avoid duplicated constants.
- Reuse existing utility classes before creating new ones.
- Do not introduce unnecessary utility methods.

## 6. Configuration & Cache

- Access application/business parameters through existing
  classes and methods under the cache package.
- Do not duplicate parameter retrieval logic.
- Avoid unnecessary repeated parameter lookups.
- Follow the template's configuration conventions.

## 7. Thread Safety

- Ensure components are safe for their execution model.
- Avoid mutable shared state in singleton beans.
- Use appropriate scopes for stateful Batch components.
- Do not share non-thread-safe readers or writers across threads.
- Preserve data consistency during concurrent processing.

## 8. Spring Batch Architecture

- Follow the Reader -> Processor -> Writer architecture.
- Use chunk-oriented processing for data processing operations.
- Use ItemProcessor only when transformation or business
  processing is required.
- Allow Reader -> Writer flow when processing is unnecessary.
- Follow existing Job and Step configuration patterns.
- Reuse template components whenever possible.

## Job Scheduling & Orchestration

- All Batch Jobs are triggered and scheduled externally via UC4.
- Each Job must be independently executable.
- Do not implement Job scheduling within the Java application.
- Do not trigger other Jobs programmatically.
- Do not implement inter-Job orchestration or sequencing.
- Do not configure parallel or sequential Job execution in Java.
- Do not introduce @Scheduled or internal scheduling mechanisms.
- Identify inter-Job data dependencies during migration design.
- Document execution prerequisites for UC4 configuration.
- Keep each Job focused on its own business responsibility.

## 9. Reader Standards

- Use JdbcCursorItemReader for database reading.
- Support multiple input files when file reading is required.
- Store SQL queries under:
  src/main/resources/sql/<schema_name>/
- Load SQL statements from resource files.
- Bind SQL parameters safely.
- Do not hardcode SQL statements inside Java classes.

## 10. Processor Standards

- Keep business processing logic in the Processor layer.
- Separate complex business rules into focused components.
- Avoid database DML operations inside processors.
- Keep transformations deterministic where possible.
- Avoid unnecessary stateful processing.

## 11. Writer Standards

- Execute business database DML operations in the Writer layer.
- Store SQL statements under:
  src/main/resources/sql/<schema_name>/
- Use parameter binding for SQL statements.
- Follow template transaction and exception-handling patterns.
- Avoid unnecessary database round trips.
- Preserve business data integrity.

## 12. Performance & Reliability

- Follow the template's chunk-size and transaction conventions.
- Avoid unnecessary database and file operations.
- Ensure resources are properly managed.
- Consider restart behavior and idempotency.
- Do not introduce multithreading or partitioning unless justified.
- Preserve existing business behavior.

## 13. Implementation Principles

- Follow the approved Spring Batch Template architecture.
- Reuse existing components before creating new ones.
- Preserve established logging and exception-handling patterns.
- Keep all implemented code testable.
- Do not make unapproved architectural changes.

## Business Logic Separation

- Keep business rules independent of technical infrastructure.
- Avoid embedding complex business logic directly in
  Reader, Writer or configuration classes.
- Extract reusable business logic into dedicated components.
- Do not create service classes for trivial operations.
- Prefer existing project patterns over new architectural layers.