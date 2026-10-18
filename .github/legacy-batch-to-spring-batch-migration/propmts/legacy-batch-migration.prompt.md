---
name: legacy-batch-migration
description: Start legacy batch migration to Java Spring Batch
agent: legacy-batch-migration
---

# Legacy Batch Migration

## Inputs

- Source Project: ${input:sourcePath:Legacy source project path}
- Target Project: ${input:targetPath:Target Java project path}

## Task

Start the Legacy Batch Migration Orchestrator.

- Use the Spring Batch Template defined in the Agent.
- Analyze only the specified legacy batch scope.
- Follow the Agent workflow and approval gates.
- Resume existing migration progress when available.
- Start with Analysis if no previous progress exists.