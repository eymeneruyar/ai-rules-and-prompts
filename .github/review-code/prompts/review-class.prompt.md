---
name: review-class
description: 'Evidence-based read-only review of a selected Java class'
argument-hint: 'File path, or attach the class file'
agent: agent
---
Read the [shared review/reporting contract](../instructions/team-standards.instructions.md) and [Java rules](../instructions/java-review.instructions.md); do not reopen them if already in context. If dependencies/imports/flows confirm Spring Batch usage, apply the [Batch rules](../instructions/spring-batch-review.instructions.md); otherwise do not open that file. These instruction links apply to read-only reviews too; do not rely solely on automatic applyTo loading.

Scope: the single Java file explicitly specified or attached by the user; otherwise the active Java file. If the target is ambiguous or multiple targets are supplied, ask only for the target; do not expand to the entire project. If a selection is supplied, review selected members and the class context needed to understand them. Read directly called classes, tests, SQL, listener/configuration, or build excerpts only to verify actual findings; do not expand call chains without bounds.

Write confirmed findings according to the shared contract only to `code-review-report.md` at the repository root; do not modify other files. Provide the report link and result in at most two English chat sentences.
