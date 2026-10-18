---
description: 'Apply when reviewing Spring Batch jobs/steps, readers/processors/writers/listeners, and SQL flows.'
applyTo: '**/*[Bb]atch*/**/*.java,**/*[Bb]atch*.java,**/*[Jj]ob*.java,**/*[Ss]tep*.java,**/*[Rr]eader*.java,**/*[Pp]rocessor*.java,**/*[Ww]riter*.java,**/*[Ll]istener*.java,**/src/main/resources/sql/**/*.sql'
---
# Spring Batch review
Apply only to Spring Batch flows; follow the [shared contract](team-standards.instructions.md). Apply these rules when the prompt confirms Batch usage even if filenames do not match.

- B-01: Jobs/steps must follow reader → optional processor → writer. Processors contain business transformation/validation; do not require one when unnecessary. Business DML belongs in writers; inspect reader/processor side effects. Framework metadata operations are not business DML.
- B-02: File readers must support multiple input files. Check resource selection, file order, empty/invalid files, and resource closure.
- B-03: The team standard for DB reads is `JdbcCursorItemReader`. Reader/writer SQL must load from `src/main/resources/sql/<schema_name>/` in the standard source set; for custom source sets, use the verified resource root. Report inline business SQL and incorrect schema/resource paths. Define SQL parameters as query placeholders and supply values through safe binding in reader/writer configuration; never concatenate values into SQL or store secrets in resources.
- B-04: File/data processing must be chunk-based. Assess chunk size, transaction boundaries, rollback, batch DML, cursor/fetch size, and memory against actual volume/configuration evidence; do not suggest arbitrary chunk sizes.
- B-05: Verify that listener error handling/logging ends processing with a failure status; logging alone is insufficient. Check skip/retry/fault-tolerant settings for conflicts with this contract, lost rollbacks, and success transitions to subsequent steps.
- B-06: For parallel steps/partitions/task executors, verify reader/writer/processor and shared-state safety. Do not assume cursor readers are thread-safe; step scope alone does not prevent sharing across threads within one step. Trace partition isolation, transactions, and resource lifecycle.
- B-07: Restartability is only a suggestion for expert assessment; do not classify its absence as a severity-rated finding. The team manages restarts through table flags; do not mandate Spring Batch metadata/log-based restart mechanisms. Provide brief evidence-based suggestions about existing flag transitions, atomicity, partial processing, reprocessing, and idempotency. Independent data integrity defects in normal execution may be reported separately with their own evidence.
- B-08: Until the package tree below is filled in, do not report package-layout violations or propose a default tree.

## Team package tree (to be supplied by the user)
```text

```
