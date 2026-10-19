---
name: legacy-batch-migration
description: Start or resume a legacy batch migration using the multi-agent orchestrator
agent: legacy-batch-orchestrator
---

# Legacy Batch Migration

- **Legacy source (read-only):** ${input:legacySource:Path to existing C++ / C# / legacy Java project}
- **Target project (writable):** ${input:targetProject:Path to new Java Spring Batch project}
- **Migration scope:** ${input:migrationScope:All batch business processes}
- **Migration name:** ${input:migrationName:Name for migration reports directory}

Use the Spring Batch Template path defined **only** in `legacy-batch-orchestrator.agent.md`.

Start or resume the orchestrated workflow for this scope. Follow the two human approvals and the **external SQL readiness gate** (user manually supplies `queries/<QUERY_NAME>.sql` after Analysis and before Design). Keep originals unchanged; specialist agents create bilingual TR/EN reports. No unit tests; implementation ends with compile/static checks and expert-review handoff. Do not repeat the agents' instructions in chat.
