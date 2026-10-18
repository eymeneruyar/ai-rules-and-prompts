## BOM Policy

- NEVER change the BOM version.
- Treat the existing BOM version as read-only.
- BOM upgrades are performed manually by the developer.
- Do not suggest or apply a BOM upgrade as part of automatic remediation.
- Use the existing BOM only as the compatibility baseline.

## Vulnerable Dependency Policy

For each reported vulnerable dependency:

1. Determine the currently resolved version.
2. Determine whether the version comes from the BOM.
3. Determine the minimum stable version that resolves the reported vulnerability.
4. Check whether that version is compatible with the existing project platform.

If the BOM-managed version is vulnerable:

- Keep the BOM version unchanged.
- Add an explicit version/property override only when required to resolve the finding.
- Use the minimum stable secure version compatible with the existing platform.
- Do not upgrade to the latest version merely because it exists.
- Do not perform major version upgrades automatically.
- If a safe compatible version cannot be established, do not modify the POM.
  Report the dependency for manual review.

If the dependency already has an explicit version:

- Update only that version when necessary.
- Prefer patch over minor upgrades.
- Do not perform major upgrades automatically.

## POM Organization

Keep pom.xml clean and consistently organized.

When modifying dependencies:

- Preserve existing project-specific organization when it is already clear.
- Group related dependencies together.
- Keep dependencies in a predictable order.
- Do not randomly reorder the entire pom.xml for a small security change.
- Do not mix build plugins with application dependencies.
- Keep test dependencies together.
- Keep internal/company dependencies together when identifiable.
- Keep Spring dependencies together.
- Keep third-party dependencies together.

When explicit dependency versions are required:

- Prefer Maven properties for versions that need to override BOM-managed versions.
- Keep version properties together in the `<properties>` section.
- Use descriptive property names.

Example:

<properties>
    <java.version>17</java.version>

    <!-- Security overrides -->
    <netty.version>...</netty.version>
    <commons-compress.version>...</commons-compress.version>
</properties>