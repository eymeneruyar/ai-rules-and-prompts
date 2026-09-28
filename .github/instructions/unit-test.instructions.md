# Unit Test Rules

## Technology
- Use Java 17 or later.
- Use JUnit 5 and Mockito.
- Use `@Mock` and `@InjectMocks` where applicable.

## Coverage
- Target at least 90% class-level test coverage.
- Do not write tests for getters or setters.
- Focus on meaningful business logic, branches, and exception paths.

## Test Design
- Prefer parameterized tests when the same behavior must be verified with multiple input values.
- Do not create separate test methods when the scenarios can reasonably be covered by a parameterized test.
- Group test methods by the production method they test.
- Separate each production-method test group with a clear comment section containing the production method name.
- Use a maximum of 20 assertions per test method.
- Avoid redundant or duplicate test cases.

## Test Data
- Reuse common constant test values across all test methods.
- Define shared test constants in `helper/ConstantHelper`.
- Do not redefine equivalent constant values inside individual test methods.

## Production Code
- Never modify production code while creating unit tests.
- Write all tests that can reasonably be implemented without changing production code.
- Do not use fragile workarounds, excessive reflection, or implementation-specific hacks only to increase coverage.
- If a production method or branch cannot reasonably be unit tested without modifying production code, leave that part untested.
- Do not create meaningless tests only to reach the coverage target.
- In such cases, identify the affected method and state:
  `Production method should be reviewed for testability.`
- Do not propose or apply production-code changes unless explicitly requested.

## Scope
- Start with the class under test.
- Inspect only files directly required to understand its dependencies, inputs, outputs, or exceptions.
- Do not inspect unrelated files.
- Do not perform repository-wide exploration unless explicitly requested.
- Do not make unrelated code changes.

## Efficiency
- Use the provided context before searching for additional information.
- Inspect additional files only when necessary to produce correct tests.
- Avoid re-reading or re-analyzing information already available in the current context.
- Prefer targeted dependency inspection over broad repository searches.
- Do not search for similar tests or implementations across the repository unless required to understand the expected behavior.
- If critical information cannot be determined from the relevant files, do not perform broad exploration or guess the behavior.

## Execution
- Do not automatically run tests.
- Do not execute build, test, coverage, or verification commands unless explicitly requested.

## Output
- Return only the required code changes.
- Do not provide explanations, summaries, test reports, or additional documentation unless explicitly requested.