Follow all rules defined in:

- [Common Unit Test Rules](../instructions/unit-test-common.instructions.md)
- [Java Unit Test Rules](../instructions/java-unit-test.instructions.md)

Update the existing Java unit tests based on the production code changes.

Use a diff-first approach.

Focus on changed or newly added behavior.
Inspect existing tests only as needed to identify and update affected test cases.

Preserve unaffected tests.
Do not regenerate or review the entire test class unless the production changes require it.

Expand the context beyond the changed code only when necessary to produce correct tests.

Do not run tests.
Do not modify production code.