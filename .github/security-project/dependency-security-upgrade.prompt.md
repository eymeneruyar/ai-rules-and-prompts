---
description: "Fix Maven dependency security findings with minimal changes."
---

# Dependency Security Fix

Fix the provided Maven security findings according to `dependency-security.instructions.md`.

- Inspect only what is necessary.
- Make only security-related changes.
- Never change the BOM version.
- Validate changes when possible.
- Keep chat output minimal.

If there are unresolved findings, risks, or manual actions, write only those issues to `dependency-security-report.md`.

If no issues remain, do not create a report.

Final response:
- Success: `Security dependency fixes completed.`
- Issues: `Completed with issues. See dependency-security-report.md.`