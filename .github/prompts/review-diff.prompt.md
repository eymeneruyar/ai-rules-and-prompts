---
name: review-diff
description: 'Evidence-based read-only review of Git changes'
argument-hint: 'Optional base ref or explicit base/head range; default staged + unstaged'
agent: agent
---
Read the [shared review/reporting contract](../instructions/team-standards.instructions.md) and [Java rules](../instructions/java-review.instructions.md); do not reopen them if already in context. If dependencies/imports/flows confirm Spring Batch usage, apply the [Batch rules](../instructions/spring-batch-review.instructions.md); otherwise do not open that file. These instruction links apply to read-only reviews too; do not rely solely on automatic applyTo loading.

Scope: with no base, review the combined staged and unstaged tracked changes against HEAD; list untracked files and read them only if explicitly included in the review. With a base ref, review committed changes from the merge base to HEAD (base...HEAD); with an explicit base/head range, review exactly that range. If a ref cannot be resolved, ask; do not fetch/pull or silently choose another base. Record actual refs/commit IDs and local-change scope in the report. Read status and changed-file lists first, then relevant hunks; account for renames and deletions. Report only issues introduced or worsened by the diff; read unchanged code only to verify impact. Prefer changed-line locations; for deletion defects, explicitly identify the old side/line. If the diff is empty, report that and do not switch to project review.

Write confirmed findings according to the shared contract only to `code-review-report.md` at the repository root; do not modify other files. Provide the report link and result in at most two English chat sentences.
