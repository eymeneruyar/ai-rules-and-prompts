---
description: Team Java 17, Spring Boot 3.x and Spring Batch implementation standards
applyTo: "**/*.java"
---

# Java & Spring Batch Team Standards

Follow the approved Spring Batch Template as the primary implementation reference. Where code and these written standards conflict, flag the conflict for design approval; never silently override business requirements.

## Java & Design

- Use Java 17 and Spring Boot 3.x versions compatible with the provided template; retain its Spring Batch version and BOM unless explicitly approved.
- Follow SOLID, Clean Code, single-purpose classes and low-complexity methods. Split complex branching into focused methods/components.
- Use meaningful names: `UpperCamelCase` for classes, `lowerCamelCase` for methods/fields, `UPPER_SNAKE_CASE` for constants and lowercase packages.
- Minimize duplication. Share DTO/entity fields only when their **meaning and lifecycle** match; do not introduce inheritance merely because names match. Prefer composition for DTOs and suitable JPA mappings (`@MappedSuperclass`, `@Embeddable`) for entities where justified.
- Use Lombok for DTOs. Avoid entity annotations that break JPA identity/proxy semantics (for example, indiscriminate `@Data`).
- Favor testable business components and change-localized rules. Apply design patterns only where complexity justifies them; avoid speculative abstractions.
- Include concise `package-info.java` files for relevant packages as required by the team template.
- Make utility class constructors `private`. Group related constants in nested `static final` classes when appropriate; avoid needless duplicates.
- Retrieve business/application parameters through existing methods in the `cache` package. Do not create parallel parameter-loading logic.
- Ensure thread safety for each actual execution model: avoid shared mutable state in singleton beans; scope stateful batch components appropriately and do not share non-thread-safe readers/writers across threads.

## Spring Batch Job Responsibility

- **One Job = one clear business responsibility.** A Job may contain several Steps only if they serve that responsibility.
- Decompose legacy multi-purpose processes rather than copying legacy Job boundaries.
- Separate file ingestion from distinct matching/reconciliation work. If credit, debit and prepaid authorization matching are present, design dedicated Jobs for each.
- Avoid unnecessary Job fragmentation; preserve business behavior and data dependencies.
- Each Job must be independently triggerable. **UC4** owns scheduling, triggering, ordering, inter-Job dependencies and parallel/sequential execution. Do not add `@Scheduled`, in-code Job-to-Job triggering or an internal scheduler.

## Reader → Processor → Writer

- Use Spring Batch Reader → (optional) Processor → Writer conventions. Use chunk-oriented processing for record/file/data processing.
- For database reads use `JdbcCursorItemReader` according to the template's transaction and threading conventions.
- File readers must support multiple input files whenever file ingestion is required.
- Keep transformations, validations and business rules in the Processor or dedicated business components. Omit Processor if not required.
- Perform business database INSERT/UPDATE/DELETE operations in Writer; technical logging continues through the template's logging components.
- Keep SQL in `src/main/resources/sql/<schema_name>/`, loaded through template conventions; bind SQL parameters safely. Never concatenate user data into SQL.
- Preserve required record ordering, fixed-width layouts, encoding, precision, aggregations and trailer/header rules.

## Transactions, Reliability & Performance

- Follow approved chunk, transaction, commit/rollback and resource handling decisions; do not invent transaction equivalence with the legacy system.
- Follow existing flag-based business restart/recovery conventions and design for idempotency where needed. Do not introduce Spring Batch metadata-based **business** restart handling without approval.
- Reuse template listeners, logging, exception handling, cache, shared libraries, configuration and dependency conventions.
- Avoid premature partitioning and multithreading. Propose concurrency only when necessary, safe and approved.
- Avoid excessive DB round-trips, resource leaks and unnecessary full-memory loading.
- Do not change BOM versions, upgrade dependencies or refactor unrelated code without explicit approval.

## Package Structure

<!-- TEAM_PACKAGE_TREE: Paste the team's package-tree below. -->


<!-- END_TEAM_PACKAGE_TREE -->

Follow this package tree once provided. Otherwise preserve the template structure; do not invent a conflicting package hierarchy.

## Migration-Specific Boundary

- Preserve approved business behavior, not the legacy language's implementation techniques.
- Do not generate or run unit tests during the initial migration. Keep resulting code testable; expert review precedes subsequent test generation.
