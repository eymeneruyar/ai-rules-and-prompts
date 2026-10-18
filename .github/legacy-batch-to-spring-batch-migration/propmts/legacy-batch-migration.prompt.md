---
name: legacy-batch-migration
description: Migrate legacy batch processes to Java Spring Batch
agent: legacy-batch-orchestrator
---

# Legacy Batch Migration

## Inputs

- Source Project: ${input:sourcePath:Legacy source project path}
- Target Project: ${input:targetPath:Target Java project path}
- Migration Scope: ${input:migrationScope:Batch or business process to migrate}

## Task

Start the Legacy Batch Migration Orchestrator.

- Use the Spring Batch Template configured in the Orchestrator.
- Migrate only the specified business process.
- Follow the Orchestrator workflow and approval gates.
- Resume from the last approved phase if progress exists.
- Otherwise, start with Analysis.
- Do not modify original source or template projects.
- Keep chat responses under 2 sentences.