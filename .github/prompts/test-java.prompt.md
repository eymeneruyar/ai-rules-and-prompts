Follow all rules defined in:

- [Common Unit Test Rules](../instructions/unit-test-common.instructions.md)
- [Java Unit Test Rules](../instructions/java-unit-test.instructions.md)

Generate or update unit tests for the Java production class provided in the current context.

Treat all referenced unit test rules as mandatory.

Use the provided production class as the primary context.
If a corresponding test class already exists, update it instead of creating a duplicate.

Inspect additional files only when necessary to produce correct tests.

Do not run tests.
Do not modify production code.