Follow all rules defined in:
[Unit Test Rules](../instructions/unit-test.instructions.md)

Generate or update unit tests for the Java production class provided in the current context.

Treat the referenced Unit Test Rules as mandatory.

Use the provided production class as the primary context.
Inspect only directly related files when necessary to produce correct tests.

If a corresponding test class already exists, update it instead of creating a duplicate.

Do not run tests.
Do not modify production code.