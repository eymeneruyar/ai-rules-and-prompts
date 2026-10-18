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
- Define shared test constants in `helper/ConstantHelper`.
- Reuse common constant values across test methods.
- Do not redefine equivalent constants inside test methods.
- Use `helper/TestDataHelper` to create reusable test objects such as DTOs and entities.
- Build test objects using values from `ConstantHelper`.
- Prefer reusable factory methods over repeated object initialization in test classes.
- Allow test-specific overrides when different values are required.
- Keep test data helpers simple and free of business logic.
- Avoid creating helper methods for objects used only once.

## Organization
- Group test methods by the production method they test.
- Separate each production-method test group with a clear comment section containing the production method name.