---
name: e2e-testing
description: Playwright E2E testing patterns for BPO/EOR applications.
---

# E2E Testing Skill

## Page Object Model

### Base Page Pattern

```ts
import { Page } from '@playwright/test'

class BasePage {
  constructor(protected page: Page) {}

  async goto(path: string) {
    await this.page.goto(config.baseUrl + path)
  }

  async waitForPageLoad() {
    await this.page.waitForLoadState('networkidle')
  }
}
```

### Extending Pages

```ts
class SettingsPage extends BasePage {
  // Locators as getters for lazy evaluation
  get saveButton() {
    return this.page.getByRole('button', { name: 'Save' })
  }

  get nameInput() {
    return this.page.getByLabel('Name')
  }

  async updateName(name: string) {
    await this.nameInput.fill(name)
    await this.saveButton.click()
  }
}
```

## Locator Priorities

See `rules/e2e-testing.md` for priority order.

**Quick reference:**
```ts
// ✅ Preferred
page.getByRole('button', { name: 'Submit' })
page.getByTestId('user-table')

// ❌ Avoid
page.locator('.btn-primary')
```

## Waiting Patterns

```ts
// ✅ Wait for specific condition
await expect(page.getByText('Success')).toBeVisible()
await page.waitForResponse(resp => resp.url().includes('/api/users'))

// ❌ Avoid arbitrary timeouts
await page.waitForTimeout(3000) // Bad!
```

## Test Structure

```ts
test.describe('User Settings', () => {
  test.beforeEach(async ({ page }) => {
    // Arrange: Set up test state
    await loginAsUser(page)
  })

  test('updates profile name', async ({ page }) => {
    // Arrange
    const settings = new SettingsPage(page)
    await settings.goto('/settings')

    // Act
    await settings.updateName('New Name')

    // Assert
    await expect(settings.nameInput).toHaveValue('New Name')
  })
})
```

