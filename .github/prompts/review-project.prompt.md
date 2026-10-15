---
name: review-project
description: 'Evidence-based read-only review of a project or module'
argument-hint: 'Optional module/directory path'
agent: agent
---
Read the [shared review/reporting contract](../instructions/team-standards.instructions.md) and [Java rules](../instructions/java-review.instructions.md); do not reopen them if already in context. If dependencies/imports/flows confirm Spring Batch usage, apply the [Batch rules](../instructions/spring-batch-review.instructions.md); otherwise do not open that file. These instruction links apply to read-only reviews too; do not rely solely on automatic applyTo loading.

Scope: the user-specified module/directory, or the repository if omitted. Start with file inventories and relevant build definitions to establish Java/Boot/Batch scope. Review production Java and its relevant SQL/configuration/test flows module by module; do not claim full-project coverage after reading only risky samples. Process files in small groups and retain brief finding notes instead of rereading. If context or access limits prevent completion, explicitly report reviewed and remaining scope; continue through accessible scope.

Write confirmed findings according to the shared contract only to `code-review-report.md` at the repository root; do not modify other files. Provide the report link and result in at most two English chat sentences.
