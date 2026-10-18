# Common Unit Test Rules

## Coverage
- Target at least 90% class or component-level test coverage.
- Focus on meaningful behavior, branches, edge cases, and error paths.
- Do not create meaningless tests only to reach the coverage target.

## Test Design
- Prefer parameterized or data-driven tests when the same behavior must be verified with multiple input values.
- Do not create separate test methods or cases when the scenarios can reasonably be covered by a parameterized or data-driven test.
- Group tests by the production method, function, or behavior they test.
- Separate test groups with a clear comment section containing the tested method, function, or behavior name.
- Use a maximum of 20 assertions per test method or test case.
- Avoid redundant or duplicate test cases.

## Production Code
- Never modify production code while creating or updating unit tests.
- Write all tests that can reasonably be implemented without changing production code.
- Do not use fragile workarounds, excessive reflection, or implementation-specific hacks only to increase coverage.
- If code cannot reasonably be unit tested without modifying production code, leave that part untested.
- In such cases, identify the affected code and state:
  `Production code should be reviewed for testability.`
- Do not propose or apply production-code changes unless explicitly requested.

## Scope
- Start with the production code under test and its existing test file, if available.
- Inspect only files directly required to understand dependencies, inputs, outputs, or expected behavior.
- Do not inspect unrelated files.
- Do not perform repository-wide exploration unless explicitly requested.
- Do not make unrelated code changes.

## Efficiency
- Use the provided context before searching for additional information.
- Inspect additional files only when necessary to produce correct tests.
- Avoid re-reading or re-analyzing information already available in the current context.
- Prefer targeted dependency inspection over broad repository searches.
- Do not search for similar tests or implementations across the repository unless required to understand expected behavior.
- If critical information cannot be determined from relevant files, do not perform broad exploration or guess the behavior.

## Execution
- Do not automatically run tests.
- Do not execute build, test, coverage, lint, or verification commands unless explicitly requested.

## Output
- Return only the required code changes.
- Do not provide explanations, summaries, test reports, or additional documentation unless explicitly requested.