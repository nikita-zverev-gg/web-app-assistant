---
paths:
  - "**/*.ts"
  - "**/*.tsx"
---

# Code Standards

## TypeScript

```typescript
// Explicit return types on exports
export function calculate(input: Input): Result

// Zod at boundaries
const Schema = z.object({...})

// Discriminated unions for state
type State =
  | { status: 'loading' }
  | { status: 'success'; data: Data }
  | { status: 'error'; error: Error }
```

## Rules

- No `any` types without justification comment
- Explicit return types on exports
- Use absolute imports via tsconfig paths
- Prefer `unknown` over `any` for unknown types

## Testing

```typescript
describe('[Function]', () => {
  describe('[scenario]', () => {
    it('should [behavior]', () => {
      // Arrange
      // Act
      // Assert
    });
  });
});
```

- Tests before implementation (TDD)
- Each test file mirrors source structure
- Descriptive test names explaining behavior
- One assertion concept per test

## Documentation

```typescript
/**
 * Brief description.
 *
 * @param input - What it is
 * @returns What it returns
 */
```

- JSDoc for exported functions
- Update docs when behavior changes
- No redundant comments (code should be self-documenting)

## Imports

- Group: external → internal → types
- Remove unused imports
- Use named exports over default exports
