---
paths:
  - "**/e2e/**"
  - "**/*.spec.ts"
  - "**/*.test.ts"
---

# E2E Testing (Playwright)

## Run Tests

```bash
moon bpo-web:test-playwright
```

## User Selection

```typescript
test.use({ user: "user-key" });
```

Users defined in `apps/bpo/web/src/e2e/utils/common/users.ts`

## Test Pattern

```typescript
// 1. Intercept API
const promise = interceptGraphQLResponse(page, "OperationName");

// 2. Navigate
await page.goto("/path");

// 3. Verify API
const response = await promise;
expect(response.data).toBeDefined();

// 4. Verify UI
await assertVisible(page.locator("..."));
```

## Helpers

| Helper | Purpose |
|--------|---------|
| `assertVisible(locator)` | Wait and assert visible |
| `assertCellText(locator, text)` | Assert table cell |
| `interceptGraphQLResponse(page, op)` | Capture GraphQL |

## Locator Priority

1. `getByRole` - Accessibility-first (best)
2. `getByTestId` - Stable identifiers
3. `getByText` - User-visible text
4. CSS selectors - Last resort only

## Test Structure

- Independent tests (no shared state between tests)
- Clear arrange/act/assert sections
- Meaningful assertions with custom error messages
- One user flow per test

## File Structure

```
tests/permissions/client-entity/
├── client.spec.ts
├── provider.spec.ts
└── workspace.spec.ts
```

## Citations

| Fact | Citation |
|------|----------|
| Playwright config | `file:apps/bpo/web/src/e2e/playwright.config.ts` |
| Users file | `file:apps/bpo/web/src/e2e/utils/common/users.ts` |
