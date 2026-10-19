---
name: legacy-batch-migration
description: Migrate legacy applications to Java Spring Batch
agent: legacy-batch-orchestrator
---

# Legacy Batch Migration

## Inputs

- Legacy Source: ${input:legacySource:Legacy project path}
- Target Project: ${input:targetProject:New Java Spring Batch project path}
- Migration Scope: ${input:migrationScope:All batch business processes}

## Task

Start the Legacy Batch Migration Orchestrator.

- Use the configured Spring Batch Template.
- Analyze only the specified legacy scope.
- Follow the defined workflow and approval gates.
- Resume existing migration progress when available.
- Otherwise, start with Analysis.
- Never modify the legacy source or original template.
- Keep chat responses under 2 sentences.