---
description: 'Code review rules for Java 17 / Spring Boot 3.x sources.'
applyTo: '**/*.java'
---
# Java review
Apply during code review; follow the [shared contract](team-standards.instructions.md).

- J-01: Verify Java 17 and Spring Boot 3.x compatibility against relevant build settings/API usage; report incompatible versions or required Jakarta migrations using concrete usage evidence.
- J-02: Use UpperCamelCase for classes, lowerCamelCase for methods/variables, and UPPER_SNAKE_CASE for constants. Names must express business meaning. Do not unnecessarily rename documented domain abbreviations.
- J-03: DTOs must use appropriate Lombok getters/setters/constructors; report manual boilerplate violations. For entities, check Lombok equals/hashCode/toString effects on lazy relationships, recursion, and identity; do not blindly recommend @Data.
- J-04: Consider a shared DTO/entity model only when fields truly repeat the same meaning, type, and behavior; identical names alone do not justify inheritance.
- J-05: Runtime parameters must come from appropriate classes/methods in the `cache` package. Show actual hardcoded or scattered parameter access that bypasses it. Check cache freshness, null handling, and concurrent access in the relevant flow.
- J-06: Method Cognitive Complexity must be <=10. Prefer existing reliable analysis results; otherwise briefly show branching/nesting contributions using Java cognitive complexity rules. Do not substitute cyclomatic complexity or condition counts. If an exact score cannot be established, record an unverified point rather than a threshold violation. Any suggested decomposition must preserve business meaning.
- J-07: Check SOLID, separation of responsibilities, and the change impact of business logic; identify concrete coupling, duplication, or forced changes across components. Assess testability through global mutable state, hidden dependencies, uncontrolled time/I/O, and dependency injection. Missing test files alone do not prove untestability.
- J-08: Every package containing classes must have `package-info.java` with a meaningful package description; check only reviewed packages. Utility classes must have private constructors; group constants in meaningful nested static classes. Do not invent unnecessary shared utilities or constant groups.
- J-09: Check SQL injection/parameter binding, authorization, input validation, secret/personal data logging, unsafe file paths, and deserialization in actual reachable flows.
- J-10: Establish evidence for N+1 queries, repeated DB/I/O calls, unbounded data/memory use, incorrect caching, resource/stream/connection leaks, and timeout behavior. Do not invent numerical performance claims without measurements.
- J-11: Errors are logged in listeners and processing stops. Trace listener wiring, exception propagation, root cause, rollback, and failure status propagation. Report swallowed exceptions, continued success paths, and sensitive data logging. Do not require repeated logging or local catches in every layer.
- J-12: The entire project must be thread-safe. Assess mutable singleton fields, shared collections/caches, check-then-act races, asynchronous state, and resource sharing. Demonstrate that state is actually shared; do not recommend unnecessary synchronization for stateless classes.
