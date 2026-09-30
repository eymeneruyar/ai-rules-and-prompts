# Java Unit Test Rules

Follow all Common Unit Test Rules.

## Technology
- Use Java 17 or later.
- Use JUnit 5 and Mockito.
- Use `@Mock` and `@InjectMocks` where applicable.

## Test Design
- Use JUnit 5 parameterized tests when the same behavior must be verified with multiple input values.
- Do not write tests for getters or setters.
- Focus on public behavior rather than implementation details.

## Test Data
- Reuse common constant test values across test methods.
- Define shared test constants in `helper/ConstantHelper`.
- Do not redefine equivalent constant values inside individual test methods.

## Organization
- Group test methods by the production method they test.
- Separate each production-method test group with a clear comment section containing the production method name.