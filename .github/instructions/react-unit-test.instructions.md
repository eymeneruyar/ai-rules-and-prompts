# React Unit Test Rules

Follow all Common Unit Test Rules.

## Technology
- Use Jest.
- Use the project's existing React testing libraries and utilities.
- Follow existing project conventions for rendering components and mocking dependencies.

## Test Design
- Test observable component behavior rather than implementation details.
- Focus on user-visible output, interactions, state changes, conditional rendering, and error behavior.
- Prefer data-driven tests such as `test.each` when the same behavior must be verified with multiple values.
- Avoid testing trivial implementation details.
- Do not test internal state directly when the same behavior can be verified through observable output.

## Mocking
- Mock only external dependencies that are necessary to isolate the unit under test.
- Avoid unnecessary mocks.
- Do not mock the behavior being tested.
- Reuse existing project mock utilities when available.

## Test Data
- Reuse common test data and constants where appropriate.
- Avoid redefining equivalent test data across multiple test cases.

## Organization
- Group tests by component behavior, function, or logical feature.
- Use `describe` blocks when they improve test organization.
- Separate logical test groups clearly.
- Keep test descriptions concise and behavior-oriented.